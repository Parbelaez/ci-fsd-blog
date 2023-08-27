# ci-fsd-blog

This is the 4th stage code-along project. It is a blog application that allows users to create, edit and delete posts. It also allows users to register and login to the application. The application is deployed to Heroku and uses a PostgreSQL database.

## Project setup

### Install dependencies

First, it is needed to create a virtual environment, which is a folder that contains a Python installation and all the packages needed for the project. This is done by running the following command at the root of the project:

```Python
python3 -m venv venv
```

**NOTE**: The name of the virtual environment folder is .venv, which is the default name. If you want to use a different name, you should add the name of the folder to the .gitignore file. Also, ```python3``` was used because the project was developed on a Mac. If you are using Windows, you should use ```python``` instead.

Then, the virtual environment is activated by running the following command:

```Python
source venv/bin/activate
```

Finally, the dependencies are installed by running the following command:

```Python
pip3 install django gunicorn dj_database_url dj3-cloudinary-storage urllib3 psycopg2 django-summernote
```

**Django**, is the main framework used to create the application. It allows the developer to create a web app using Python.
**Gunicorn** is a web server that is used to deploy the application to Heroku. dj_database_url is a package that allows the developer to connect to a database. **dj3-cloudinary-storage** is a package that allows the developer to connect to Cloudinary, which is a cloud-based image and video management service.
**urllib3** is a package that allows the developer to make HTTP requests.
**psycopg2** is a package that allows the developer to connect to a PostgreSQL database.
**django-summernote** is a package that allows the developer to add a rich text editor to the application.

After installing the dependencies, it is needed to create a requirements.txt file by running the following command:

```Python
pip3 freeze > requirements.txt
```

.venv file in the root of the project with the following variables:

```Python
import os   # for os.environ.get

# Get the environment variables
os.environ.get('DATABASE_URL') == 'YOUR_DB_URL'
os.environ.get('SECRET_KEY') == 'YOUR_SCRET_KEY!'
```

**NOTE:** The env.py file is not pushed to GitHub because it contains sensitive information. Therefore, if you want to run the project locally, you need to create your own env.py file.

But, Django also needs to know where to get the variables from, therefore, the following lines are added to the settings.py file:

```Python
import os
import dj_database_url

if os.path.isfile("env.py"):
    import env
```

### Create a Django project

**NOTE:** Please, be aware that one thing is the project and another thing is the application. The project is the whole thing, while the application is a part of the project. In this case, the project is called *ci-fsd-blog* and the application is called *blog*.

A Django project is created by running the following command:

```Python
django-admin startproject blogproj .
# The dot at the end is important because it tells Django to create the project in the current directory.
```

An app's name should follow [Pep 8 Guidelines](https://www.python.org/dev/peps/pep-0008/#package-and-module-names), namely it should be short, all-lowercase and not include numbers, dashes, periods, spaces, or special characters. It also, in general, should be the plural of an app's main model, so our posts app would have a main model called Post.

A Django application is created by running the following command:

```Python
python3 manage.py startapp blogapp
```

Then, the application is added to the project by adding the following line to the INSTALLED_APPS list in the settings.py file:

```Python
'blogapp.apps.BlogappConfig',
```



To create the templates for the registration and login pages, the following command is run:

```shell
cp -r ./.venv/lib/python3.11/site-packages/allauth/templates/* ./templates
```

This will copy all the templates from the allauth package to the templates folder.


To be able to manage the comments and have a proper interface to do so, you need to install crispy forms by running the following command:

```shell
pip3 install django-crispy-forms
```

Then, you need to add the 'crispy-forms' line to the INSTALLED_APPS list in the settings.py file.

And, as we will be using Bootstrap for these forms, then it is needed to declare the following line in the settings.py file:

```Python
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

NOTE: As of django-crispy-forms 2.0 the template packs are now in separate packages.

You will need to pip install crispy-bootstrap4 and add crispy_bootstrap4 to your list of INSTALLED_APPS.