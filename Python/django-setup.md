> ****WIP***
# Django project setup

# 1. Installation

## 1.1 Platform setup
1. Check python installation `python3 -V`
2. Install PIP, virtualenv and virtualenvwrapper `sudo apt install python3-pip` confirm `pip3 -V`
3. Install VirtualEnv `pip3 install virtualenv`
4. Install DJango `pip3 install Django`

## 1.2 Setting up new project
1. Make folder and change dir: `mkdir proj1` && `cd proj1`
2. Set virtual env: `virtualenv env -p '/usr/bin/python3'` where -p option is for python version selection
3. Activate your environment `. env/bin/activate`
4. Install django `pip install django==2.2`
5. Start new project `django-admin startproject proj1`
6. Run server `cd proj1` & `python manage.py runserver`


# 2. Starting with new app-module and setting DB
## 2.1. New app module
1. Add new app `python manage.py startapp polls_app`
2. Include new app's urls file in parent urls file
    ```py
    ...
    from django.urls import path, include
    urlpatterns = [
        ...
        path('polls/', include('polls.urls')),
    ]
    ```
3. Define new view functions
    ```py
    from django.shortcuts import render
    from django.http import HttpResponse
    def index(request):
        return HttpResponse('helloworld')
    ```
4. Add new app specific URLS
    ```py
    from django.urls import path
    from . import views
    urlpatterns = [
        path('', views.index, name = 'index'),
    ]
    ```
5. Run server `python manage.py runserver` and open open URL `http://127.0.0.1:8000/polls/`

## 2.2. Setting database and running migrations

1. DB settings in settings.py, default is `sqlite`.
2. Running migration `python manage.py migrate`

## 2.3 Setting new app model and running migrations
1. Update polls.models.py
    ```py
    from django.db import models

    class Question(models.Model):
        question_text = models.CharField(max_length = 200)
        pub_date = models.DateTimeField('date published')

        def __str__(self):
            return self.question_text

    class Choise(models.Model):
        question = models.ForeignKey(Question, on_delete = models.CASCADE)
        choice = models.CharField(max_length = 200)
        votes = models.IntegerField(default = 0)

        def __str__(self):
            return self.question_text

    ```
2. Add new app to settings.py INSTALLED_APPS array,
    ```py
    # Application definition
    INSTALLED_APPS = [
        ...,
        'polls'
        ...
    ]
    ```
3. Create new migrations `python manage.py makemigrations polls` -> creates new migration files `polls/migrations/0001_initial.py`
4. Run new migrations `python manage.py migrate`

## 2.4. Using Django shell

1. Accessing django shell `python manage.py shell`
2. Import Polls models `from polls.models import Choices, Question`
3. Import Timezone model `from django.utils import timezone`
4. Show all data `Question.objects.all()`
4. Store data
    ```py
    q = Question (question_text = 'Whats new?', pub_date = timezone.now())
    q.save()
    q.id #-> give ID
    q.question_text # question_text

    #update\
    q.question_text = 'newquestion?'
    q.save()

    #Filter
    Question.objects.filter(id=1)
    Question.objects.filter(question_text__startswith='w')
    Question.objects.filter(pub_date__year = current_year) #Multiple result
    Question.objects.get(pub_date__year = current_year) #Single result

    q.choices_set.all() #All set choices
    q.choices_set.create(choice = 'Cooler') # Set val

    #Custom
    Question.objects.all()
    ```
# 3. Using builtin admin panel

1. Add new superuser `python manage.py createsuperuser`
2. Registering models to admin.
3. Edit `polls/admin.py`
    ```py
    from django.contrib import admin
    from .models import Choices, Question

    admin.site.register(Question)
    admin.site.register(Choices)
    ```



-----------------------RawInfo------------------------
1. Check python installation `python3 -V`
2. Install PIP, virtualenv and virtualenvwrapper `sudo apt install python3-pip` confirm `pip3 -V`
3. Install VirtualEnv `pip3 install virtualenv`
4. Install DJango `pip3 install Django`
5. `virtualenv -p python3 env` next, `source env/bin/activate`
6. Check version `django-admin --version`
7. Create project `django-admin startproject django_poll_project`
8. Start migrate `cd proj_dir` and `python manage.py migrate`
9. Start server `python manage.py runserver`
10. Add new app (Single purpose) `python manage.py startapp polls`

. python manage.py makemigrations
. python manage.py migrate

``` py
python manage.py shell 
    import django
    django.setup()
    from django.utils import timezone
    from polls.models import Question, Choice
    Question.objects.all()
    q = Question(question_text = 'Whats your name', pub_date = timezone.now())
    q.save()
    Question.objects.all()

    q.choice_set.create(choice_text = 'Sam', votes = 0)
    q.choice_set.create(choice_text = 'Ram', votes = 0)
    q.choice_set.create(choice_text = 'Pam', votes = 0)
    q.save()
```
 python manage.py createsuperuser