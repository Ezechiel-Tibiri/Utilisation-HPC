##  Exercices pour utiliser un cluster de calcul
### Logiciels à installer
* [putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
* [filezilla](https://filezilla-project.org/)
Transférer des fichiers depuis votre ordinateur vers des serveurs Linux et inversement avec SFTP (SSH File Transfer Protocol)

###Exercice 1: Se connecter à un serveur Linux avec `ssh`
* 1. taper votre identifiant (username) et le l'adresse IP `165.16.215.34`
```
ssh tibionez@165.16.215.34
```
* 2. Dans le champ, entrer le mot de passe ****** quand il est demandé. 
* 3. Taper la commande `sinfo` et commenter le resultat
* 4. Taper la commande `scontrol shown nodes` et commenter le resultat

### Exercice 2: Reserver un coeur sur le noeud de calcul et créer son répertoire de travail
* 1. Taper la commande `squeue` et commenter le résultat
* 2. Taper la commande
```
srun --time=60:00 -p short --pty bash -i
```
puis
```
squeue
```
une nouvelle fois

* 3. Taper la commande `squeue -u` et commenter le résultats
* 4. Créer votre répertoire de travail dans `/tmp` du noeud:
```
cd /tmp
 mkdir exo1_username
```

### Exercice 3: Transférer des fichiers avec Filezilla `sftp`

* 1. Depuis votre ordinateur vers le cluster : cliquer et déposer le fichier depuis la colonne de gauche vers la colonne de droite
* 2. Du cluster vers votre ordinateur : cliquer et déposer le fichier depuis la colonne de droite vers la colonne de gauche
* 3. Récupérer le fichier HPC_ouaga_oct2019.pdf situé dans le répertoire `/opt/HPC`

### Exercice 4: Transférer des fichiers au noeud de calcul avec `scp`

* 1. En utilisant `scp`, transférer le répertoire `tp-cluster` situé dans `/opt` dans votre répertoire de travail
* 2. Vérifier que le transfert s’est bien déroulé avec la commande `ls`.

### Exercice 5: Utiliser Module Environment pour charger ses outils
* 1. Charger le *module blast+ vers 2.7.1*
* 2. Vérifier que le module soit chargé.

### Exercice 6: Lancer ses analyses

Aller dans le répertoire Blast et taper la commande suivante:
```
$ blastn -db All-EST-coffea.fasta -query sequence-NMT.fasta -out blastn.out
```
Bonus:

Aller dans le répertoire `/tmp/formationX/BWA`

Charger le *module bwa v 0.7.17*

Puis lancer les commandes suivantes:
```
bwa index Reference.fasta
bwa mem reference.fasta RC1_1_CUTADAPT_forwardRepaired.fastq RC1_2_CUTADAPT_reverseRepaired.fastq > mapping.sam
```
### Exercice 7: Transférer ses résultats vers son /home avec scp

* 1. En utilisant `scp`, transférer vos résultatx depuis votre `/tmp/username` vers votre `/home/username`
* 2. Vérifier que le transfert est OK avec la commande `ls`

###Exercice 8: Supprimer vos répertoires de données d’analyse
```
 cd /tmp
rm -r exo_username
exit
```
### Exercice 9: Lancer un job en mode batch
S’inspirer du script suivant pour lancer une analyse blast :

Exemple de script slurm:
```
#!/bin/bash
## On définit le nom du job
#SBATCH --job-name=test
## On définit le nom du fichier de sortie
#SBATCH --output=res.txt
## On définit le nombre de tâches
#SBATCH --ntasks=1
## On définit le temps limit d'éxécution
#SBATCH --time=10:00
## On définit 100Mo de mémoire par cpu
#SBATCH --mem-per-cpu=100
sleep 180 #on lance un sleep de 3 minutes
```
Taper toutes les commandes utilisées au cours du tp.

Le script généré permettra de les lancer de manière automatique.

Une analyse sera lancée ensuite grâce à la commande:
```
sbatch script.sh
```
Avec `script.sh` le nom du script à utiliser
