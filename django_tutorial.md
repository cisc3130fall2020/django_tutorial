# Django Tutorial
#### By: Mark MacEachen

### Overview

In this tutorial I quickly show you how to develop a simple website with Python using the Django Web Framework. The contents of this tutorial cover:
- [x] Introduction to the Python Package Index
- [x] Introduction to pip
- [x] Brief overview of Python virtualenv/venv
- [x] Brief overview of Django Web Framework
- [x] Introduction to developing with the model-view-template pattern

## What is Django?

- Django is a high-level Python web framework that takes care of much of the hassle of web development <sub>(1)</sub>.
- Django is essentially just one of almost 300,000 python modules that you can install from the **Python Package Index** <sub>(2)</sub>.
- Django is open source.
- A Django project is an abstraction on top of a Python project, so it's advisable to follow Python best practices from the start.
- Each time, before you start a new Django (Python) project, you need to create a new virtual environment (virtualenv or venv) to house your project.


### What is venv

- **venv** is a subset of **virtualenv**, a tool for creating isolated python environments <sub>(3)</sub>.
- At a very basic level, venv addresses the problem of **dependency management** for Python projects.
- venv does what the name suggests -- it creates an isolated virtual environment for your python project.
- **IF YOU DON'T USE A UNIQUE VENV/VIRTUALENV FOR EACH PROJECT YOU WILL RUN INTO PROBLEMS**.
- **Imagine a python project is a planet**. There are eight or nine planets in our Solar System; only one supports life. Now consider that each planet has an atmosphere. If a planet is a python project, then a planet's atmosphere would be a python package from the Python Package Index. Without venv, if you try to install an atmosphere to one planet, it will be universally accessable. **If you don't use venv** and you install venus's atmosphere, there will be conflict with the atmosphere on the other seven or eight planets. **You kill all the animals on Earth**. venv creates an isolated environment each project to prevent such problems.


### Installing Python packages

- Django, venv and every other Python module can be installed from the Python Package Index using **pip**, Python's package manager <sub>(4)</sub>.

<br>
This is all we need to get started so let's build a website.<br>
<sub>**Note**: If you are interested to start your own Django project, links to the webpages for all the tools mentioned in this tutorial are available in the works cited section of this document. You will need to follow the instructions available at the links provided to properly intall Python, venv or virtualenv, and pip in order to follow along.</sub><br>

### Getting Started

1. Create a new directory to house your project: ```$ mkdir lab07```
2. cd to your project directory: ```$ cd lab07```
3. Create a virtual environment for your project dependencies: ```$ python3 -m venv lab07-env```
4. After you create a virtual environment, you must activate/enter it. On mac/linux: ```$ source lab07-env/bin/activate```
    - Your command line should now look something like this: ```(lab07-env) name@name:/path/to/lab07$``` Notice how the virtual environment name now preposes the current path. If it's annoying to type ```source lab07-env/bin/activiate``` every time you need to enter the virtual environment, you can make a bash function to enter it for you. Mine is located in ```~/bin/.commands.sh```:
       ```bash
       function enter7() {
           source /path/to/lab07/lab07-env/bin/activate
           echo 'Activating lab07 virtual environment.'
       }
       ```
       Make sure the file is available in your path:
       ```
       echo "source /home/gohan/bin/.commands.sh" >> ~/.bashrc
       ```
       
    - After restarting your shell, you can activate/enter your virtual environment using your new command:
       ```
       $ enter7
       Activating lab07 virtual environment.
       (lab07-env) home@home:/path/to/lab07$
       ```
    - Note: it's always good to double check what version of software you're using. You can check what version of Python is used by your virtual environment like this:
       ```
       $ python --verson
       Python 3.6.9
       ```
5. Now that we're in the virtual environment, download the Django package. Use pip for this: ```python -m pip install django```
6. You want to track your packages. Use the following commands each time your install a new package to track your dependecies:
    ```
    $ pip freeze requirements.txt
    asgiref==3.3.1
    Django==3.1.4
    pkg-resources==0.0.0
    pytz==2020.4
    sqlparse==0.4.1
    ```
    You can see that Django version 3.1.4 was successfully installed to your virtual environemnt. Any time you need to check your environment, type ```cat requirements.txt``` into the command line from the path where ```requirements.txt``` exists in your file system.
    
7. Now that all of the requirements are install to start building a website, start a new Django project (make sure your in the directory where you want to house your project). Type: ```$ django-admin startproject lab07website``` into the command line to start a new Django project called lab07website.
8. All the heavy lifting has been done by Django. You can type ```$ cd lab07website``` to enter your project and start working.

