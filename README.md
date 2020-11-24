# Django-Project
{% extends "faculty/base.html" %}
{% block content %}

<div class= "container">
   <div class= "jumbotron text-center">
      <h1>Django Project</h1>
      <p>BUS 443: {{ firstname }} {{ lastname }}</p>
   </div>
</div>

{% endblock %}
{% extends "faculty/base.html" %}
{% block content %}

<div class="container" style="margin-top:50px">
     <form method="post" action="{% url 'login' %}">
          {% csrf_token %}
         <table class="table">
             {{ form }}
         </table>
         <input type="submit" value="Login">
     </form>
</div>

{% endblock %}{% extends "faculty/base.html" %}
{% block content %}

<div class="container">
   <div class="jumbotron text-center">
      <h1>Django Project</h1> 
   </div>
</div>

<div class="container">
     <table class ="table">
        <thead>
            <tr>
               <th>Student ID</th>
               <th>First Name</th>
               <th>Last Name</th>
               <th>Major</th>
               <th>Year</th>
               <th>GPA</th>
            </tr>
        </thead>
        <tbody>
            {% for row in data %}
            <tr>
                <td>{{ row.studentid }}</td>
                <td>{{ row.firstname }}</td>
                <td>{{ row.lastname }}</td>
                <td>{{ row.major }}</td>
                <td>{{ row.year }}</td>
                <td{{ row.gpa }}</td>
            </tr>
            {% endfor %} 
        </tbody>
     </table>

     <div class="pagination">
         <span class="step-links">
             {% if data.has_previous %}
                 <a href="?page={{ data.previous_page_number }}">Previous</a>
             {% endif %}
             <span class="current">
                 Page {{ data.number }} of {{ data.paginator.num_pages }}
             </span>
             {% if data.has_next %}
                 <a href="?page={{ data.next_page_number }}">Next</a> 
             {% endif %}
         </span> 
</div>

{% endblock %}

{% extends "faculty/base.html" %}
{% block content %}

<div class="container">
   <div class="jumbotron text-center">
      <h1>Django Project</h1> 
   </div>
</div>

<div class="container">
     <table class ="table">
        <thead>
            <tr>
               <th>Course ID</th>
               <th>Course Title</th>
               <th>Course Section Code</th>
               <th>Course Department</th>
               <th>Instructor Full Name</th>
            </tr>
        </thead>
        <tbody>
            {% for row in data %}
            <tr>
                <td>{{ row.courseid }}</td>
                <td>{{ row.coursetitle }}</td>
                <td>{{ row.coursesectioncode }}</td>
                <td>{{ row.couredepartment }}</td>
                <td>{{ row.instructorfullname }}</td>
            </tr>
            {% endfor %} 
        </tbody>
     </table>

     <div class="pagination">
         <span class="step-links">
             {% if data.has_previous %}
                 <a href="?page={{ data.previous_page_number }}">Previous</a>
             {% endif %}
             <span class="current">
                 Page {{ data.number }} of {{ data.paginator.num_pages }}
             </span>
             {% if data.has_next %}
                 <a href="?page={{ data.next_page_number }}">Next</a> 
             {% endif %}
         </span> 
</div>
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
   <title>Navbar Example - BUS 443 </title>
   <meta charset="utf-8">
   <meta name="viewport" content="width=device-width, initial-scale=1">
   <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
   <link rel="stylesheet" type="text/css" href="{% static 'faculty/css/style.css' %}">
   <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
   <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
   <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</head>
<body>   

    <header>
      <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
        <a class="navbar-brand" href="#">Ramiro's App</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarCollapse" aria-controls="navbarCollapse" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarCollapse">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a class="nav-link" href="{% url 'home'  %}">Home <span class="sr-only">(current)</span></a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="{% url 'studentdetails' %}">Student Details</a>
            </li>
            <li class="nav-link">
              <a class="nav-link" href="{% url 'coursedetails' %}">Course Details</a>
            </li>
            <li class="nav-link">
              <a class="nav-link" href="{% url 'enrollment' %}">Enrollment</a>
            </li> 
          </ul>
          <ul class="navbar-nav">
              {% if not user.is_authenticated %}
                 <ul class="navbar-nav px-3">
                     <li class="nav-item text-nowrap">
                         <a class="btn btn-light btn-sm" role="button" href="{% url 'login' %}">Log in</a>
                     </li>
                 </ul>
              {% else %}
                  <ul class="navbar-nav">
                      <li class="nav-item text-nowrap">
                          <a class="nav-link" href="{% url 'logout' %}">Log out</a>
                      </li>
                  </ul>
              {% endif %}
          
           
          </ul>
        </div>
      </nav>
    </header>
     
     {% block container %}
           <div>
               {% block content %}
               {% endblock %}
           </div>
     {% endblock %}
