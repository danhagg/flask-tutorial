For Linux and Mac:

$ export FLASK_APP=flaskr
$ export FLASK_ENV=development
$ flask run

For Windows cmd, use set instead of export:

> set FLASK_APP=flaskr
> set FLASK_ENV=development
> flask run

For Windows PowerShell, use $env: instead of export:

> $env:FLASK_APP = "flaskr"
> $env:FLASK_ENV = "development"
> flask run

FLASK_APP="hello:create_app('dev')"
The create_app factory in hello is called with the string 'dev' as the argument.

The environment in which the Flask app runs is set by the FLASK_ENV environment variable. 
If not set it defaults to production. The other recognized environment is development. 
Flask and extensions may choose to enable behaviors based on the environment.
If the env is set to development, the flask command will enable debug mode and flask run will enable the interactive debugger and reloader.
FLASK_ENV=development flask run

To explore the data in your application, you can start an interactive Python shell with the shell command. 
An application context will be active, and the app instance will be imported.

flask shell

Use shell_context_processor() to add other automatic imports.

The flask command is implemented using Click. 

This example adds the command create-user that takes the argument name.

```python
import click
from flask import Flask

app = Flask(__name__)

@app.cli.command("create-user")
@click.argument("name")
def create_user(name):
    ...
```
$ flask create-user admin

This example adds the same command, but as user create, a command in a group. This is useful if you want to organize multiple related commands.

```python
import click
from flask import Flask
from flask.cli import AppGroup

app = Flask(__name__)
user_cli = AppGroup('user')

@user_cli.command('create')
@click.argument('name')
def create_user(name):
    ...

app.cli.add_command(user_cli)
```

$ flask user create demo