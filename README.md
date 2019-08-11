# PyDjango-Demo

Description: 
Sample app to test out Python/Django fullstack capabilities 

* [Versions](#Current-Local-Set-Up)
* [Start-Up Doc](#Steps-For-Easy-Start-Up)
    1. [Download](1.download)
    2. [Create Scaffolding](2.scaffold)
        * [Project Explanation](#Whats-going-on-in-myproject)


## Current Local Set-Up
| Software | Version |
| -------- |:-------:| 
|Python    |3.7.64   |
|Pip       |19.2.1   |
|Django    |2.2.4    |

## Steps for Easy Start-Up
1. Download [Django](https://www.djangoproject.com/download/)
    > `pip install Django==2.2.4`
   
2. Create the project scaffold 
    > `django-admin startproject <myproject>` 

 __What's going on in myproject:__ 

manage.py – It is a command-line utility that lets you interact with this Django project in various ways. 

'myproject/' – It is the actual Python package for your project. It is used to import anything, say –  myproject.urls. 

init.py – Init just tells the python that this is to be treated like a python package.

settings.py – This file manages all the settings of your project. 

urls.py – This is the main controller which maps it to your website.

wsgi.py – It serves as an entry point for WSGI compatible web servers.

  ![Project Directory](assets\doc\ProjectDirectory-Django.png)

3. Create your app. Navigate to the myproject directory and type the following:  
    > `python manage.py startapp webapp`

4. Open the myproject/settings.py, and add the following:
     ```
    INSTALLED_APPS = (
    'webapp',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    )
    ```

5. Create a view! Open webapp/views.py and add the following:
    ```
    from django.shortcuts import render
    from django.http import HttpResponse
    
    def index(request):
        return  HttpResponse("<H2>HEY! Welcome to Myproject! </H2>")
    ```
6. Map the view to a URL. Create a new file ("urls.py") inside the webapp. In webapps/urls.py, input the following code:
    ```
    from django.conf.urls import url
    from . import views
    urlpatterns = [
     url(r'^$', views.index, name='index'),
    ]
    ```
    *Note: The url pattern is in regular expression format where ^ stands for beginning of the string and $ stands for the end.*

7. Point the root URLconfig at the webapp.urls module. Input this into myproject/urls.py:
    ```
    from django.conf.urls import include, url
    from django.contrib import admin
 
    urlpatterns = [
        url(r'^admin/', include(admin.site.urls)),
        url(r'^webapp/', include('webapp.urls')),
    ]
    ```
    We have now added the webapp and included the webapp.urls. Now don’t forget to import django.conf.urls.include and insert an include() in the urlpatterns list. The include() function allows referencing other URLconfs. 

    Note that the regular expression doesn’t have a ‘$’ but rather a trailing slash, this means whenever Django encounters include(), it chops off whatever part of the URL matched up to that point and sends the remaining string to include URLconf for further processing.

8. Start the server, and go to go to http://localhost:8000/webapp/
    > `python manage.py runserver`


Special thanks to the www.edureka.com who this start-up guide came from. See it here at [Django Tutorial ](https://www.edureka.co/blog/django-tutorial/)