</body>
</html>
{% endblock %}
"""university URL Configuration

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
from faculty import views
from django.contrib.auth.views import LoginView, LogoutView

urlpatterns = [
    path('admin/', admin.site.urls),
    path('home/' , views.home, name='home'),
    path('login/',LoginView.as_view(template_name="faculty/login.html") ,name='login'),
    path('logout/',LogoutView.as_view(), name='logout'),
    path('studentdetails/', views.studentdetails, name='studentdetails'),
    path('coursedetails/', views.coursedetails, name='coursedetails'),
    path('enrollment/', views.enrollment, name='enrollment')
    
]
from django.shortcuts import render
from django.http import HttpResponse
from faculty.models import Coursedetails
from faculty.models import Studentdetails
from django.db import connection
from django.core.paginator import Paginator
from django.contrib.auth.decorators import login_required

# Create your views here.

@login_required
def home(request):
    context = {'CourseName':'Faculty Seminar Topics in Entr', 'Course Section Code':'1'}
    return render(request, 'faculty/home.html',context)

def dictfetchall(cursor):
    #"Return all rows from a cursor as a dict"
    columns = [col[0] for col in cursor.description]
    return [
        dict(zip(columns, row))
        for row in cursor.fetchall()
    ]

@login_required
def coursedetails(request):
    #cursor = connection.cursor()
    #cursor.execute('SELECT * FROM FACULTY.COURSEDETAILS')
    #faculty = dictfetchall(cursor)
    faculty = Coursedetails.objects.all()
    paginator = Paginator(faculty, 10)
    page = request.GET.get('page')
    facultydata = paginator.get_page(page)
    
    return render(request, 'faculty/coursedetails.html', {'data':facultydata})
    
@login_required
def studentdetails(request):
    #cursor = connection.cursor()
    #cursor.execute('SELECT * FROM FACULTY.STUDENTDETAILS')
    #faculty = dictfetchall(cursor)
    faculty = Studentdetails.objects.all()
    paginator = Paginator(faculty, 10)
    page = request.GET.get('page')
    facultydata = paginator.get_page(page)

    return render(request, 'faculty/studentdetails.html',{'data':facultydata})

def enrollment(request):
    faculty = Studentdetails.objects.all()
    enrollmentdata = ''
    if('firstname' in request.session):
        enrollmentdata = Enrollment.objects.filter(firstname = request.session['firstname'])
    if('fname' in request.GET and 'aname' not in request.GET):
        fname = request.GET.get('fname')
        request.session['firstname'] = fname
        return HttpResponse('Success')
    if('fname' in request.GET and 'aname' in request.GET):
        fname = request.GET.get('fname')
        aname = request.GET.get('aname')
        enrollmentdata = Enrollment.objects.filter(firstname = fname)
        for row in enrollmentdata:
            if row.enrollment == aname:
               return HttpResponse('Error')
        newdata = Enrollment(firstname = fname, award = aname)
        newdata.save()
        return HttpResponse("Success")
    return render(request, 'faculty/enrollment.html', {'faculty':faculty, 'Enrolled':enrollmentdata})
"""
Django settings for university project.

Generated by 'django-admin startproject' using Django 3.1.2.

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
SECRET_KEY = 'rqel%kso@$jjki5nkf38f=ysm83ouh^z@w&ks-2+(if#6qz*m9'

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
    'faculty',
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

ROOT_URLCONF = 'university.urls'

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

WSGI_APPLICATION = 'university.wsgi.application'


# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'faculty',
        'USER': 'facultyuser',
        'PASSWORD': 'Amanda@2323',
        'HOST': 'localhost',
        'PORT': '3306'
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

LOGIN_REDIRECT_URL = 'home'

LOGIN_URL = 'login'

LOGOUT_REDIRECT_URL = 'login'
from django.db import models

class Studentdetails(models.Model):
     studentid = models.IntegerField(primary_key=True)
     firstname = models.CharField(max_length=500)
     lastname = models.CharField(max_length=500)
     major = models.CharField(max_length=500)
     year = models.CharField(max_length=500)
     gpa = models.DecimalField(max_digits=3, decimal_places=1)

class Coursedetails(models.Model):
     courseid = models.IntegerField(primary_key=True)
     coursetitle = models.CharField(max_length=500)
     coursename = models.CharField(max_length=500)
     courseselectioncode = models.IntegerField()
     coursedepartment = models.CharField(max_length=500, default='SOME STRING')
     instructorname = models.CharField(max_length=500, default='SOME STRING')

class Enrollment(models.Model):
     studentid= models.IntegerField()
     courseid = models.IntegerField()
     coursetitle = models.CharField(max_length=500, default='SOME STRING')
     coursename = models.CharField(max_length=500, default='SOME STRING')
     courselectioncode = models.IntegerField(default=0)
     coursedepartment = models.CharField(max_length=500, default='SOME STRING')
     instructorname = models.CharField(max_length=500, default='SOME STRING') 

# Create your models here.
from django.contrib import admin
from faculty.models import Coursedetails
from faculty.models import Studentdetails
 

admin.site.register(Coursedetails)
admin.site.register(Studentdetails)

# Register your models here.
