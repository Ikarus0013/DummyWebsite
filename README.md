# DummyWebsite


Following A Flask Tutorial by Tech with Tim:

https://www.youtube.com/watch?v=dam0GPOAvVI&t=6735s

Important to mention here is:

In __init__.py this specific Section did not work anymore ... i guess Flask changed in the course of 2 Years:

-----

create_database(app)

    login_manager = LoginManager()
    login_manager.login_view = 'auth.login'
    login_manager.init_app(app)

    @login_manager.user_loader
    def load_user(id):
        return User.query.get(int(id))

    return app


def create_database(app):
    if not path.exists('website/' + DB_NAME):
        db.create_all(app=app)
        print('Created Database!')

-----

Researched a bit, and this piece of code seemed to work: 

-----

with app.app_context():
        db.create_all()

    login_manager = LoginManager()
    login_manager.login_view = 'auth.login'
    login_manager.init_app(app)

    @login_manager.user_loader
    def load_user(id):
        return User.query.get(int(id))

    return app

-----
