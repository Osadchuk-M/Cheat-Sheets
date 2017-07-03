# Flask-extensions Cheat Sheet
___

## Table of contents
* [flask-bootstrap](#flask-bootstrap)
* [flask-login](#flask-login)
* [flask-moment](#flask-moment)
* [flask-script](#flask-script)
* [flask-sqlalchemy](#flask-sqlalchemy)
* [flask-wtf](#flask-wtf)
___

## Flask Bootstrap
___
> shell

    (venv) $ pip install flask-bootstrap

> app/\__init\__.py
    
    from flask_bootstrap import Bootstrap
    bootstrap = Bootstrap()
    
    def create_app(config_name):
        # ...
        bootstrap.init_app(app)
        # ...
        return app
        
> app/templates/index.html

    {% extends 'bootstrap/base.html' %}
    
    {% block title %} This is Title {% endblock %}
    
    {% block navbar %}
        ...
    {% endblock %}
    
    {% block content %}
    <div class="container">
        <h1>Hello, Maxim!</h1>
    </div>
    {% endblock %}
___
___

## Flask login
___
> shell

    (venv) $ pip install flask-login
    
> app/\__init\__.py

    from flask_login import LoginManager
    login_manager = LoginManager()
    login_manager.login_view = 'auth.login'
        
    def create_app(config_name):
        # ...
        login_manager.init_app(app)
        # ...
        return app

> models.py

    from flask_login import UserMixin # add some methods to our class(is_authenticated(), is_active(), ...)
    from . import db, login_manager
    
    class User(UserMixin, db.Model):
        # ...
        
    @login_manager.user_loader
    def load_user(user_id):
        return User.query.get(int(user_id))
___
___

## Flask moment
___
> shell

    (venv) $ pip install flask-moment
    
> app/\__init\__.py
    
    from flask_moment import Moment
    moment = Moment()
    
    def create_app(config_name):
        # ...
        moment.init_app(app)
        # ...
        
> app/templates/base.html

    {% block scripts %}
    {{ super() }}
    {{ moment.include_moment() }}
    {% endblock %}
    
> use it
    
    {{ moment(talk.date, local=True).format('LL') }}
___
___

## Flask script
___
> shell
    
    (venv) $ pip install flask-script

> manage.py

    #!/usr/bin/env/ python
    import os
    from app import create_app
    from flask_script import Manager
    
    app = create_app(os.getenv('FLASK_CONFIG') or 'default')
    manager = Manager(app)
    
    if __name__ == '__main__':
        manager.run()

> shell

    (venv) python manage.py runserver
___
___
## Flask-SQLAlchemy
___
> shell

    (venv) $ pip install flask-sqlalchemy
    
> manage.py or not
    
    app.config['SQLALCHEMY_DATABASE_URI'] = 'path/to/database.db'
___
___
## Flask-WTF
___

>shell

    (venv) $ pip install flask-wtf
    
> use in view

    @route('/some_url', methods=['GET', 'POST'])
    def foo():
        form = MyForm()
        if form.validate_on_submit():
            # process form data
            # values are in form.<field>.data
            return redirect(url_for('...'))
        # initialize form fields here
        # form.<field>.data = value
        return render_template('template.html', form=form)
___
___