# Python

## Call parent constructor

```python
def __init__(self, instance=None, data=empty, **kwargs):
    ...
    super(BaseSerializer, self).__init__(**kwargs)
```

## dict.pop()/.update()
```python
kwargs.pop('key', default_value)
...
list_kwargs.update({
    key: value for key, value in kwargs.items()
    if key in LIST_SERIALIZER_KWARGS
})
```

## __init__ vs __new__

__init__ is `instance level`, used to `initialize instance`, returns nothing
__new__ is `class level`, used to `create instances`, returns an instance

```python
def __init__(self, instance=None, data=empty, **kwargs):
    ...

def __new__(cls, *args, **kwargs): # check first arg `cls` because its class level
    if kwargs.pop('many', False):
        return cls.many_init(*args, **kwargs)
    return super(BaseSerializer, cls).__new__(cls, *args, **kwargs)
```


# REST Framework

Start from `serializer`, first we bypass the case for many

ModelSerializer <= Serializer <= BaseSerializer

BaseSerializer
    __new__
        _many_init
    __init__

    .data (an `property`)
