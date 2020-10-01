### Variable and class naming conventions

* naming conventions:
	* Function: Use a lowercase word or words. Separate words by underscores to improve readability.	```function, my_function````
	* Variable: 	Use a lowercase single letter, word, or words. Separate words with underscores to improve readability.	x, var, my_variable
	* Class:	Start each word with a capital letter. Do not separate words with underscores. This style is called camel case.	```Model, MyClass```
	* Method:	Use a lowercase word or words. Separate words with underscores to improve readability.	```class_method, method```
	* Constant:	Use an uppercase single letter, word, or words. Separate words with underscores to improve readability.	```CONSTANT, MY_CONSTANT, MY_LONG_CONSTANT```
	* Module: Use a short, lowercase word or words. Separate words with underscores to improve readability.	```module.py, my_module.py```
	* Package: Use a short, lowercase word or words. Do not separate words with underscores.



* when to add underscore to methods or attributes?
	- clearly internal method that does not have any standalone sense (messy intermediate operation or helper)
	- method for private use, that can be misinterpreted and used publicly
	- public method duplicate names with underscore for implementation details helpers


* for module global constants - can start with underscore if they are for private use
	- the will be still accessible but not loaded with import *
	- another way to specify what's in import * is to define __all__
	- conventionis to define __all__ and use w/o underscores if there a lot of constants for private use
	- if there's a few number of them - better use underscroe

* use or pre- and post underscores (conventions)
	- single pre-underscore : private method
	- single post-underscore : for variable names coinciding with keywords (e.g. class_, len_)
 	- double pre-underscore : Any identifier of the form ```__spam``` (at least two leading underscores, at most one trailing underscore) is textually replaced with _classname__spam, where classname is the current class name with leading underscore(s) stripped. This mangling is done without regard to the syntactic position of the identifier, so it can be used to define class-private instance and class variables, methods, variables stored in globals, and even variables stored in instances. private to this class on instances of other classes. 
 	Using this will prevent from automatic access to the field in a derived class (i.e. if we have __x in Base, we cannot directly assign to __x in Derived)
 	_ double pre-post: magic methods (__str__, __init__ etc)




## Splitting of the code into modules, classes, functions

* define constants on the level where they are exactly used:
	- if used for multiple functions or method from different class in a module, define on the module level
	- if used for multiple modules, put in a separate config file
	- if used inside a function, define inside this function
	- if inside a class, define as class attributes
	- in all cases constant is smth that won't change its value during execution, and must be name with capital snake style

* constants can be organized into dict by logical groups
* to store constant list of value - more convenient to use tuple, can always transform to list, but can use as default value in functions


* for reading config files - better to write config class in a separate module, client modules with load class and interact with config through the interface; 
later even if config format changes, I only need to change the config API class



* recommended to divide big package into sub packages (subfolders with __init__.py file each)






## Signs that it's better to use OOP instead of functional programming

* inside a module there are multiple groups of function that work in chain on different data/variables;
there no reason why those groups must see each other: better to split functions into classes and put common data for function groups into class variable

* multiple groups of functions requires separate subsets of constants, config specifications (again will put those constants subsets in different classes)



* If you need to preserve some state between function calls, use class with a method, not function (e.g. need to save the running number of function calls, or any variable, that must be persistent outside function)

* If function is called multiple times and some argument subset is repeated, then better to craeate a class, where these argumets are class variables and functions are methods, e.g.
```
df = ...
f1(df, x, y)
f1(df, w, z)
f2(df, a)
f2(df, b)
```
replace with class containing df, and methods .f1(x, y), .f2(a)

* **If we have data and functions acting specifically on these data, create a class with these data and functions as methods**

* In Python you can get away with using lists, dictionaries, tuples, numpy arrays and other common collections to group data, without having to write a custom class just for storage. E.g. a df input for which we access certain columns implicitly specifies an interface for this arg : dataframe with those columns existing.
	- use custom classes if there methods along with data
	- otherwise can use standard libs types, and dicts of them
	- standard class with just data variables basically has the functionality of a dict (but w/o .items(), .keys() etc)
	- a good is example is dataframe and xarray in one container for which we can select date interval for both df and xr simultaneously


* method class without data for composition interface: if function consists of multiple steps, that can be overloaded, but the composition is always the same -> then it's a usecase for an abstract class (like Learner with data_check, fit, predict, collect_summary etc)

* a function that must take some config constants, etc is good case for a class (put config in the class, create one class method, or implement __call__)


* **if I want to fix the API for some resource**, say config file or another extract - create a class for it:
	- sometimes this is not necessary: e.g. the resource is a csv, I load it to dataframe; then the client code accesses some fields; ok to have a simple function to load it, the client code creates an implicit interface
	- however, a proper way would be to set a data manager for this file (it may contain parameters, e.g. extract date, and method to get full path, etc, and a method to return data in the fixed format, and also assert the format)
	- this is especially useful if the resouces is not controlled or create by us - e.g. result of API call


* if I have multiple functions with names like get_dataset_element, get_dataset_fields, load_dataset -> dataset is in all names - maybe it's better to have a class representing dataset and related functions as methods
	- using function names (along with argument and their names) is good rule of thumb to group functions into classes and extract data outside functions


* another case for OOP use : if a middleman functionality is reused many times, can put it in a class with everything around it as abstract; then a particular implementation will fill those methods









## Language conventions



* try to always simplify or even abbreviate module names; should avoid long names with more than 2 words for this, should be shorter than class names (e.g. AssetClassBuffer class may be in a file named just buffer)


* inside a class can simplify method names depending on the class name, examples:
	- normalize_equity_data inside EquityData -> normalize
	- normalize_equity_data inside EquityDataManager -> normalize_data


* for a class consisting of one method (enhanced function):
	- can use the following naming style:
	evaluate_feature -> FeatureEvaluator.evaluate
	normalize_data -> DataNormalizer.normalize

* prefered way should be to explicitly use namespaces; thus it's better to shorten them like  
```import numba as nb``` and use ```@nb.njit``` then to import smth from numba directly


* for abbreviations, leave them all uppercase, e.g. like in JSONStatistics



* conventions: 
	- start with get_ : smth that return smth from a class variable (with minor extra steps) 
	- start with load_ : smth that actually load the data from somewhere, not just returns a class variable
	- write_ or save_: smth that writes to a file
	- create : smth that applies some functionality to create a new object, and then returns it or saves inside a class (but probably not saves)
	- add _one suffix and pre-underscore for pattern where I have a function for a single element first, and then aggregated over element list in the main function


* try to hit a balance between being too vague and being too verbose, the class/module name can help to shorten the function/method name : can skip what is already mention in the class/module name (but only do this to shorten the function name)
* add docstring if you feel like the function name is not self-evident and is supposed to be used in client code


* Dataset and DataManager (and similar : DataHander etc) class name (and equivalent examples)
	- use Dataset if it's a containers having multiple data variables, which are created during instance construction;
	the methods must mostly work with data extraction, queries, insertions, stats, etc
	- use name DataManager if the class has more broad responsibilities : loading and normalizing data, saving data, or does not have fixed data varaibles at all and e.g. provides a generator and subsequently loads data chunks
	- e.g. for config api simple name is good : like ModelConfig
	- when class is resource API, simple name is ok
	- for data pipeline use DataManager (??, can use DataPipeline ??)






## str or list

* it often happens that a function is taking a list of str or a single str which will be equivalent to a single element list

* the preferred way to do this is to
	- impose str or list input type
	- check type at the start
	```
	def f(arg : Union[str, List[str]]):
		if isinstance(arg, str):
			arg = [arg]
		...
	```
	- if instead for the list the behaviour is different and it requires going through indiv. str calls, 
	check for types str, then list, then throw error
	- do not implement it for array-like sequences of str (comlicated and most often useless)
	- **don't write any decorators for this** unless absolutely necessary and additional functionality is used


## Inheritance, classes


* sometimes we need to create derived class instance from base class instance:
	- doing by changing __class__ attribute of the instance is a dirty trick, **don't do it**
	- must either have copy constructor in the derived, that might use super() copy construct from base inside
	- but the best is to use composition overall instead of inheritance in this case




* composition is always recommeneded instead of inheritance if possible
	* inheritance may create obscure construction, hard to work with
	* existing code may check for type, not just use methods of a class, so inheritance won't guarantee that all code used for base class will work for the derived class
	* instead of inheriting to just add a couple of methods and try to use derived class everywhere instead of base - just write several simple functions (instead of methods) to apply where necessary
	* try to restrict inheritance to subclassing simple interface (e.g. via abc module), and not existing class that's used in many places already
	* natural case where inheritance maybe used is for abstract classes (interfaces), mixins, and for direct obvious augmentations 



* to put common functionality from child classes to parent class need at least 3 different use cases in prod
	- if that requires type switch-case in the base class -> no much value in it, better leave it with some code duplication in child classes
	- don't try to predict what will be used later and don't add unused functionality in interfaces


* to create abstract interfaces use abc.ABC, abs.abstractmethod, etc decorators (same for class and static method)
	- abstract method can also have implementation
	- this just indicates that it must be reimplemented in the derived class, thus imposes an interface

* use dataclasses to assign multiple attribute in __init__



## Data format conventions

* in my own code always better and more robust to fix input types, use typing hints
* **however in most cases it's not recommended to explicitly check types in the code** since it contradicts the basic python principle: duck typing; just need to specify hint, the user will understand what to pass

* examples:
	- if function processes list, don't try to make it work with array like, ok to use list methods, and specify list in the typing hint
	- if passing date, pass it e.g. as date_iso string, and map to pandas timestamp with explicit format
	- avoid third library generalized convertions like in pd.to_datetime(..) - have to be more explicit
	- in those libs : generality is because the lib has millions of users, not the case for my code, I can adjust the client code for the function if needed, make it more flexible if there are really a lot of useful use-cases

* main principle for my programming : always make service code as simple as possible; need to accumulate enough client cases to make any complications


* a config file could be .py but as a general rule yaml file is preferred because .py is executable and is not suitable for config in serous apps (e.g. anything can be put there by hackers and the code will run by loading config, also sometimes low-priority users are allowed to change yaml config files, but not .py code files) : my convention - **always use .yaml for config** unless it requires more complicated python structures than lists and dicts



## Typical patterns in data analysis and quant trading

* avoid all sort of automatic detections, e.g. if I need smth to work with existing list of class, have this list specified direcly, do not make any implicit criteria
* avoid too smart functions that do different things depending on the input type: better to split into multiple function with clear names, or pass the functionality to convert to a unique input type to the client code


* implementing \_\_call\_\_ is usually not a good way to go if the functionality is more or less the same all the time, better create a method with clear name to do the same functionality


* need to generally minimize or avoid wrapper layers, they only must serve important purposes

* create type hints using typing module, same name conventions as for new types as for a class (cap camel)


* preferred way for data cleaning/normalization/queries is to use chains; can create function to implement separate stages and then chain them with .pipe(...)


* can use try catch to reraise certain errors with more specific message 


* if class is getting too big, it means it has too much responsibility; separation into functions and classes should be mostly by size than by action (to avoid both soft and hard code); can always split bigger class into smaller classer 
(e.g. DataLoader, DataNormalizer etc)


* for my programming business domain is always the same: data normalization pipelines, daily flat-file data extracts, datasets, data managers (daily and intraday data), financial calendar, http api sessions, learners, feature evaluators, signal, model, portfolio optimizers, backtesters, backtest stats, transaction cost model, etc etc
---> this largely simplifies my preparation -- need to know various solution to the same set of problems in detail;
----> for data processing the area of problems may be more reach; may altimately it's still very narrow; there no business logic like in standard web applications with complicated business-related backend












