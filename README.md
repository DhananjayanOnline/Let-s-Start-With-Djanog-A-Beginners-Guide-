# Let's Start With Django, A Beginners Guide

Django follows MVT architecture,
MVT - Model View Template Concept

	1. Install django
	
		a. pip install django==2.2
		b. django-admin startproject <projectname> .
		c. python manage.py runserver
		d. python manage.py startapp <appname>
	
	2. Start new project
	
		 Step : 1	Step : 2	Step : 3            	Step : 4
		app/views.py --> app/urls.py --> project/url.py --> project/settings.py
		
		views.py :
			
			from django.shortcut import render
			from django.http import HttpResponse
			
			Def index(request):
				Return HttpResponse("Welcome to django")
				
			
		urls.py:
		
			from django.urls import path
			from .import views
			
			urlspatterns = [
				Path('',view.index)
			]
			
		project urls.py:
		
			from django.contrib import admin
			from django.urls import path,include
			
			urlpatterns=[
				path('admin/',admin.site.urls),
				path('',include('myapp.urls')),
			]
			
		settings.py : 
		
			INSTALLED_APPS = [
				---------------------,
				---------------------,
				---------------------,
				---------------------,
				' <appname> ',
			]
			
			
	3. Connecting With Database (MODEL)

		1. model.py --> views.py --> urls.py --> project/urls.py --> settings.py 
		
	
			model.py :
			
				from django.db import models
				
				class Student(models.Model):
				
					name = models.CharField(max_length=25)    \\
					course = models.CharField(max_length=25)   \\
		
		
			views.py :
				
				from django.shortcuts import render
				from .models import Student
				from django.views.generic import CreateView,ListView,DetailView,DeleteView,UpdateView

				 
				class StudentAdd(CreateView):              \\
					model = Student                         \\
					fields = ['name','course']              \\
					success_url = '/'                       \\
					                                      \\
				class StudentList(ListView):                \\
					model = Student                          \\
				
				class StudentDetails(DetailView):
					model = Student
				
				class StudentUpdate(UpdateView):
					model = Student
					fields = ['name','course']
					success_url = '/'
				
				class StudentDelete(DeleteView):
					model = Student
					success_url = '/'
					
				
			urls.py :
			
				from django.urls import path
				from.views import StudentAdd,StudentDetails,StudentList,StudentUpdate,StudentDelete
				
				urlpattern = [
				
					path('add/',StudentAdd.as_view()),
					path('list/',StudentList.as_view()),
					path('<int:pk>',StudentDetails.as_view()),
					path('update/<pk>',StudentUpdate.as_view()),
					path('delete/<pk>',StudentDelete.as_view()),
				]
				
				
			project/urls.py :
				
				from django.contrib importadmin
				from django.urls importpath, include
				
				urlpatterns = [
					path('admin/',admin.site.urls),
					path('', include('student.urls')),
				]
				
				
			project/settings.py :
			
				INSTALLED_APPS=[
					'django.contrib.admin',
					'django.contrib.auth',
					'django.contrib.contenttypes',
					'django.contrib.sessions',
					'django.contrib.messages',
					'django.contrib.staticfiles',
					'student',
				]
				
				
		2. create new directory "template" --> 
	
			inside "template" create new directory (directory name = app name) -->
	
				inside new directory --> write html files
				
				
					Student_form.html
					
					Student_list.html              -               (list all records)
					
					Student_details.html        -         (to get a particular record)
					
					Student_Confirm_delete.html
				
		
				
				
		3. Migrate 
	
			!--cmd --!   #in terminal
			
					python manage.py makemigrations
					
					-->
					
						python manage.py migrate
					
						-->
					
							python manage.py runserver
							
							
							
							
	4. Admin creation and connection

		1. admin.py 
		
	
			from django.contrib import admin
			from .models import Student
			
			#Register your model shere.
			
			class StudentAdmin(admin.ModelAdmin):
				list_display = ('name','course')
				search_fields = ('name','course')
			
			admin.site.register(Student,StudentAdmin)
		
		
				
			§ !--cmd--!     #in terminal
			
		
				python manage.py createsuperuser
				
					-->
					
						python manage.py runserver
![image](https://user-images.githubusercontent.com/82816086/219459839-e1bdfc4b-e982-4712-a0fd-1feb1a6eadc9.png)


