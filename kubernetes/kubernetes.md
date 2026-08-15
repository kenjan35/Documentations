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