### Django project skeleton

The command ```$ django-admin startproject lab07website``` created an entire project skeleton for us to use. If you want to take a technical look at everything that's there, you can read through the Django documentation online. It's inadvisable to tweak with any of the files this command created. I'll only going to focus on the files and directories that you would likely interact with when building a website.

One of the files worth mentioning now is manage.py, in the project root directory. manage.py is a python script that needs to be called quite regularly during the development process. Two such uses that we will go over are (i) for creating applications for a website, and (ii) for updating database.

Another file worth mentioning is the configuration file settings.py located in the the the project subdirectory /lab07/lab07website/lab07website/settings.py. settings.py defines variables that we will need to edit in the development process. The first variable we will need to look at is INSTALLED_APPS. INSTALLED APPS is a list that contained a reference to variable applications that the project needs to work. When we build a Django website we are essentially building new applications that will need to be added to this list.

```python
# /lab07/lab07website/lab07website/settings.py
"""
Django settings for lab07website project.

Generated by 'django-admin startproject' using Django 3.1.4.

For more information on this file, see
https://docs.djangoproject.com/en/3.1/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/3.1/ref/settings/
"""

from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent


# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/3.1/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = '5jq5u31zlfrfyp#2e3w23(ck6x3n=j$@8chr-q8p_&lc8w%$xd'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'lab07website.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'lab07website.wsgi.application'


# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}


# Password validation
# https://docs.djangoproject.com/en/3.1/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]


# Internationalization
# https://docs.djangoproject.com/en/3.1/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_L10N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.1/howto/static-files/

STATIC_URL = '/static/'
```



Now that you have a project skeleton, you need to fill it up with applications containing logic specific to your website needs. This tutorial follows along as I build a website for Lab 07. As far as functionality goes, it has the bare minimum: One application using the default database provided by Django. A real Django project will house multiple applications that interact with each other and a production ready database such as PostgreSQL which is all beyond the scope of this tutorial.


## Developing Django applications

- To start a new application, make sure manage.py is available in your path (ie make sure you are in the project root directory) and type ```$ python manage.py startapp labs``` into the command line. In this case labs is the application name. Django will create a skeleton for a web application just like ```$ django-admin startproject project-name``` created a project skeleton. You can cd into the new application directory and start working on it.
- The next thing we need to do is add our application to the INSTALLED_APPS list in settings.py.
    ```python
    # /lab07/lab07website/lab07website/settings.py
    
    INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'labs.app.LabsConfig',
    ]
    ```

- Django applications follow a model-view-template design pattern.
- Each application directory will contain a models.py file and views.py file where you will write a majority of your python code.
- Template files will house html code to render website data for display online.

### models.py

- Models are a specific class of object used by Django to format data for persistent storage.
- Models inherit all the required functionality to work with django, we just need to do is define models specific to our website needs. Just like a class field is defined in java as an int, double, String, etc... Django model use specific types of fields as you can see below. These fields are a high level abstraction on top of the primitive data types and contain the functionality needed by Django to work with databases.
- Because this is a website for an online coding portfolio, I will define a model for a CISC3130 lab. Each model will have a field for the lab number, a brief description of the lab, and the url of the repository where I uploaded my solution to GitHub:
   ```python
   from django.db import models

   # Create your models here.
   class Lab(models.Model):
       number = models.IntegerField(
           primary_key=True,
       )
       description = models.TextField(
           help_text = "Brief description of the lab."
       )
       lab_url = models.CharField(
           max_length=200,
           help_text = "The url of the repository where I uploaded my solution."
       )

       def __str__(self):
           """
           Specify the String represtation of each Lab object. This is equivalent
           to the java as_string() funtion.
           """
           return "Lab {}".format(self.number)

    ```
    
- The lab class is a blueprint for lab objects. I haven't hardcoded any specific values into the lab fields because these values will be assigned for each instance of the lab model once the website is up and running.
- Models define objects that will be stored in a database. Each time you define a new model, or make changes to an existing model, you need to let django know. This is handles by something called "migrations" which is beyond the scope of this tutorial. All you need to know is that each time you create or change a model definition, you need to let Django know. We need to use the manage.py script for this, so make sure it's available in your path and run the script twice with the following args. If you skip this step, you will run into painful problems.
    ```
    $ python manage.py makemigrations
    Migrations for 'labs':
    labs/migrations/0001_initial.py
    - Create model lab
    $ python manage.py migrate
    Operations to perform:
    Apply all migrations: admin, auth, contenttypes, labs, sessions
    Running migrations:
    Applying labs.0001_initial... OK
    ```
