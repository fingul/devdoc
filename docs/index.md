# Welcome to MkDocs

For full documentation visit [mkdocs.org](http://mkdocs.org).

# stack

- study

    udemy

- single page app

    angular2 / ionic2

- django

- foreground process manager

    circus + config file + autoreload

- background process(taskqueue)

    `celery` -> `rq`

    - todo : make `rq task killer` 

# bootstrap django

<http://www.metaltoad.com/node/1109>
<https://dezoito.github.io/2016/01/06/django-automate-browsersync.html>


    # cookiecutter 1.5 not released yet. (need for extra argument)
    pip install -e git+https://github.com/audreyr/cookiecutter#egg=cookiecutter


    cookiecutter --no-input https://github.com/pydanny/cookiecutter-django  project_name=za author_name=fingul email=0@0.com timezone=Asia/Seoul use_celery=n use_heroku=y
    mkconda za
    pip install -r requirements/local.txt
    npm i
    createdb za
    python manage.py migrate
    echo "User.objects.create_superuser('0', '0@0.com', '0')" | python manage.py shell_plus
    pip install honcho

    touch 0.$(date +"%Y%m%d_%H%M%S").txt

    cat <<EOT >> greetings.txt
    line 1
    line 2
    EOT



 9526  honcho start
 9527  nano Procfile
 9528  
 9529  honcho start




> Procfile 
web: python manage.py runserver
worker: celery worker --app=za.taskapp --loglevel=info
watch: gulp watch
 







# wagtail

<https://github.com/torchbox/wagtail/wiki/Contributed-apps-and-website-code>

이건 갑임. 홈피 끝판왕

<https://github.com/chrisdev/wagtail-cookiecutter-foundation>

# django plugin

conda install jupyter

> jupyter-notebook 

- mommys_boy = faker + modelmommy
- django-inspect-model



        ./manage.py shell_plus --print-sql


        IPYTHON_ARGUMENTS = [
            '--ext', 'django_extensions.management.notebook_extension',
            '--ext', 'myproject.notebook_extension',
            '--debug',
        ]

        SHELL_PLUS_PRE_IMPORTS = (
            ('module.submodule1', ('class1', 'function2')),
            ('module.submodule2', 'function3'),
            ('module.submodule3', '*'),
            'module.submodule4'
        )

    ipython --ext=autoreload

    mkdocs serve -a :9000


## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs help` - Print this help message.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.
