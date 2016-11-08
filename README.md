## Get Django Running

```
git clone https://github.com/resalisbury/drf-starter
cd drf-starter

# get the venv setup
virtualenv venv
sh -c 'touch .env; echo source $PWD/venv/bin/activate > .env'
cd .  # activates the venv, simply by cd-ing into to the current directory
which python  # should be ./venv/bin/python
pip install --upgrade --no-binary :all: -r requirements/dev.txt

#start the project
django-admin startproject website
cd website

# check everything is working
python manage.py runserver

# run migrations
python manage.py migrate

# visit localhost:8000/admin to verify all is hunky dory

# create a new app and you're off!
python manage.py startapp api
```
## Wire things together

update website/urls.py to:
```
from django.conf.urls import url, include
from django.contrib import admin
from rest_framework.schemas import get_schema_view
from rest_framework_raml.renderers import RAMLRenderer, RAMLDocsRenderer


schema_view = get_schema_view(
    title='Example API',
    renderer_classes=[RAMLRenderer, RAMLDocsRenderer]
)


urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^raml/$', schema_view),
    # url(r'^api/', include('api.urls')),
]
```

update website.settings.INSTALLED_APPS to:
```
INSTALLED_APPS = [
    # django
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    # third party
    'django_extensions',

    # DRF
    'rest_framework',
    'rest_framework_raml',
    'drf_generators',

    # Apps
    'api',
]
```
## Write your first model
...in api.models

for example:
```
from __future__ import unicode_literals

from django.db import models


class Author(models.Model):
    name = models.CharField(max_length=40, blank=True, null=True)
    age = models.IntegerField(blank=True, null=True)

## Auto generate code
```
# generally the below is fine
```
python manage.py generate api --format modelviewset
```
uncomment `url(r'^api/', include('api.urls'))` to wire it all together
```
urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^raml/$', schema_view),
    # url(r'^api/', include('api.urls')),
]
```
more info: https://github.com/Brobin/drf-generators

## RAML Documentation
more info: https://github.com/tomchristie/django-rest-raml




