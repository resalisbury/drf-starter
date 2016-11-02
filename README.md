a skeleton of a DRF app 

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

## RAML Documentation
follow instructions here: https://github.com/tomchristie/django-rest-raml

## Auto generate code
follow instruction here: https://github.com/Brobin/drf-generators


```
# generally the below is fine
python manage.py generate api --format viewset
```

