# Flask-extensions Cheat Sheet
___

## Table of contents
* [flask-bootstrap](#flask-bootstrap)
* [flask-login](#flask-login)
* [flask-moment](#flask-moment)
* [flask-script](#flask-script)
* [flask-sqlalchemy](#flask-sqlalchemy)
* [flask-whooshalchemy](#flask-whooshalchemy)
* [flask-wtf](#flask-wtf)


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


## Flask-SQLAlchemy
___
> shell

    (venv) $ pip install flask-sqlalchemy
    
> manage.py or not
    
    app.config['SQLALCHEMY_DATABASE_URI'] = 'path/to/database.db'


## Flask-Whooshalchemy

> shell
    
    (venv) $ pip install flask-whooshalchemy==0.8 (not 0.56)
    
> manage.py

    import flask_whooshalchemy
    
    # set the location for the whoosh index
    app.config['WHOOSH_BASE'] = '/path/to/whoosh'
    app.config[SQLALCHEMY_TRACK_MODIFICATIONS] = True
    
    class MyModel(db.Model):
        ...
        __searchable__ = ['field1', 'field2']
        ...
        field1 = db.Column(db.String(...), ...)
        field2 = db.Column(db.Text())
        field3 = db.Column(...)
        
    wa.whoosh_index(app, MyModel)

> python console

    >>> MyModel.query.whoosh_search('query string').all()


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
