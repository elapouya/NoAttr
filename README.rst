======
NoAttr
======

When you access an object with chained attributes ::

    info = obj.a.b.c.d or 'Unknown'
    
Usually, it will failed when one intermediate attribute return ‘None‘ ::
    
    if obj.a returns None
    obj.a.b.c.d will fail with that exception :
    AttributeError: 'NoneType' object has no attribute 'b'
    
To avoid that, instead of returning a ‘None‘ value, one should return ‘NoAttr‘, by this way, 
even next chained attribute will return ‘NoAttr‘ ::

    if obj.a returns NoAttr
    obj.a.b.c.d will not fail and will return NoAttr
    
‘NoAttr‘ can be seen as False, 0, '', [] or {} depending on the context, so ::

    if obj.a returns NoAttr
    
    obj.a.b.c.d or 'Unknown' will return 'Unknown'
    
    for i in obj.a.b.c.d:
        print i
    prints nothing     
   
    obj.a.b.c.d + 1 returns 1
    
    obj.a.b.c.d.anyfunc() returns NoAttr
    
    but for ljust(), rjust(), rfind(), find(), rindex(), index(), count()
    NoAttr is seen as '' :
    
    obj.a.b.c.d.ljust(3) returns '   '