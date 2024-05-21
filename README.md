# Introduction-developpement-Web-Python

Bienvenue au Workshop d'introduction au développment Web en Python.
N'hésitez pas à consulter les liens à chaque étapes, il s'agit de documentation pour vous aider à réaliser les tâches.

D'abord, assurez-vous d'avoir Python d'installer sur votre ordinateur.
Pour vérfier vous pouvez utiliser la ligne ci-dessus.
```
python --version
```
ou
```
python3 --version
```

Si ce n'est pas le cas, vous pouvez l'installer avec la ligne suivante:
```
sudo dnf install python3 python3-pip
```

Il faut aussi intaller Django pour ce workshop.
Django est un framework de développement Web open-source écrit en Python https://docs.djangoproject.com/fr/ .
https://docs.djangoproject.com/en/5.0/
https://realpython.com/tutorials/django/

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
Il faut ensuite se troouver dans le dossier créé pour exécuter la ligne suivante.

2. Création d'une application Django
```
python manage.py startapp tasks
```
Pour créer une nouvelle application Django nommée "tasks".

3. Définition d'un modèle de tâche dans le fichier models.py

C'est quoi le modèle de tâche ?
Le modèle de tâche est une représentation de la structure des données d'une tâche dans la base de données.
https://docs.djangoproject.com/fr/3.2/topics/db/models/

4. Création de "vues" dans le fichier urls.py

Afficher la liste des tâches, ajouter une nouvelle tâche, marquer une tâche comme complétée et supprimer une tâche.
https://docs.djangoproject.com/fr/3.2/topics/http/views/

5. Définition d'URL pour chaques vues dans le fichier urls.py

Diriger/associer les requêtes vers les vues appropriées.
https://docs.djangoproject.com/fr/3.2/topics/http/urls/
   
6. Création de Templates dans un dossier templates (suggestion)

Créer des templates HTML pour afficher les différentes pages de l'application.
Suggestion: un fichier html par vues.
Plusieurs possibilitées: 
- Utiliser des templates existantes spécialement conçus pour ce type d'application
Vous pouvez en retrouver ici:
https://adminlte.io/
ou sur la plateforme Bootstrap avec SB Admin2
ou même sur GitHub
Sinon, vous pouvez créez le votre soit écrire votre propre fichier html.
Exemple:
```
templates/
├── task_list.html
├── task_detail.html
├── task_form.html
```
task_list.html = template pour afficher la liste des tâches.
task_detail.html = template pour afficher les détails d'une tâche individuelle.
task_form.html = template pour afficher le formulaire d'ajout/modification/terminé de tâche.

https://docs.djangoproject.com/fr/3.2/topics/templates/
https://tutorial.djangogirls.org/en/template_extending/

7. Intégration des templates avec les vues

Intégration des données des vues aux templates.
Dans vos vues Django, vous pouvez utiliser la fonction render pour renvoyer les templates HTML en réponse aux requêtes des utilisateurs. 
Assurez-vous d'importer la fonction render depuis django.shortcuts.

https://docs.djangoproject.com/fr/3.2/topics/templates/
https://docs.djangoproject.com/fr/3.2/topics/http/shortcuts/#render

8. C'est terminé
Vous pouvez exécuter votre application en utilisant la commande
```
python manage.py runserver
```
Accéder à celle-ci via votre navigateur Web.







   