- Notice the output provided by manage.py. It essentially tells us that manage.py has successfully created a database table for our lab model. manage.py provides detailed error messages to help track down errors in migrating so if you run into problems with this step, read the error message carefully, correct any issues and try again.


### views.py

- After defining models that will represent our website data, we need to specify exactly how the data is going to be displayed. This logic goes into views.py
- Django is used to create dynamic websites and Django views define logic that displays conent to dynamic webpages oon a dynamic website.
- A view can be either a function or a class, however **Django comes with predefined generic class based views** with pretty much everything needed to work for most types of webpages. This website will have two types of webpages using two different views:
    1. **LabListView inherits from the generic class based ListView**. The ListView class already contains fields and functions Django needs to display lists of data on a webpage. I just need to tell the ListView that it is going to display a list of lab instances, and override a few default fields.
    2. **LabDetailView inherits from the generic class based DetailView**. The DetailView class already contains fields and functions Django needs to display details about a specific instance of a class to a webpage. I just need to tell the DetailView that it is going to display details for an instance of a lab object and override a few default fields.
- Before we define these views, there are a couple things we need to consider.
   - Remembering that views are classes or functions Django uses to present data to a webpage, we need to consider the elements of a webpage. **Three things every webpage needs are the following**:
      1. **url**: the location of the webpage
      2. **HTML file**: the blueprint of the webpage
      3. **Data**: the contents of the webpage
   - Django views must contain all three elements, or references to them in order to work. Therefore, before we define our views, we need to do the following:
      1. **define the webpage url somewhere**
      2. **create the HTML blueprint for the webpage**
      3. **import model(s) from models.py into views.py**

### urls.py

- Django created a default urls.py file for us when we ran the command ```$ django-admin startproject lab07website```. We could define the url's for our webpages here but this causes a problem that we can't decouple our application from the Django project. One of the goals in developing Django applications is to following the **DRY** principle:
   - **DRY**: **D**on't **R**epeat **Y**ourself
- Right now we are building the Labs application specifically for use in the website for Lab07, however **we might want to reuse this application in another website**. If we don't completely decouple Labs from the Lab07website, then we will need to rebuild the Labs application fur use in the other website. So in order to follow DRY principles we need to completely decouple Labs from lab07website, which effectively makes Labs a **reusable application**.
- So instead of defining Lab's url's in the project url.py file, we will define a seperate url.py file inside the /labs directory, then import these urls into the project url.py file.
- The respective url configuration files look something like this:

   ```python
   # /lab07/lab07website/lab07website/urls.py

   """lab07website URL Configuration

   The `urlpatterns` list routes URLs to views. For more information please see:
       https://docs.djangoproject.com/en/3.1/topics/http/urls/
   Examples:
   Function views
       1. Add an import:  from my_app import views
       2. Add a URL to urlpatterns:  path('', views.home, name='home')
   Class-based views
       1. Add an import:  from other_app.views import Home
       2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
   Including another URLconf
       1. Import the include() function: from django.urls import include, path
       2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
   """
   from django.contrib import admin
   from django.urls import path
   from django.urls import include

   urlpatterns = [
       path('admin/', admin.site.urls),
       path('labs/', include('labs.urls')),
   ]
   ```
   - I use the django.urls.include function to include the urls defined in the labs url.py file in the project urlpatterns list. For details on how this works, see the Django documentation online.

### HTML Templates

I won't go into too much detail explaining this. In Django it is generally recommended that your HTML files are located in a nested subdirectory of each applicaiton. The reason for this is specified online in the Django documentaion. The HTML files for my two webpages look something like this:

#### /lab07/lab07website/labs/templates/labs/list.html
```html
<!DOCTYPE html>
{% load static %}
<html>
  <head>
  </head>
  <body>
    <h1>CISC3130 Labs</h1>
    <ul>
      {% for lab in lab_list %}
      <li><a href="{% url 'labs:lab_detail' lab.number %}">{{ lab }}</a></li>
      {% endfor %}
    </ul>
  </body>
</html>
```

#### /lab07/lab07website/labs/templates/labs/detail.html
```html
<!DOCTYPE html>
{% load static %}
<html>
  <head>
  </head>
  <body>
    <h1>{{ lab }}</h1>
    <p>Problem Description: <a href="{{ lab.description }}">notion.so</a></p>
    <p>Solution: <a href="{{ lab.lab_url }}">github.com</a></p>
  </body>
</html>
```

Recall the steps we needed to take to make views work. We've taken care of step i. and step ii. Now it's time to write the views.
   1. [x] define the webpage url somewhere
   2. [x] create the HTML blueprint for the webpage
   3. [ ] import model(s) from models.py into views.py

