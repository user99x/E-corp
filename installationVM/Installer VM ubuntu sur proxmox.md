Prérequis : 
* 32 Go dispo, 2 coeurs, 2 giga de ram,
* avoir l'image iso (suivre doc max)

## Créer la VM
![[Pasted image 20241022130205.png]]
### General
![[Pasted image 20241022130306.png]]
* Choisir sa node
* chosir son ID (s'incrémente au fur et a mesure que l'on créer des vm donc pas toucher)
* Choisir le nom
### OS
* Choisir ubuntu-24.04.....

### System
![[Pasted image 20241022130618.png]]
* Choisir VirtIO SCSI

### Disks

![[Pasted image 20241022130716.png]]
* Choisir la taille se son disque : 32

### CPU
![[Pasted image 20241022130834.png]]
* 2 coeurs
* kvm64
### Memory
![[Pasted image 20241022130925.png]]
### Network
![[Pasted image 20241022130957.png]]

## Lancer sa VM

Aller dans l'onglet "virtual machine", puis appuyer sur Start.

## Configuration de l'installation

Bien choisir le nom de l'utilisateur, serveur, et adresse ip du serveur.
La gateway est 192.168.0.1.
