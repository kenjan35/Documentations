## API (Application Programming Interface) :
C'est une interface qui permet à deux programmes de communiquer entre eux.

API SOAP ou REST
Pour standardiser l'échange des informations entre les API toujours plus nombreuses, il a fallu développer un protocole : le « Simple Object Access Protocol », plus connu sous le nom de SOAP. Les API conçues d'après le protocole SOAP utilisent le format XML pour leurs messages et reçoivent des requêtes via HTTP ou SMTP. SOAP a pour objectif de simplifier l'échange des informations entre les applications qui s'exécutent dans des environnements différents ou qui ont été écrites dans des langages différents.

Le « Representational State Transfer », ou REST, est une autre tentative de normalisation. Les API web qui respectent les contraintes de l'architecture REST sont appelées API RESTful. Ces deux éléments diffèrent sur un point fondamental : SOAP est un protocole, alors que REST est un style d'architecture. Cela signifie qu'il n'existe aucune norme officielle qui régit les API web RESTful. Selon la définition proposée par Roy Fielding dans sa thèse « Architectural Styles and the Design of Network-based Software Architectures », les API sont RESTful tant qu'elles respectent les six contraintes de conception d'un système RESTful :

* Architecture client-serveur : une architecture REST est composée de clients, de serveurs et de ressources et elle traite les requêtes via le protocole HTTP.
* Serveur stateless : le contenu du client n'est jamais stocké sur le serveur entre les requêtes. Les informations sur l'état de la session sont, quant à elles, stockées sur le client.
* Mémoire cache : la mise en mémoire cache permet de se passer de certaines interactions entre le client et le serveur.
* Système à couches : des couches supplémentaires peuvent assurer la médiation dans les interactions entre le client et le serveur. Ces couches peuvent remplir des fonctions supplémentaires, telles que l'équilibrage de charge, le partage des caches ou la sécurité.
* Code à la demande (facultatif) : un serveur peut étendre les fonctionnalités d'un client en lui transférant du code exécutable.
* Interface uniforme : cette contrainte est capitale pour la conception des API RESTful et couvre quatre aspects différents :
  * Identification des ressources dans les requêtes : les ressources sont identifiées dans les requêtes et sont séparées des représentations retournées au client.
  * Manipulation des ressources par des représentations : les clients reçoivent des fichiers qui représentent les ressources. Ces représentations doivent contenir suffisamment d'informations pour être modifiées ou supprimées.
  * Messages autodescriptifs : tous les messages renvoyés au client contiennent assez d'informations pour décrire la manière dont celui-ci doit traiter les informations.
  * Hypermédia comme moteur du changement des états applicatifs : après avoir accédé à une ressource, le client REST doit être en mesure de découvrir toutes les autres actions disponibles par des hyperliens.
Ces contraintes peuvent sembler difficiles à appliquer, mais dans les faits, elles le sont moins qu'un protocole. C'est pour cette raison que les API RESTful prennent progressivement le pas sur les API SOAP.

Ces dernières années, la spécification OpenAPI s'est imposée comme la norme commune pour définir les API REST. La norme OpenAPI permet aux développeurs de créer des interfaces d'API REST indépendantes du langage de manière à ce que les utilisateurs puissent les comprendre avec un minimum d'approximation.

Une autre norme d'API est en train d'émerger : GraphQL, un langage de requête et un environnement d'exécution côté serveur qui se propose de remplacer l'architecture REST. GraphQL s'attache à fournir aux clients uniquement les données qu'ils ont demandées, et rien de plus. Utilisé à la place de REST, GraphQL permet aux développeurs de créer des requêtes qui extraient les données de plusieurs sources à l'aide d'un seul appel d'API.

## CI/CD :
Le CI/CD désigne l'intégration continue et la livraison ou le déploiement continu, des pratiques clés du développement logiciel qui automatisent la construction, les tests et la mise en production des codes.

* Intégration Continue (CI)
  * Fusion fréquente : les développeurs ajoutent leur code dans un dépôt commun plusieurs fois par jour.
  * Tests automatiques : le système lance des tests pour trouver les erreurs tout de suite.
  * Correction rapide : les équipes réparent les bugs avant qu'ils ne grossissent.

* Livraison et Déploiement Continus (CD)
  * Livraison continue : le code prêt est validé pour aller en phase de test final (staging).
  * Déploiement continu : le code validé est envoyé directement aux utilisateurs sans action humaine.
  * Moins d'erreurs : l'automatisation évite les oublis et les gestes manuels.

## Hyperviseur :
C'est un logiciel qui permet de faire tourner un ou plusieurs systèmes d'exploitation sur un seul ordinateur physique.

  * **Type 1** (Natif ou Bare Metal) : Il s'installe directement sur le matériel de l'ordinateur. Il est très rapide et sert surtout pour les serveurs professionnels. Exemple : VMware ESXi, KVM, Microsoft Hyper-V.
  * **Type 2** (Hébergé) : Il s'installe comme un programme classique sur un système d'exploitation déjà présent. Il est idéal pour tester des choses sur son propre ordinateur. Exemple : VirtualBox, VMware Workstation.

## MaaS (Model as a Service) :
C'est un service cloud qui fournit des outils, des frameworks et des API d’apprentissage automatique pour le développement de modèles IA. Ses utilisateurs cibles incluent des scientifiques des données, des ingénieurs en IA et des entreprises cherchant à tirer parti de l’apprentissage automatique sans avoir à construire une infrastructure à partir de rien.

**Exemple :**
L'utilisation de l'API OpenAI pour intégrer GPT-4 dans un chatbot d'entreprise

## PaaS (Platform as a Service) : 
C'est un modèle de cloud computing qui fournit aux développeurs une plateforme pour créer, déployer et gérer des applications sans se soucier de l’infrastructure sous-jacente. Il permet aux développeurs de se concentrer sur l’écriture de code, tandis que le fournisseur de cloud gère l’infrastructure, la maintenance et la scalabilité.

**Exemple :**
Heroku, Google App Engine, Microsoft Azure App Service, Vercel et Clever Cloud.

## SaaS (software as a Service) :
C'est une solution logicielle entièrement managée auxquelles les utilisateurs accèdent via Internet sans installation. Les applications sont hébergées et gérées par un fournisseur de services. Les utilisateurs n’ont pas à se soucier de l’infrastructure sous-jacente ou de la maintenance.

**Exemple :**
Canva pour le design, Slack pour la messagerie d'équipe, Netflix pour la vidéo, et Microsoft 365 pour la bureautique.

## URI (Uniform Resource Identifier) : 
C'est une adresse qui permet d'identifier une ressource.

**Exemple :**

Quand on fait :
```powershell
start ms-settings:
```
ms-settings: est un URI.
