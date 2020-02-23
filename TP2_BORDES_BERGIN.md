# TP2-Emile_BERGIN-Corentin_BORDES

## Exercice 1. Variables d’environnement

1) Les commandes bash se trouvent dans le fichier .bash_history situé dans le home directory.

2) La commande est "cd $HOME"

3) * LANG = "Language" détermine la langue que les logiciels utilisent pour communiquer avec l’utilisateur.

	 * PWD = " print working directory ". Elle permet d'afficher le chemin d'accès vers le répertoire où se situe l'utilisateur qui a entré la commande.
	 
	 * OLDPWD = " OLDPrintWorkingDirectory ". Contient le repertoire avant la derniere commande cd.
	 
	 * $SHELL = path to /bin/bash = $BASH.
	  
	 * $_ = derniere variable en dernier argument de la derniere commande executé

4) MY_VAR='Bla'

5) La commande bash sans argument redémarre une console.
		
6) export MY_VAR, cela permet de créer une variable d'environnement disponible dans n'importe quel terminal bash.

7) export NOMS='BERGIN BORDES';
	 printenv NOMS;

8) echo "Bonjour à vous deux, $NOMS"

9) unset efface les variables de la mémoire au lieu de les garder vide.

10) echo "\$HOME = $HOME"

## Exercice 2. Contrôle de mot de passe

export PATH=$PATH:~/script

### script :
```
#!/bin/bash
PASSWORD=vmbb
echo "mdp ?"
read -s mdp
if [ "$mdp" == "$PASSWORD" ]; then
        echo "mdp correct"
else
        echo "mdp incorrect"
fi
```

## Exercice 3. Expressions rationnelles

```
#!/bin/bash
function is_number(){
        echo $1
        re='^[+-]?[0-9]+([.][0-9]+)?$'
        if ! [[ $1 =~ $re ]] ; then
                return 1
        else
                return 0
        fi
}

is_number $1

if [ $? -eq 1 ]; then
       echo "erreur $1 n est pas un reel"
fi
```

## Exercice 4. Contrôle d’utilisateur

```
#!/bin/bash
if [ "$#" -ne 1 ]; then
        echo "Utilisation : $0 nom_utilisateur"
        exit
fi
#res= $(cut -d: -f1 /etc/passwd)
res=$(eval cut -d: -f1 /etc/passwd)

#echo "$res"

resEcho=$(echo "$res" | grep $1)
#echo $resEcho

if [ "$resEcho" == "$1" ]; then
        echo "present"
else
        echo "pas la"
fi
```

## Exercice 5. Factorielle

```
#!/bin/bash
  
res=1
for i in `seq 1 $1`;
do
        res=$(($res*$i))
done
echo $res
```

## Exercice 6. Le juste prix

```
#!/bin/bash
  
ECHELLE=1000

nombre=$RANDOM

let "nombre %= $ECHELLE"

var=$((1001))
echo "Veuillez choisir un nombre s'il vous plait ! "
while read var 
do
        if [ $var -gt $nombre ]; then
                echo "C'est moins"
        elif [ $var -lt $nombre ]; then
                echo "C'est plus"
        else
                echo "Gagné !"
                exit
        fi
        echo "Veuillez choisir un nombre s'il vous plait ! "
done

```

## Exercice 7. Statistiques

2)
```
#!/bin/bash
min=$1
max=$1
avr=0
for arg
do
	if ! [[ "$arg" =~ ^[+-]?[0-9]?[0-9]+$|[+-]?100+$ ]]
    then
        echo "$arg n'est pas un nombre entre -100 et 100"
        exit
	fi
	
	avr=$(($avr+$arg))
	
	if [ $min -gt $arg ]
	then
		min=$arg
	fi
	
	if [ $arg -gt $max ]
	then
		max=$arg
	fi
done
	avr=$((avr/$#))
	echo "moyenne= $avr"
	echo "min= $min"
	echo "max= $max"
```
3)
```
#!/bin/bash
min=0
max=0
avr=0
nbNombre=0
echo "Saisissez un nombre :"
while read var 
do
	if ! [[ "$var" =~ ^[+-]?[0-9]?[0-9]+$|[+-]?100+$ ]]
    then
        echo "$var n'est pas un nombre entre -100 et 100"
        exit
	fi
	
	avr=$(($avr+$var))
	
	if [ $min -gt $var ]
	then
		min=$var
	fi
	
	if [ $var -gt $max ]
	then
		max=$var
	fi
	nbNombre=$(($nbNombre+1))
	
	echo "Encore un autre nombre (y/n)?"
	read encore
	if [ $encore == 'n' ] 
	then
		avr=$((avr/$nbNombre))
		echo "moyenne= $avr"
		echo "min= $min"
		echo "max= $max"
		exit
	fi
	echo "Saisissez un nombre :"
done
```
