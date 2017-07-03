# Flask Cheat Sheet

___
## Table of contents
* [Database](#database)
* [Files](#files)
* [Login](#login)
* [Manager](#manager)
* [Others](#others)
___

## Database
___
### Upload files to database using BLOB type.

> add one Column to Model
  
    class MyModel(db.Model):
        ...
        file_data = db.Column(db.LargeBinary)

> get from request and add to database

    @app.route('/upload', methods=['POST'])
    def upload():
        _file = request.files['inputFile']
        new_fileile = MyModel(..., file_data=_file.read())
        db.session.add(new_file)
        db.session.commit()
___
___

## Files
___
### File view
    
> import this class

    from io import BytesIO

> use it

    @app.route('/file/<filename>')
    def get_file(filename):
        _file = MyModel.query.filter_by(file_name=filename).first()
        if _file:
            return send_file(BytesIO(_file.file_data), attachment_filename=_file.file_name)
        return abort(404)
___
___

## Login
___

### Logging Users In

> import all what do we need

    from flask import render_template, redirect, request, url_for, flash
    from flask_login import login_user
    from ..models import User
    from .forms import LoginForm
    
> and let's write login function

    @auth.route('/login', methods=['GET', 'POST'])
    def login():
        form = LoginForm()
        if form.validate_on_submit():
            user = User.query.filter_by(email=form.email.data).first()
            if user is None or not user.verify_password(form.password.data):
                flash('Invalid email or password')
                return redirect(url_for('.login'))
            login_user(user, form.remember_me.data)
            return redirect(request.args.get('next') or url_for('main.index'))
        return render_template('auth/login.html', form=form)

___

### Logging Users Out

> import some functions 
    
    from flask_login import logout_user, login_required

> and let's write logout function

    @auth.route('/logout')
    @login_required
    def logout():
        logout_user()
        flash('You have been logged out')
        return redirect(url_for('main.index'))

___
___

## Manager
___
### User Registration

> import db and User objects

    from app import db
    from app.models import User
    
> add these lines in manage.py
    
    # ...
    
    @manager.command()
    def adduser(email, username, admin=False):
        """Register a new user"""
        from getpass import getpass
        password = getpass()
        password2 = getpass(prompt='Confirm')
        if password != password2:
            import sys
            sys.exit('Error: passwords do not match.')
        db.create_all()
        user = User(email=email, username=username, password=password, is_admin=is_admin)
        db.session.add(user)
        db.session.commit()
        print('User {0} was registered successfully.'.format(username))
        
___
___

## Others
___
### Flashed Messages

> app/templates/base.html
    
    ...
    {% for message in get_flashed_messages() %}
    <div class="alert alert-warning">
        <button type="button" class="close" data-dismiss="alert">x</button>
        {{ message }}
    </div>
    {% endfor %}
    ...