======
NoAttr
======

When accessing an object with chained attributes, ::

    info = obj.a.b.c.d or 'Unknown'
    
naïvely this will fail as soon as one of the intermediate attributes returns ``None``: ::
    
    >>> obj.a 
    None
    
    >>> obj.a.b.c.
    AttributeError: 'NoneType' object has no attribute 'b'
    
*NoAttr* gives you a way around this in cases where a series of ``None`` checks would be too much effort and result in complex code. 
Instead of returning ``None``, you want to return an instance of ``NoAttr``, which will caused hierarchical attribute accesses to keep returning ``NoAttr`` until the end of the chain ::

    >>> from noattr import NoAttr
    >>> obj = NoAttr

    >>> obj.a
    NoAttr
    
    >>> obj.a.b.c.d
    NoAttr
    
*NoAttr* behaves as a "falsy" value, meaning that it can stand for ``None``, ``False``, ``0``, ``''``, ``[]`` or ``{}``, depending on context. Here are some examples: ::

    >>> obj.a
    NoAttr
    
    >>> obj.a.b.c.d or 'Unknown'  # behaves like a falsy value
    'Unknown'
    
    >>> for i in obj.a.b.c.d:  # behaves like an enumerable that does not yield a value
    ...     print(i)
    (no output)
    
    >>> len(obj.a.b.c.d)  # behaves like an empty collection
    0
   
    >>> obj.a.b.c.d + 1  # behaves like a 0
    1
    
    >>> obj.a.b.c.d.anyfunc()  # behaves like a callable
    NoAttr

However, for ``ljust()``, ``rjust()``, ``rfind()``, ``find()``, ``rindex()``, ``index()``, and ``count()``, *NoAttr* is seen as a single whitespace character (``' '``) to preserve the expected behavior of these methods: ::
    
    >>> obj.a.b.c.d.ljust(3)
    '   '

Installation
############

$ ``pip install noattr``