Let's take a look at the view I wrote for my two webpages in views.py

### views.py
```python
# /lab07/lab07website/labs/views.py

from django.shortcuts import render

#  Import the generic class based views
from django.views.generic.list import ListView
from django.views.generic.detail import DetailView

# Import Lab model (python classes defined in the cwd aren't
# automatically available like they are in java and must be imported
# explicitly or implicitly.
from .models import *

# Create your views here.
class LabsListView(ListView):
    template_name = 'labs/list.html'
    model = Lab

    def get_queryset(self, **kwargs):
        """
        We need to make sure the list of labs is rendered to the
        html file so they can be displayed on the webpage. This
        is called rendering context data. ListView handles this
        with the get_queryset function.

        Simply specify that the queryset contains a reference to
        each lab in the database.
        """
        return Lab.objects.all()

class LabsDetailView(DetailView):
    # Tell Django the data for this webpage is a lab
    model = Lab
    
    # The webpage blueprint for the lab
    template_name = 'labs/detail.html'
```
- We've complete our views:
   1. [x] define the webpage url somewhere
   2. [x] create the HTML blueprint for the webpage
   3. [x] import model(s) from models.py into views.py


### Where are we at now?

- At this point, we've written all the python code necessary so Django can do the following:
   1. Fill database tables with Lab data
   2. Render this Lab data in two types of webpages
      1. A webpage to display a list of Labs.
      2. A webpage to display data specific to each lab.
- Django can run a development server as local host so you can actually view the website on localhost at port 8000. Once again navigate to the directory housing manage.py, ensure that the virtual environment for lab07 is activated, and run the development server:
   ```
   $ cd ~/lab07/lab07website
   $ enter7
   Activating lab07 virtual environment
   $ python manage.py runserver
   Watching for file changes with StatReloader
   Performing system checks...

   System check identified no issues (0 silenced).
   December 06, 2020 - 20:37:29
   Django version 3.1.4, using settings 'lab07website.settings'
   Starting development server at http://127.0.0.1:8000/
   Quit the server with CONTROL-C.
   ```
As the output shows, our website is now running at http://127.0.0.1:8000/ aka http://localhost:8000/. We need to open our browser and navigate to the url location for a website we have defined on the website. In this case we'll go to http://127.0.0.1:8000/labs/.

#### http://127.0.0.1:8000/labs/
 ![one!](1.png)


As we can see, the website is up and running, but we stil haven't added any labs. There is nothing in the database tables to populate the website. There are many ways to do this that are out of the scope of this quick tutorial. I'm going to use the default Django admin panel in this case. Configuration is simple. Once you have the admin panel configured, you can find the admin panel at the /admin url and fill the table up with instances of lab objects. I've gone ahead and done that, after which we can see of like of links to the details page for each lab:

#### http://127.0.0.1:8000/labs/
 ![two!](2.png)


#### http://127.0.0.1:8000/labs/4/
 ![three!](3.png)

<br>

## Conclusion / Next Steps

This completes a very basic introductory tutorial on Django programming. In theory, with some slight configuration work you could upload this website to a webserver and make it available on the web, but it won't do very much.

At this point you should be familiar with the Django model-view-template development pattern. Next steps could include learning how to work with forms <sub>(5)</sub>, completing the official Django tutorial <sub>(6)</sub>, deploying your Django project <sub>(7)</sub> or completing an advanced tutorial where you learn how to properly package a reusable Python/Django app that can be uploaded to the Python Package Index (PyPI) <sub>(8)</sub>.

<br>

## References

1. Django. (n.d.). Retrieved December 04, 2020, from https://www.djangoproject.com/
2. Find, install and publish Python packages with the Python Package Index. (n.d.). Retrieved December 04, 2020, from https://pypi.org/
3. Virtualenv¶. (n.d.). Retrieved December 04, 2020, from https://virtualenv.pypa.io/en/latest/
4. Pip. (n.d.). Retrieved December 04, 2020, from https://pypi.org/project/pip/
5. Documentation. (n.d.). Retrieved December 06, 2020, from https://docs.djangoproject.com/en/3.1/topics/forms/
6. Documentation. (n.d.). Retrieved December 06, 2020, from https://docs.djangoproject.com/en/3.1/intro/tutorial01/
7. Documentation. (n.d.). Retrieved December 06, 2020, from https://docs.djangoproject.com/en/3.1/howto/deployment/
8. Documentation. (n.d.). Retrieved December 06, 2020, from https://docs.djangoproject.com/en/3.1/intro/reusable-apps/