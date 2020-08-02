* cannot get the length of any iterable with casting it to list (this will load the whole list in case the iterable was a generator)

* The most Pythonic idiom is to clearly document what the function expects and then just try to use whatever gets passed to your function and either let exceptions propagate or just catch attribute errors and raise a TypeError instead. Type-checking should be avoided as much as possible as it goes against duck-typing. Value testing can be OK – depending on the context.

* check if None: just use ```if var``` instead of ```if var is None```

* in python>=3.7 standard dicts retain order?? (don't need OrderedDict anymore?)