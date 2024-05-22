# Introduction au développement web avec Python

## Objectifs

✔️ Créer une To-Do app avec Python et Django

✔️ Découvrir le framework Django

## Introduction

Bienvenue à ce workshop d'introduction au développment web en Python. 🚀

Dans ce workshop, vous allez créer une simple application To-Do à l'aide du [langage Python](https://www.python.org/) et du [framework Django](https://www.djangoproject.com/).

Django est un framework Python, une boite à outils qui facilite le développement d'applications web. ⚙️

L'objectif, à la fin de ce workshop, est d'avoir une application sur laquelle on peut voir nos tâches, ajouter, modifier et supprimer une tâche. ✨

Au cours de ce workshop, n'hésitez pas à consulter la [documentation officielle de Django](https://docs.djangoproject.com/fr/) ! 👍

## Etape 0 - Setup

### Installation

Tout d'abord, assurez-vous d'avoir Python d'installer sur votre ordinateur.

```
python --version
```
ou
```
python3 --version
```

Si Python est bien installé, vous devriez voir la version de Python que vous avez actuellement.

```
python --version
Python 3.XX.X
```

Si ce n'est pas le cas, vous pouvez l'installer avec la commande suivante:

```
sudo dnf install python3 python3-pip
```

Il faudra aussi installer Django pour ce workshop.

```
pip install django
```
ou
```
pip3 install django
```

Pour vérifier que Django s'est bien installé sur votre ordinateur, lancez la commande suivante:

```
django-admin --version
```

Vous devriez voir la version actuelle que vous avez de Django.

### Démarrer Django

Créeons notre projet Django, qui s'appellera Todo, en exécutant la commande suivante:

```
django-admin startproject Todo
```

Rendez-vous dans le dossier ```Todo``` qui a été généré, puis créeons notre application Django ```todolist```.

```
cd Todo && django-admin startapp todolist
```

### Setup l'application Django

Copiez-collez le dossier ```templates``` de ce dépôt dans le dossier ```todolist```.

