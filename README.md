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

1. Démarrage django
```
django-admin startproject Todo
```
Cette commande va créer un dossier. Après avoir fait un cd Todo, on peut utiliser la ligner suivant pour créer un nouveau projet Django du nom de Todo.

```
django-admin startapp todolist
```

2. Installation des prerequites de l'application

- Dans le dossier todolist, créez un dossier nommé "templates".
- Remplacez le fichier settings.py existant créer par Django par le fichier du même nom dans ce ripo.
- Dans le dossier todolist, créer un dossier nommé "static". Ce dossier contiendra les fichiers .css nécéssaires (javascript).
- Dans le dossier todolist créez un fichier urls.py même s'il y en a déjà un généré par Django dans le dossier Todo (on va l'inclure dedans).
- Copier le fichier views.py du ripo dans celui de votre dossier. N'oubliez pas d'ajouter les includes nécéssaires.
- Dans votre terminal:
```
python manage.py migrate
python manage.py createsuperuser
```
Attention, il faudra se souvenir des informations que vous donnez plus tard.

```
python manage.py runserver
```
Si tout c'est bien passé, vous devriez avoir un lien à ouvrir sur Firefox spécifiquement et un message de félicitations pour une installation réussie.

3. Démarrage de l'application

- Dans le fichier urls.py créer dans le dossier todolist
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='accueil')
]
```
Cette partie associe la page d'accueil à la fonction index dans les vues.
- Dans le fichier urls.py du dossier Todo (celui généré par Django), ajouter "include" à la fin de la ligne 17, elle devrait ressembler à ça maintenant:

```
from django.urls import path, include
```

Juste en dessous se trouve la liste des urls pattern, il y en a un relier à la partie admin, il faut en ajouter un pour le reste. Vous pouvez ajouter la ligne suivante à la liste urlpattern pour ça.

```
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include(todolist.urls)),
]
```

Si vous recharger le serveur sur votre navigateur, vous devirez voir le message "Hello World!" s'afficher.
Vous venez de définir votre première view.

