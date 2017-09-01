    $ python
    ...
    >>> min              # built-in
        <built-in function min>
    >>> min = 42         # global
    >>> def f(*args):
            min = 2      # enclosing
            def g():
                min = 4  # local
                print(min)
