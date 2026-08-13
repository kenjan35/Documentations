## C'est quoi un Vagrantfile ?

Un Vagrantfile est un fichier écrit en Ruby qui décrit une machine virtuelle.

Au lieu de créer une VM à la main dans VirtualBox :
* choisir Ubuntu
* donner 2 Go de RAM
* ajouter un réseau privé
* partager un dossier
* installer nginx

On écrit simplement un fichier :

```ruby
Vagrant.configure("2") do |config|

end
```

Puis on lance :

```bash
vagrant up
```

et tout est créé automatiquement.

## Structure d'un Vagrantfile

Voici le plus petit Vagrantfile possible :

```ruby
Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/jammy64"
end
```

Regardons chaque ligne.

#### 1. Vagrant.configure("2")

```ruby
Vagrant.configure("2") do |config|
```

Cela signifie :

"Je vais utiliser la version 2 du format de configuration."

The important thing to understand as a general user of Vagrant is that within a single configuration section, only a single version can be used. You cannot use the new config.vm.provider configurations in a version 1 configuration section. Likewise, config.vm.forward_port will not work in a version 2 configuration section (it was renamed). (From https://developer.hashicorp.com/vagrant/docs/vagrantfile/version)

Le mot config est simplement une variable.

On pourrait écrire :

```ruby
Vagrant.configure("2") do |machine|
```

ou

```ruby
Vagrant.configure("2") do |banana|
```

mais tout le monde utilise :

```ruby
config
```

#### 2. config.vm.box

```ruby
config.vm.box = "ubuntu/jammy64"
```

Une **box** est une image de machine virtuelle.

Comme Docker possède :

* ubuntu
* alpine
* debian

Vagrant possède :

* ubuntu/jammy64
* debian/bookworm64
* generic/alpine319

Lorsqu'on fait :

```bash
vagrant up
```

Vagrant télécharge automatiquement cette box si elle n'est pas déjà présente.

Le bloc se termine

```ruby
end
```

Il ferme le bloc commencé par :

```ruby
do
```

## Ajouter un nom

On peut écrire :

```ruby
Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/jammy64"
    config.vm.hostname = "serveur-web"

end
```

Une fois connecté :

```ruby
hostname
```

on obtiendra :

```ruby
serveur-web
```

## Donner de la RAM

```ruby
Vagrant.configure("2") do |config|

    config.vm.box = "ubuntu/jammy64"

    config.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
    end

end
```

Ici :

```ruby
config.vm.provider
```

signifie :

"Lorsqu'on utilise VirtualBox..."

et

```ruby
vb.memory = 2048
```

donne :

```
2 Go de RAM
```

On peut aussi ajouter :

```ruby
vb.cpus = 2
```

## Configurer le réseau

Une IP privée :

```ruby
config.vm.network "private_network", ip: "192.168.56.10"
```

La VM aura donc :

```
192.168.56.10
```

## Dossier partagé

```ruby
config.vm.synced_folder "./data", "/home/vagrant/data"
```

Cela signifie :

```
PC
|
|-- projet
    |-- data
```

sera visible dans la VM ici :

```
/home/vagrant/data
```

## Installer un logiciel automatiquement

On peut exécuter un script Shell au premier démarrage :

```ruby
config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y nginx
SHELL
```

Lorsqu'on fait :

```
vagrant up
```

Vagrant :

* crée la VM
* démarre Ubuntu
* lance apt update
* installe Nginx

On n'a rien à faire.
