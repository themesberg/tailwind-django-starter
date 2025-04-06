# Tailwind Django Starter

By [following this guide](https://flowbite.com/docs/getting-started/django/) you will learn how to properly set up a Django project with Tailwind CSS and Flowbite to start developing modern web applications even faster.

## Requirements

Follow the next steps to create a new Django project and install Tailwind CSS with Flowbite to get the full benefits of the component library.

Make sure that you have both [Node.js](https://nodejs.org) and [Python](https://www.python.org/) installed on your local machine.

After that, you'll need to install Django on your local computer by following the official [installation guide](https://docs.djangoproject.com/en/4.0/intro/install/) or by running the following command in the terminal if you have pip available in your Python environment:

```bash
python -m pip install Django
```

Now that you have all the required technologies installed you can start by creating a new Django project.

## Create a Django project

1. Run the following command in the terminal to create a new Django project with the name `flowbiteapp`:

```bash
django-admin startproject flowbiteapp
cd flowbiteapp/
```

2. Create a new `templates/` directory inside the project folder and then update the existing `settings.py` file:

```bash
TEMPLATES = [
    {
        ...
        'DIRS': [BASE_DIR / 'templates'], # new
        ...
    },
]
```

3. Install `django-compressor` and `django-browser-reload` by running the following commands in your terminal:

```bash
python -m pip install django-compressor
```
```bash
python -m pip install django-browser-reload
```

4. Add `compressor`,`django_browser_reload` and `flowbiteapp` (or the name of your app) to the installed apps inside the `settings.py` file:

```bash
# config/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'compressor',  # new
    'flowbiteapp',  # new
    'django_browser_reload' #new
]
```

5. Configure the `compressor` inside the `settings.py` file:

```bash
COMPRESS_ROOT = BASE_DIR / 'static'

COMPRESS_ENABLED = True

STATICFILES_FINDERS = [
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',
    'compressor.finders.CompressorFinder',
]
```
6. Add the Middleware in the `settings.py`:
```bash
MIDDLEWARE = [
    # ...
    "django_browser_reload.middleware.BrowserReloadMiddleware",
    # ...
]
```   
6. Create two new folders and an `input.css` file inside the `static/src/` folder:

```bash
static
└── src
    └── input.css
```

Later we will import the Tailwind CSS directives and use it as the source file for the final stylesheet.

7. Create a new `views.py` file inside `flowbiteapp/` next to `urls.py` and add the following content:

```bash
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

8. Import the newly created view instance inside the `urls.py` file by adding the following code:

```bash
from .views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index, name='index')
]
```

9. Create a new `_base.html` file inside the `templates/` directory:

```html
<!-- templates/_base.html -->

{% load compress %}
{% load static %}

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Django + Tailwind CSS + Flowbite</title>

    {% compress css %}
    <link rel="stylesheet" href="{% static 'src/output.css' %}">
    {% endcompress %}

</head>

<body class="bg-green-50">
    <div class="container mx-auto mt-4">
        {% block content %}
        {% endblock content %}
    </div>
</body>

</html>
```

10. Create an `index.html` file that will be served as the homepage:

```html
<!-- templates/index.html -->

{% extends "_base.html" %}

{% block content %}
  <h1 class="text-3xl text-green-800">Django + Tailwind CSS + Flowbite</h1>
{% endblock content %}
```

11. Finally, create a local server instance by running the following command:

```bash
python manage.py runserver
```

You'll now get an error that the `output.css` file doesn't exist, but that'll be fixed once we install Tailwind CSS.

Awesome! Now you have a working Django project locally. Let's continue by installing Tailwind.

## Install Tailwind CSS

1. Run the following command the install Tailwind CSS as a dev dependency using NPM:

```bash
npm install tailwindcss @tailwindcss/cli --save-dev
```

2. Import the Tailwind CSS directive inside the `input.css` file:

```css
/* static/src/input.css */

@import "tailwindcss";
```

4. Run the following command to watch for changes and compile the Tailwind CSS code:

```bash
npx @tailwindcss/cli -i ./static/src/input.css -o ./static/src/output.css --watch
```

Open `localhost:3000` in your browser and you'll see working HTML with Tailwind CSS code.

Now that you have configured both Django and Tailwind CSS you can also set up Flowbite to get access to the whole collection of interactive components like navbars, modals, dropdowns, buttons, and more to make development even faster.

## Install Flowbite

Flowbite is an open source library of interactive components built on top of Tailwind CSS and it can be installed using NPM and required as a plugin inside Tailwind CSS.

1. Install Flowbite as a dependency using NPM by running the following command:

```bash
npm install flowbite --save
```

2. Import the default theme variables from Flowbite inside your main `input.css` CSS file:

```css
@import "flowbite/src/themes/default";
```

3. Import the Flowbite plugin file in your CSS:

```css
@plugin "flowbite/plugin";
```

4. Configure the source files of Flowbite in your CSS:

```css
@source "../../node_modules/flowbite";
```

5. Include Flowbite's JavaScript file inside the `_base.html` file just before the end of the `<body>` tag using CDN or by including it directly from the `node_modules/` folder:

```html
<script src="https://cdn.jsdelivr.net/npm/flowbite@3.1.2/dist/flowbite.min.js"></script>
```

Now that you have everything configured you can check out the components from Flowbite such as navbars, modals, buttons, datepickers, and more.

## Flowbite components

You can now start using the components from [Flowbite](https://flowbite.com/blocks/).
