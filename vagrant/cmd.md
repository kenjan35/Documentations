## init

Cette commande crée un fichier Vagrantfile dans le répertoire courant.

Par exemple :

```bash
mkdir mon_projet
cd mon_projet

vagrant init
```

On obtiendra :

```
mon_projet/
└── Vagrantfile
```

Ce fichier contient un modèle de configuration que tu pourras modifier.

Que se passe-t-il en interne ?

Lorsqu'on exécute :

```bash
vagrant init
```

Vagrant :

1. vérifie que le dossier ne contient pas déjà un Vagrantfile ;
2. crée un nouveau fichier Vagrantfile avec des commentaires et des exemples ;
3. n'installe aucune machine virtuelle ;
4. ne télécharge aucune box ;
5. ne démarre rien.

Autrement dit :

vagrant init prépare uniquement le projet.

### Options

* --force : Si spécifié, cette commande va écraser le Vagrantfile existant.

Exemple :

```bash
vagrant init -f hashicorp/bionic64
```

## up

### Étape 1 : Lire le Vagrantfile

Il commence par ouvrir ton fichier :

```
Vagrantfile
```

Il analyse toutes les directives :

* quelle box utiliser ?
* VirtualBox ou VMware ?
* combien de RAM ?
* combien de CPU ?
* réseau ?
* dossiers partagés ?
* scripts d'installation ?

### Étape 2 : Vérifier la box

Il regarde si :

```
ubuntu/jammy64
```

est déjà présente sur ton ordinateur.

#### Cas 1 : la box existe

Il l'utilise directement.

#### Cas 2 : elle n'existe pas

Il la télécharge automatiquement.

Tu verras quelque chose comme :

==> default: Box 'ubuntu/jammy64' could not be found.
==> default: Downloading...

Une fois téléchargée, elle sera réutilisée pour les prochains projets utilisant cette même box.

#### Étape 3 : Créer la machine virtuelle

À partir de cette box, Vagrant demande à VirtualBox de créer une nouvelle VM.

C'est l'équivalent de :

* Nouvelle VM
* Ubuntu
* Disque virtuel
* Configuration

mais tout est automatique.

#### Étape 4 : Configurer la VM

Il applique ensuite les paramètres définis dans le Vagrantfile :

Par exemple :

```ruby
vb.memory = 2048
```

↓

RAM = 2 Go

```ruby
vb.cpus = 2
```

↓

2 processeurs virtuels

```ruby
config.vm.hostname = "server"
```

↓

Nom de la machine :

```
server
```

```ruby
config.vm.network ...
```

↓

Configuration des interfaces réseau.

#### Étape 5 : Démarrer la VM

VirtualBox démarre la machine.

C'est comme si tu cliquais sur :

```
Start
```

dans l'interface graphique de VirtualBox.

#### Étape 6 : Provisionnement

Si tu as défini un provisionneur :

```ruby
config.vm.provision "shell", inline: <<-SHELL
apt update
apt install -y nginx
SHELL
```

Vagrant exécute ces commandes à l'intérieur de la VM.

Il se connecte automatiquement et lance :

```
apt update
apt install -y nginx
```

Tu n'as rien à faire.

#### Étape 7 : La VM est prête

À la fin, tu verras un message indiquant que la machine est prête.

Tu peux alors te connecter avec :

```
vagrant ssh
```

#### *Que se passe-t-il si je relance vagrant up ?*

Supposons que la VM existe déjà.

Tu exécutes de nouveau :

```
vagrant up
```

Vagrant vérifie son état.

Si la VM est arrêtée

Il la redémarre simplement.

Si elle est déjà démarrée

Il affiche un message du type :

```bash
Machine already provisioned.
Machine already running.
```

Il ne recrée pas une nouvelle VM.

## ssh

Elle permet de se connecter à la machine virtuelle en SSH.

```
vagrant ssh
```

Au lieu d'ouvrir VirtualBox et de te connecter manuellement, Vagrant utilise automatiquement :

* l'adresse IP,
* le port SSH,
* le nom d'utilisateur,
* la clé SSH.

Tu arrives directement dans le terminal de la VM.

Exemple :

```bash
$ vagrant ssh

vagrant@ubuntu:~$
```

Tu peux alors exécuter des commandes Linux :

```bash
pwd
ls
ip addr
hostname
```

Pour quitter la machine :

```bash
exit
```

Tu reviens sur ton ordinateur hôte.

## halt

Elle arrête proprement la machine virtuelle.

```bash
vagrant halt
```

C'est l'équivalent de faire :

```bash
sudo shutdown -h now
```

à l'intérieur de la VM.

La machine est éteinte mais elle n'est pas supprimée.

Toutes tes données restent présentes.

Tu peux la rallumer avec :

```bash
vagrant up
```

## reload

Cette commande redémarre la machine.

```bash
vagrant reload
```

C'est l'équivalent de :

```
Arrêter
    ↓
Redémarrer
```

Pourquoi faire un reload ?

Supposons que tu modifies le Vagrantfile.

Avant :

```ruby
vb.memory = 1024
```

Après :

```ruby
vb.memory = 4096
```

La VM utilise toujours l'ancienne configuration.

Il faut donc :

```bash
vagrant reload
```

Vagrant :

1. arrête la VM ;
2. applique les nouveaux paramètres (si possible) ;
3. redémarre la VM.

Avec provisionnement

Tu peux également exécuter :

```bash
vagrant reload --provision
```

Dans ce cas :

```
Arrêt
↓
Démarrage
↓
Réexécution des scripts de provisionnement
```

C'est pratique lorsque tu modifies un script d'installation.

## destroy

Cette commande supprime complètement la machine virtuelle.

```
vagrant destroy
```

Vagrant te demandera généralement une confirmation :

```
Are you sure you want to destroy the machine? [y/N]
```

Si tu réponds :

```
y
```

La VM est supprimée.

Ce qui est supprimé

* le disque virtuel ;
* la mémoire de la VM (si elle était sauvegardée) ;
* les paramètres de la machine ;
* la VM dans VirtualBox.

Ce qui n'est pas supprimé

Ton dossier de projet reste intact.

Par exemple :

```
Projet/
│── Vagrantfile
│── scripts/
│── data/
```

reste sur ton ordinateur.

Tu peux ensuite recréer une nouvelle VM avec :

```
vagrant up
```
