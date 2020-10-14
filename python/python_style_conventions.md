* Function: Use a lowercase word or words. Separate words by underscores to improve readability.	```function, my_function````
* Variable: 	Use a lowercase single letter, word, or words. Separate words with underscores to improve readability.	x, var, my_variable
* Class:	Start each word with a capital letter. Do not separate words with underscores. This style is called camel case.	```Model, MyClass```
* Method:	Use a lowercase word or words. Separate words with underscores to improve readability.	```class_method, method```
* Constant:	Use an uppercase single letter, word, or words. Separate words with underscores to improve readability.	```CONSTANT, MY_CONSTANT, MY_LONG_CONSTANT```
* Module: Use a short, lowercase word or words. Separate words with underscores to improve readability.	```module.py, my_module.py```
* Package: Use a short, lowercase word or words. Do not separate words with underscores.	
--------

* for module global constants - start with underscore if they are non-public or (better) specify 
__all__ inside a module (that will be used if we import *)
--> my convention : write CONSTANTS_WITHOUT_UNDERSCORE and add __all__

* double underscore : Any identifier of the form ```__spam``` (at least two leading underscores, at most one trailing underscore) is textually replaced with _classname__spam, where classname is the current class name with leading underscore(s) stripped. This mangling is done without regard to the syntactic position of the identifier, so it can be used to define class-private instance and class variables, methods, variables stored in globals, and even variables stored in instances. private to this class on instances of other classes.


* don't need to defined all constants at the start of the module : if they're used once or only in the same place - define it locally before usage


questions:
- how to hold static data (constants, lists etc) - in python modules or in separate config yml file
- when I read config into global constants - where to store them
- when working with data sets / APIs sometimes need columns names as they're defined in the dataset - do I need to store those names in separate variables

----------------------------------------------------------------------------

working with datasets in python:
- always the same steps:
* have data provider (vendor or internal) where we get data through API
* for this provider we have:
	* api keys
	* constants related to the form of the raw data (e.g. url, column names, constants reflecting how the data is structured)
* may want to load raw data, preprocess, save local extract, then load it and use anytime when needed:
		->> for all this need to define name and structure conventions


my convention:
load for external source (e.g. through API)
get - for local source or simple direct getting that goes to output
typical names:
* get_fx_daily_data
* get_fx_statics
* get_redemption_yields
(the word data can be omitted or not, depending of the case)

* create_fx_extract etc for creating local extract
(get_fx_daily_data should not contain the word 'extract' because it's gonna be frequently use)

* when splitting function into getting one object and combined data for a list of objects use
_load_fx_data_one, load_fx_data etc

* normalize_fx_data for processing 
* parse_name, parse_amount

* add _one if the operation can be only done on one instance

* always separate steps like loading, processing, normalization , creation of extract and getting data 
(even if a step is trivial -- this will create a structure)

* typical problem : str_or_list decorator (think about, but if used one - always better to have smth very simple, or write directly)

-----------------------------------------------------

* avoid name like is_valid, be more specific




## misc

* create derived class instance from base class instance:
	- changing __class__ attribute of the instance is a dirty trick
	- best to use composition

* xarray dataset : can convert date coordinate using pd.to_datetime to datetime64, 
the use .sel and slice(start, end) to select data w.r.t. the date

* strange behaviour of bools and ~ & | operators --- see https://stackoverflow.com/questions/13600988/python-tilde-unary-operator-as-negation-numpy-bool-array

* best way to process extract_date, dates in a data object : do I use pd.to_datetime or enforce a specific format 
(ISO string, datetime.date object, etc)?????

* questions related to extract and job processing, timezones, days, datetime, AP EU and US, sunday runs etc

* GET, POST, PUT - go back again and make quizlet notes

* create a list of things to remember during package development (logging, pytest, CLI, etc)

* explore xr.concat, xr.merge, etc




- its ok to put constants in uppercase at the beginning of a function, class (as attribute) or module (e.g. put inside a function if it's only used in this function)
- if a constant used in a multiple modules : have a separate config file for this
- a config file could be .py but as a general rule yaml file is preferred because .py is executable and is not suitable for config in serous apps (e.g. anything can be put there by hackers and the code will run by loading config, also sometimes low-priority users are allowed to change yaml config files, but not .py code files) : my convention - always use .yaml for config

- let's use pd.Timestamp for single datetime and pd.to_datetime for arrays


- first run the full procedure (example productionizing) for a piece of code, make all run, then will be easy to generalize on the rest


-----------

* The most Pythonic idiom is to clearly document what the function expects and then just try to use whatever gets passed to your function and either let exceptions propagate or just catch attribute errors and raise a TypeError instead. Type-checking should be avoided as much as possible as it goes against duck-typing. Value testing can be OK – depending on the context.
