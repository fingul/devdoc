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

# django plugin

conda install jupyter

> jupyter-notebook 

- faker + modelmommy
mommys_boy
django-inspect-model



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
