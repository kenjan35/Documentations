### Qu'est-ce qu'un pod ?
Un pod (terme anglo-saxon décrivant un groupe de baleines ou une gousse de pois) est un groupe d'un ou plusieurs conteneurs (comme des conteneurs Docker), ayant du stockage/réseau partagé, et une spécification sur la manière d'exécuter ces conteneurs.

Les conteneurs d'un pod partagent une adresse IP et un espace de ports, et peuvent communiquer via localhost. Ils peuvent aussi communiquer entre eux en utilisant des communications inter-process standard comme les sémaphores SystemV ou la mémoire partagée POSIX. 

### Intérêts des pods
#### Gestion
La co-localisation (co-ordonnancement), la fin partagée (par ex. l'arrêt), la réplication coordonnée, le partage de ressources et la gestion des dépendances sont traités automatiquement pour les conteneurs dans un pod.

#### Partage de ressources et communication
Les applications dans un pod utilisent toutes le même réseau (même adresse IP et espace de ports) et peuvent donc "se trouver" entre elles et communiquer en utilisant localhost. À cause de cela, les applications dans un pod doivent coordonner leurs usages de ports.

### Cas d'utilisation de pods
Des pods peuvent être utilisés pour héberger verticalement des piles applicatives intégrées (par ex. LAMP), mais leur principal intérêt est la mise en place de programmes auxiliaires co-localisés et co-gérés, comme :

* systèmes de gestion de contenu, chargeurs de fichiers et de données, gestionnaires de cache local, etc.
* sauvegarde de log et checkpoint, compression, rotation, prise d'instantanés, etc.
* data change watchers, log tailers, adaptateurs de logs et monitoring, éditeurs d'événements, etc.
* proxies, bridges et adaptateurs
* contrôleurs, gestionnaires, configurateurs et gestionnaires de mise à jour

### Alternatives envisagées
Pourquoi ne pas simplement exécuter plusieurs programmes dans un unique conteneur (Docker) ?

1. Transparence. Rendre les conteneurs à l'intérieur du pod visibles par l'infrastucture permet à l'infrastucture de fournir des services à ces conteneurs, comme la gestion des processus et le monitoring des ressources. Ceci apporte un certain nombre de facilités aux utilisateurs.
2. Découpler les dépendances logicielles. Les conteneurs individuels peuvent être versionnés, reconstruits et redéployés de manière indépendante. Kubernetes pourrait même un jour prendre en charge la mise à jour à chaud de conteneurs individuels.
3. Facilité d'utilisation. Les utilisateurs n'ont pas besoin d'exécuter leur propre gestionnaire de processus, de se soucier de la propagation de signaux et de codes de sortie, etc.
4. Efficacité. L'infrastructure prenant plus de responsabilités, les conteneurs peuvent être plus légers.
Pourquoi ne pas prendre en charge le co-ordonnancement de conteneurs basé sur les affinités ?

Cette approche pourrait fournir la co-localisation, mais ne fournirait pas la plupart des bénéfices des pods, comme le partage de ressources, IPC, la garantie d'une fin partagée et une gestion simplifiée.

### Durabilité des pods (ou manque de)
Les pods ne doivent pas être considérés comme des entités durables. Ils ne survivent pas à des erreurs d'ordonnancement, à un nœud en échec ou à d'autres expulsions, suite à un manque de ressources ou une mise en maintenance d'un nœud.

### Arrêt de pods
Les pods représentant des processus s'exécutant sur des nœuds d'un cluster, il est important de permettre à ces processus de se terminer proprement lorsqu'ils ne sont plus nécessaires (plutôt que d'être violemment tués avec un signal KILL et n'avoir aucune chance de libérer ses ressources). Les utilisateurs doivent pouvoir demander une suppression et savoir quand les processus se terminent, mais aussi être capable de s'assurer que la suppression est réellement effective.

Un exemple de déroulement :

1. Un utilisateur envoie une commande pour supprimer un Pod, avec une période de grâce par défaut (30s)
2. Le Pod dans l'API server est mis à jour avec le temps au delà duquel le Pod est considéré "mort" ainsi que la période de grâce.
3. Le Pod est affiché comme "Terminating" dans les listes des commandes client
4. (en même temps que 3) Lorsque Kubelet voit qu'un Pod a été marqué "Terminating", le temps ayant été mis en 2, il commence le processus de suppression du pod.
    1. Si un des conteneurs du Pod a défini un preStop hook, il est exécuté à l'intérieur du conteneur. Si le preStop hook est toujours en cours d'exécution à la fin de la période de grâce, l'étape 2 est invoquée avec une courte (2 secondes) période de grâce supplémentaire une seule fois. Vous devez modifier terminationGracePeriodSeconds si le hook preStop a besoin de plus de temps pour se terminer.
    2. Le signal TERM est envoyé aux conteneurs. Notez que tous les conteneurs du Pod ne recevront pas le signal TERM en même temps et il peut être nécessaire de définir des preStop hook si l'ordre d'arrêt est important.
5. (en même temps que 3) Le Pod est supprimé des listes d'endpoints des services, et n'est plus considéré comme faisant partie des pods en cours d'exécution pour les contrôleurs de réplication. Les Pods s'arrêtant lentement ne peuvent pas continuer à servir du trafic, les load balancers (comme le service proxy) les supprimant de leurs rotations.
6. Lorsque la période de grâce expire, les processus s'exécutant toujours dans le Pod sont tués avec SIGKILL.
7. Kubelet va supprimer le Pod dans l'API server en indiquant une période de grâce de 0 (suppression immédiate). Le Pod disparaît de l'API et n'est plus visible par le client.
