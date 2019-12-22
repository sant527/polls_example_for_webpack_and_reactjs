## Example to demonstrate webpack and reactjs:

In the project https://github.com/sant527/django_basic_documentation_ver2. We will be importing this repo to demostrate example of using webpack and reactjs and django-webpack.

Installing npm, webpack, react, babel, django-webpack and setting up webpack and babel is discussed there.

Go to the project folder (where .manage.py resides)

```bash

$ svn ls https://github.com/sant527/polls_example_for_webpack_and_reactjs.git

$ svn export https://github.com/sant527/polls_example_for_webpack_and_reactjs.git/trunk/polls_example_for_webpack_and_reactjs
```

Add `polls_example_for_webpack_and_reactjs.polls` to the installed `INSTALLED_APPS`


Eg:
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'polls_example_for_webpack_and_reactjs.polls'
]
```

Then make the migrations
```bash
 $ python manage.py makemigrations
 $ python manage.py migrate
```

### Providing initial data for polls models

Here we are providing data using fixtures file: https://docs.djangoproject.com/en/3.0/howto/initial-data/#providing-data-with-fixtures

Its just a json file lying inside a folder called fxitures inside the app

Here it is `polls_example_for_webpack_and_reactjs/polls/fixtures/poll_database.json`

We have created some initial data to pass and test. To add that to database just do

```bash
$ manage.py loaddata poll_database.json
```

Then add to the webpack.config.js the paths of the ReactJs files

Assuming the name of the folder which contains `manage.py` is `basic_django`

```javascript
  entry: {
    'polls/js/bundles/index':  path.resolve(__dirname, 'basic_django/polls_example_for_webpack_and_reactjs/polls/static/polls/js/index.js'),
    'polls/js/bundles/question':  path.resolve(__dirname, 'basic_django/polls_example_for_webpack_and_reactjs/polls/static/polls/js/questions.js'),
   },

  output: {
    path: path.join(__dirname)+"/basic_django/polls_example_for_webpack_and_reactjs/polls/static/", // add / at the end
    filename: "[name]-[hash].js",
  }
```

Then add to the urls of of the project

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('polls_webpack_react_example/', include('polls_example_for_webpack_and_reactjs.polls.urls')),
]
```

After starting the server open the links:

```
localhost:8000/polls_webpack_react_example
localhost:8000/polls_webpack_react_example/questions
```
