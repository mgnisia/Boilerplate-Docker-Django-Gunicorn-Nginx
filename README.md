# Boilerplate-Docker-Django-Gunicorn-Nginx

This repo contains a small example for a Django App in a Docker Container. For the deployment the docker container uses Gunicorn and nginx. 

The `Dockerfile` and the `docker-compose`-File are based on the repo from [pawamoy](https://github.com/Pawamoy/docker-nginx-postgres-django-example). The config file includes a setup for an additional database, however this is not included in the `docker-compose`-File. If you would like to checkout the configuration for this setup have a look in the [pawamoy](https://github.com/Pawamoy/docker-nginx-postgres-django-example)-repo.

### Manual

To build this container run in the folder of the `docker-compose`-file: 

1. `docker-compose build`
2. `docker-compose run -d` this runs the containers detachted
3. Open you favourite browser and go to [localhost/index/](localhost/index/)
4. To shutdown run `docker-compsose down`

### Installing new libraries

Just run `pipenv install your_library` and the pipenv will update the `pipfile` and check for the dependencies. Make sure you have `pipenv` installed in your own (not the virtualenv one) python3 installation.  

### Static Files

#### Dockerfile

The static files are mounted wih the volumes of the `docker-compose` files! However if you change the static files make sure, you remove the volumes with `docker volumes prune` or run `docker-compsose down -v`. Those commands remove the volumes and if you run `docker-compose build` again the volumes will be mounted again correctly :smile: You can inspect all listed mounted files in the menu

#### Templates

To include the static files in your templates you can insert in e.g. in your header:
```css
<link rel="stylesheet" href="{% static 'demo/css/main.css' %} ">
```

You can also select another path, just make sure that the static files will be collect when the command `python3 manage.py collectstatic` will be run. In the current setting the static files are set via 
`STATICFILES_DIRS = [os.path.join(BASE_DIR, 'demo', 'static'),]`.
