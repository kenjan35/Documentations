Kubernetes est une plateforme open source portable et extensible pour gérer les charges de travail et les services conteneurisés, qui facilite à la fois la configuration déclarative et l'automatisation.

Kubernetes n'est pas un système PaaS (Platform as a Service) traditionnel et tout compris.
 Étant donné que Kubernetes fonctionne au niveau des conteneurs plutôt qu'au niveau du matériel, il fournit certaines fonctionnalités généralement applicables communes aux offres PaaS, telles que le déploiement, la mise à l'échelle, l'équilibrage de charge, et permet aux utilisateurs d'intégrer leurs solutions de journalisation, de surveillance et d'alerte.

Docker sert principalement à créer et exécuter des conteneurs. Kubernetes sert à gérer et orchestrer des conteneurs, souvent sur plusieurs machines.

```
Imagine que tu as :

        Kubernetes
             │
    ┌────────┼────────┐
    ↓        ↓        ↓
 Node 1    Node 2    Node 3
    │        │        │
  Pod      Pod      Pod
   │        │        │
Container Container Container
```

Kubernetes peut notamment :

* démarrer des conteneurs ;
* arrêter/remplacer automatiquement des conteneurs ;
* redémarrer une application qui plante ;
* répartir les applications entre plusieurs machines ;
* faire du scaling ;
* gérer le réseau entre les applications ;
* effectuer des mises à jour progressivement ;
* exposer les applications à travers des Services/Ingress ;
* maintenir l'état souhaité du système.

Par exemple, tu demandes :
```
Je veux 3 instances de mon application.
```
Kubernetes essaie constamment de maintenir :

```
Application
├── Pod 1
├── Pod 2
└── Pod 3
```

Si Pod 2 tombe :

```
Application
├── Pod 1
├── ❌ Pod 2
└── Pod 3
```

Kubernetes peut créer automatiquement un nouveau Pod :

```
Application
├── Pod 1
├── Pod 3
└── Pod 4
```

Un Pod est la plus petite unité déployable de Kubernetes.

Le point important à retenir :

Un Pod est une enveloppe dans laquelle Kubernetes fait tourner un ou plusieurs conteneurs.

1. Le rapport Docker → Pod

Avec Docker, tu peux avoir :

```
Docker
  │
  └── Conteneur
       └── Application
```

Avec Kubernetes :

```
Kubernetes
    │
    └── Pod
         │
         └── Conteneur
              └── Application
```

## Comprendre la communication entre Server et ServerWorker
Avant d'installer K3s, il faut comprendre comment les deux machines vont communiquer.

Notre objectif est de comprendre ce qui se passe lorsqu'un Worker rejoint un cluster Kubernetes.
### 1. Comprendre le rôle du Server
Le Server va héberger le Control Plane de Kubernetes.

Il expose notamment une API appelée Kubernetes API Server.
```
Server — 192.168.56.110
K3s Server
     |
     |
Kubernetes API Server
6443
Port TCP utilisé par les agents pour communiquer avec le serveur
     |
     |
ServerWorker — 192.168.56.111
K3s Agent
```

Le Worker devra pouvoir contacter l'API Server sur le port TCP 6443.

### 2. Comprendre les ports réseau
Voici les principaux ports à connaître pour ton projet :
```
Port	Protocole	Utilisation
6443	TCP	Kubernetes API Server
10250	TCP	Kubelet API
8472	UDP	Flannel VXLAN (si utilisé)
22	TCP	SSH
```

Attention : tous ces ports n'ont pas besoin d'être ouverts sur toutes les interfaces. Par exemple, le port 6443 doit être accessible depuis les agents vers le Server.

### 3. Tester la connectivité du port 6443
Pour le moment, K3s n'est pas encore installé. Il est donc normal que le port 6443 ne soit pas ouvert.

Depuis ServerWorker, tu peux tester :
```bash
nc -zv 192.168.56.110 6443
```

Tu obtiendras probablement une erreur de connexion refusée.

C'est normal : aucun service n'écoute encore sur ce port.

Tu peux également vérifier les interfaces réseau :
```bash
ip addr
```

Et les routes :
```bash
ip route
```

Ces deux commandes sont importantes pour comprendre comment Linux choisit une interface pour joindre une adresse IP.

### 4. Comprendre le fonctionnement du token
Une fois K3s installé sur Server, un fichier sera créé :
```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

Ce fichier contient le token utilisé pour authentifier les agents qui souhaitent rejoindre le cluster.

Le Worker aura besoin de deux informations :
```
K3S_URL
K3S_TOKEN
```

Par exemple :
```
K3S_URL=https://192.168.56.110:6443
K3S_TOKEN=<token-du-server>
```

Le token est un secret : ne le publie pas et ne le place pas directement dans un dépôt Git.

## Installation de K3s Server

### 1. Se connecter au Server

Depuis l'ordinateur :

```bash
vagrant ssh atolojanS
```

### Comprendre ce que nous allons installer

K3s est une distribution legere de Kubernetes.

Lorsqu'on installe K3s en mode Server, plusieurs composants sont installes et configures automatiquement.

```md
K3s Server

    **API Server**
    Reçoit les requêtes Kubernetes.

    **Scheduler**
    Décide sur quel Worker placer les Pods.

    **Controller Manager**
    Maintient le cluster dans l'état souhaité.

    **Datastore**
    Stocke l'état du cluster (SQLite par défaut pour un Server K3s autonome).
```

Tu n'as pas besoin d'installer chacun de ces composants manuellement.


