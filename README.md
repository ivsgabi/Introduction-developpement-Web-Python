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

- Dans le fichier urls.py créer dans le  todolist
```
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='accueil')
]
"""Cette partie associe la page d'accueil à la fonction index dans les vues."""
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

3. Utiliser sa première template

- Dans ce ripo se trouve un dossier templates avec deux templates en html généré sur bootstrap, copiez les dans le dossier templates précedemment créé dans le dossier todolist.
- Les dossiers css et js aussi présents sur le ripo doivent être copié dans votre dossier static précédemment créé.
- Les templates .html sont les pages qui apparaitront dans votre application.

Maintenant, il faut les lier aux pages approprié.

- Pour ça, dans la fonction index dans la fichiers views.py, au lieu de return une réponse http pour afficher "Hello World!", vous pouvez utiliser la fonction render() avec le fichier index.html.
- Si tout c'est bien passé, la page d'accueil de votre application Web est mise en place.

4. Créer le modèle de tâche

- Pour pouvoir créer une base de données à une seule entrée (la ToDoList), on défini un modèle de tâche dans le fichier models.py en créant une classe Task.

```
class Task(models.Model):
    tache = models.CharField(max_length=500)

    def __str__(self):
        return self.tache
```

Ici on créer une classe Task qui créera des objet tache qui auront un champs d'entrée de 500 caractères maximum.
Si ce n'est pas encore le cas, vous pouvez fermez le début de l'application Web.

5. Gérer la base de données

- Pour gérer la base de donnée avec django, dans le terminal:

```
python manage.py makemigrations
python manage.py migrate
python manage.py shell """ouvre un shell python, les prochaines lignes sont à mettre dedans"""
from todolist.models import Task
Task.objects.all() """pour voir toutes les tâches qui se trouvent dans la base de données, normalement c'est vide"""
Task.objects.create(tache='task1') """ajoute une task1 à la base de données"""
Task.objects.delete(tache='task1') """supprimer une task1 de la base de données"""
```

La base de données est crée. 

vous pouvez la voir en relançant l'application avec la commande suivante, et lorsque vous la lancez sur Firefox, vous ajouter /admin juste après l'adresse. 

```
python manage.py runserver
```

- Dans le fichier admin.py, ajoutez
```
from .models import Task

admin.site.register(Task) """ ça va créer la rubrique task sur l'interface admin, vous pouvez le voir en temps réel"
```

Et dans la section Task, vous verez les task créer précédemment dans le shell si vous en avez mises en place.

6. Rendre la base de données "accessible"

- Dans le dossier todolist, créez un fichier forms.py dans lequel vous devez mettre ceci:

```
from django.db.models import fields
from .models import Task

class FormTask(forms.ModelForm):
    Tache = forms.CharField(max_length=500, widget=forms.TextInput(attrs={
        'placeholder': 'Add your Task',
        'class': 'form-control form-control-lg',
    }))

    class Meta:
        model = Task
        fields = ['Tache']
```
Cette partie crée un formulaire basé sur le modèle Task, avec un champ de texte pour Tache.

- Dans le fichier views.py, pour pouvoir utiliser ectte forme de formulaire dans ce fichier, ajoutez:

```
from .forms import FormTask
```

Vous pouvez jeter un coup d'oeil à l'application pour vérifier que tout va bien.

- Toujours dans le fichier views.py, le but est maintenant d'afficher un formulaire de la forme définie dans le fichier forms.py qui prendra donc en paramètre la requête de l'utilisateur.
Si le formulaire est valide, on enregistre dans la base de données. Attention, il ne faut pas oublier de set un contexte pour les variables qu'on veut mettre en place dans la fonction index.

- Pour vérifier si ça fonctionne, rendez-vous sur votre application Web, ajoutez une tâche et regardez si elle est ajouté dans la liste des taches du coté admin.

7. Lister les tâches, les supprimer et les modifier

- Pour que la liste de tache soit aussi visible sans le statut admin, on va afficher la base de données en faisant:
```
list = Task.objects.all() """ + context"""
```

- Pour modifier une tâche de la to do list, dans fichier views.py, déclarez une fonction update qui prend en paramètre une request (comme la fonction index) et un paramètre my_id. Cette fonction va gérer le bouton modifier. La fonction ressembla assez à la fonction index.
Conseil: utiliser get_object_or_404()
Elle devrait ressembler à ça sans les includes nécéssaires:

```
def update(request, my_id):
    obj = Task.objects.get(id=my_id) """pour recupérer l'id de la tâche qu'on veut modifier"""
    form = FormTask(request.POST or None, instance=obj)
    if form.is_valid():
        form.save()
        return redirect('/') """pour rediriger vers une autre page"""
    return render(request, 'update.html', {'form': form })

```

- Du coup, il faut ajouter cette nouvelle page à la liste d'urls de urlpatterns dans urls.py.

```
path('/update', views.update, name='update') """vous aurez peut-être quelque chose à ajouter"""

```

- Encore une fois vous pouvez vérifier du coté de l'application si tout est ok.

- Pour supprimer une tâche, le principe est très proche de celui pour modifier, on vous laisse faire, bon courage et #bravo si vous êtes arrivé jusque là!

8. L'application est terminée.

Vous pouvez désormais enregistrer vos tâches à faire, les modifier et les supprimer via votre ToDoList virtuelle.




