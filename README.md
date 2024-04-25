# Introduction-developpement-Web-Python

Bienvenue au Workshop dd'introduction au développment Web en Python.

D'abord, assurez-voous d'avoir Python d'installer sur votre ordinateur.
Pour vérfier vous pouvez utiliser la ligne ci-dessus.
```
python --version
```
ou
```
python3 --version
```

Si ce n'est pas le cas, vous pous l'installer avec la ligne suivante:
```
sudo dnf install python3 python3-pip
```

Il faut aussi intaller Django pour ce workshop.
Django est un framework de développement Web open-source écrit en Python https://docs.djangoproject.com/fr/ .
```
pip3 install django
```
Normalement, django devrait maintenant être installé sur votre système, vous pouvez vérifier avec la ligne suivante.
```
django-admin --version
```

Création d'une application de gestion de tâches avec Django
Objectif : Créer une application Web de liste de tâches où les utilisateurs peuvent ajouter, supprimer et marquer les tâches comme complétées.

1. Création d'un projet Django
```
django-admin startproject nom_de_votre_projet
```
Pour créer un nouveau projet Django.

2. Création d'une application Django
```
python manage.py startapp tasks
```
Pour créer une nouvelle application Django nommée "tasks".

3. Définition d'un modèle de tâche dans un fichier models.py (suggestion)
C'est quoi le modèle de tâche ?
Le modèle de tâche est une représentation de la structure des données d'une tâche dans la base de données.
https://docs.djangoproject.com/fr/3.2/topics/db/models/

4. Création de "vues" dans un fichier urls.py (suggestion)
Afficher la liste des tâches, ajouter une nouvelle tâche, marquer une tâche comme complétée et supprimer une tâche.
https://docs.djangoproject.com/fr/3.2/topics/http/views/

5. Définition d'URL pour chaques vues dans un fichier urls.py (suggestion)
Diriger/associer les requêtes vers les vues appropriées.
https://docs.djangoproject.com/fr/3.2/topics/http/urls/
   
6. Création de Templates :
Créez des templates HTML pour afficher les différentes pages de l'application.
Plusieurs possibilitées, 


   
