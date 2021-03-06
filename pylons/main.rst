The Main Function
+++++++++++++++++

Both Pyramid and Pylons have a top-level function that returns a WSGI
application. The Pyramid function is ``main`` in *pyramidapp/\_\_init\_\_.py*.
The Pylons function is ``make_app`` in *pylonsapp/config/middleware.py*. Here's
the main function generated by Pyramid's 'starter' scaffold:


.. literalinclude:: examples/starter_main.py
   :linenos:

Pyramid has less boilerplate code than Pylons, so the main function subsumes
Pylons' middleware.py, environment.py, *and* routing.py modules. Some people
like to put their route definitions in a separate module, but that's a personal
choice. The point is that Pyramid's ``main`` function has just 5 Python
statements out of the box, while Pylons' ``make_app`` 16 -- or 35 if you
include environment.py and routing.py. 

Most of the ``main`` function deals with the Configurator (``config``).  It's
not the application object; it's a helper class which configures the
application object. You instantiate the Configurator by passing the deployment
settings as keyword args, and call methods to set up routes, views, and other
things.  Finally you call ``config.make_wsgi_app()`` to get the application,
and return it. The application is an instance of ``pyramid.router.Router``. (A
Pylons application is an instance of a ``PylonsApp`` subclass.)

We'll discuss the route and view methods in their respective chapters, so
there's not much more to say here. But we'll close with a quick look at how you
can use the main function. The normal way is to run "pserve", which
automatically calls it. But you can also call it directly in Python code; for
instance to use it with a custom server or testing environment, or with
mod_wsgi. You could also wrap the application in WSGI middleware before
returning it.