Un [_template_](https://docs.djangoproject.com/fr/5.0/topics/templates/) (gabarit en français) est un fichier texte qui nous permet de générer dynamiquement des pages HTML, pour une application Django. C'est dans le dossier ```templates``` que nous allons stocker nos _templates_.

Ensuite, remplacez le fichier ```Todo/settings.py``` par le fichier du même nom dans ce dépôt.

Copiez-collez également le dossier ```static``` de ce dépôt dans le dossier ```todolist```. Ce dossier contient les fichiers CSS et JavaScript nécessaires pour l'application.

Créez aussi le fichier ```todolist/urls.py```.

Enfin, exécutez la commande suivante, afin de créer un compte superuser. Nous en aurons besoin plus tard, donc notez le nom d'utilisateur et le mot de passe que vous allez donner.

```
python manage.py createsuperuser
```

Enfin, lancez votre application avec la commande suivante.

```
python manage.py runserver
```

Vous devriez voir apparaître un lien, qui vous redirige vers votre application. 👍

### Etape 1 - Créer sa première vue 👓

Une [vue](https://docs.djangoproject.com/fr/5.0/topics/http/views/), en Django, est une fonction qui accepte une requête web et renvoie une réponse web.

Dans le fichier ```todolist/views.py```, crée une fonction ```index``` retournant une page HTML contenant le texte ```Hello world```.

> Jettez un coup d'oeil à la classe [HttpResponse](https://docs.djangoproject.com/fr/5.0/ref/request-response/#httpresponse-objects) 👍


Après avoir créé la vue, il faut rendre la vue de ```todolist/views.py``` accessible depuis notre application.

Pour ce faire, mettez à jour la liste ```urlspatterns``` du fichier ```todolist/urls.py```. Cette liste contient les mappages entre les chemins d'URL et les vues correspondantes. Django utilise cette liste pour déterminer quelle vue appeler pour une URL donnée.

Ici, on veut appeler associer à l'URL racine de notre application aux vues dans le fichier ```todolist/views.py```.

> Regardez ce qu'est un [_path_](https://docs.djangoproject.com/en/5.0/ref/urls/#path) et la fonction [include](https://docs.djangoproject.com/en/5.0/ref/urls/#include).

Profitez en aussi pour associer l'URL ```admin/``` à ```admin.site.urls```, qui correspond à la configuration intégrée de Django pour l'interface administrateur.
Cela nous permettra d'accéder à la partie administrateur en se rendant à l'URL ```admin/```.

Vous devriez maintenant avoir le message "Hello world" qui s'affiche sur votre application. Bien joué, vous avez créé votre première vue. 💯


### Etape 2 - Utiliser sa première template

Il est temps d'utiliser les templates définies dans le dossier ```todolist/templates```. On a la template ```index.html``` qui va correspondre à la page d'acceuil de notre application, et la template ```update.html`` qui va être la page permettant à l'utilisateur de mettre à jour une tâche.

> Vous remarquerez que ces fichiers ne contiennent pas seulement du code HTML, elles contiennent aussi un autre langage appelé le [langage de gabarit Django](https://docs.djangoproject.com/fr/5.0/topics/templates/#the-django-template-language) (_Django template language_). Prenez le temps de jeter un coup d'oeil aux _templates_ mises à disposition.

Commençons par utiliser la template ```index.html``` pour avoir la page d'acceuil de notre application. Pour ce faire, modifiez la fonction ```index``` de ```todolist/views.py```.

> Regardez comment s'utilise la fonction [render](https://docs.djangoproject.com/fr/4.2/topics/http/shortcuts/#render) ✨

Super, vous venez d'utiliser votre _template_!

### Etape 3 - Créer sa base de données 📑

Maintenant que nous avons notre page, il nous faut créer une base de données, qui contiendra nos tâches.

Vous pouvez stopper la commande `python manage.py runserver`.

Pour ce faire, définissons tout d'abord un [modèle de tâche](https://docs.djangoproject.com/fr/5.0/topics/db/models/) ```Task```.

Un modèle de tâche est une classe Python qui va nous permettre de définir la structure d'un objet dans une base de données.

Ici, ```Task``` est un objet qui représente une tâche. Pour une tâche, on aimerait:

- un id unique (```id```)
- un nom (```title```)
- une description (```description```)
- une date de création (```created_date```)
- une date de rendu (```due_date```) 
- et savoir si la tâche a été faite ou non (```done```).


Créez dans le fichier ```todolist/models.py``` la classe ```Task```.

> Regarder comment se définit un [modèle](https://docs.djangoproject.com/fr/5.0/topics/db/models/) et les [différents champs](https://docs.djangoproject.com/en/5.0/ref/models/fields/) qu'offre Django.


Après avoir défini notre modèle, dans le terminal, exécutez les commandes suivantes pour appliquer à notre base de données.

```
python manage.py makemigrations
python manage.py migrate
```

Pour tester que notre modèle fonctionne, créeons une tâche, directement depuis le shell de Python:

```
python manage.py shell
>> from todolist.models import Task
>> Task.objects.create(title='zappy', description='epitech')
>> Task.objects.all()
```

Vous pourrez voir que la tâche "Zappy" s'est bien créée.

Et voilà vous avez créé votre base de données. ✍️

Dans le fichier ```todolist/admin.py```, copiez-collez ce qui suit:

```
from .models import Task

admin.site.register(Task)
```

Vous pouvez ensuite vous rendre à l'URL ```/admin``` pour voir que le modèle ```Task``` s'est bien créé, après avoir lancé votre application. En cliquant sur la section ```Task```, vous pourrez voir que la tâche "Zappy" s'est bien créée.


### Etape 4 - Ajouter une nouvelle tâche depuis l'application 📁

Essayons maintenant de faire en sorte que l'on puisse ajouter une tâche depuis notre application. 👍

Pour y parvenir, nous devons tout d'abord créer un formulaire ```TaskForm```, qui permettra à l'utilisateur de renseigner une nouvelle tâche.

> Regardez comment définir un [formulaire](https://docs.djangoproject.com/en/5.0/topics/forms/modelforms/) en Django, à partir d'un modèle. Dans notre cas, on aimerait définir un formulaire à partir de notre modèle ```Task```.

Après avoir défini le formulaire, utilisez-le dans la vue ```index```.

> Dans le _template_ ```index.html```, vous avez dû remarquer qu'il y a des variables entourées par des accolades ```{{ }}```. Ces variables sont définies grâce au contexte donné en argument à la fonction [render](https://docs.djangoproject.com/fr/4.2/topics/http/shortcuts/#render). Un contexte est un [dictionnaire](https://courspython.com/dictionnaire.html) en Python. 

> Regardez comment s'utilise [un formulaire dans une vue](https://docs.djangoproject.com/en/5.0/topics/forms/#the-view).


Vous devriez avoir sur votre application un formulaire pour ajouter une nouvelle tâche. Si vous remplissez ce formulaire, vous devriez voir les tâches nouvellement ajoutées sur l'interface administrateur.

### Etape 5 - Listes les tâches

Essayez maintenant de faire la même chose pour pouvoir lister les tâches.

> Jettez un coup d'oeil à la fonction ```objects.all()``` :eyes:

### Etape 6 - Modifier ou supprimer une tâche

Pour finir, essayons de faire en sorte que l'on puisse modifier ou supprimer une tâche.

Pour ce faire, créez deux nouvelles vues ```update``` et ```delete``` dans ```todolist/views.py```.

> Regardez comment [mettre à jour un objet d'un modèle](https://openclassrooms.com/fr/courses/6967196-create-a-web-application-with-django/7349667-update-a-model-object-with-a-modelform).

Les fonctions ```update``` et ```delete``` devrait prendre, en plus de l'objet [HttpRequest](https://docs.djangoproject.com/en/5.0/ref/request-response/#django.http.HttpRequest) request, en argument l'id de la tâche à modifier.

> Regardez les différentes [requêtes](https://docs.djangoproject.com/en/5.0/topics/db/queries/) que vous pouvez effectuer sur un modèle.

Bravo, vous devriez avoir maintenant votre To-Do App, qui vous permet de gérer vos tâches!


## Auteur

| [<img src="https://avatars.githubusercontent.com/u/114922714?v=4" width=85><br><sub>Johana</sub>](https://github.com/sephorah) | 
|:------------------------------------------------------------------------------------------------------------:|