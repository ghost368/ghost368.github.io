* **server and cliend side programming**
	- data processed on the server and displayed on the client
	using html or javascript (interactive objects)
	- web-browsers communicate with web-servers via http
	- browser sends request via http using get, delete or post method 
	and waits for server response
	- body of the response will contain the requested resource (html page, image, etc)

	- on dynamic websites : some part of the response is generated dynamically only when needed

	- most of the site support is run on the server (server-side programming or backend)

	- back and front end languages are typically different except for Javascript

	- client side code - behaviour of the rendered web page
	- server side code - responsible for the page contents
	- cliend side code - written in HTML, CSS, Javascript, run by browser and has little access to the OS resources

	- NodeJS - server-side Javascript framework, other server-side languages: PHP, Ruby, Python, Java, C#
	- typically each language has web-frameworks for server-side web development (Rails, Laravel, Django and Flask); would be too hard to develop http server from scratch

	- server-side return html, javascript or simply json or xml data for the client-side to process and render
	- main task of the server-side code is to get some info in the database and to return it back as a response

	- main difference from desktop - info is stored on the server databases and requests are processed by powerfull servers rather than client PC
	- typical server programming works to processing a large number of requests, while desktop code assumes a single user and pay a lot of attention to GUI experience etc 


* **HTTP**
	- http was designed to enable client-server communication via request-response
	- http methods : most common are GET and POST (but there's also DELETE, PATCH etc)

	- example of GET (use to get data)
	``` /test/demo_form.php?name1=value1&name2=value```
	- POST (used to send data to create/update a resource)
	- both GET and POST can be used for similar purposes, 
	see the comparison here https://www.w3schools.com/tags/ref_httpmethods.asp
	- in particular, GET has data length restriction while POST does not
	- Both GET and POST method is used to transfer data from client to server in HTTP protocol but GET carries request parameter appended in URL string while POST carries request parameter in message body (a more secure way of transferring data from client to server in http protocol).

	- request returns the code signifying success or different types of errors (response status)

	- response can be in json (common for http APIs) or a HTML (if get is applied to a simple web-page)

	- what server sends to the client to help render the page:
		* HTML - main content of the page
		* CSS - page styling
		* JS - page interactivity
		* images

* **HTML**
	- <html> ... </html> : example of a tag
	- some info is stored inside tag box (may contain other tags)
	- there are page head and body tags
	- paragraph tag denoted by p
	- tags form a tag tree
	- tag can contain hyperlink (```a``` tag is used for it) 
	```<a href="https://www.python.org">Python</a> </p>```
	- a and p are very common html tags
	- other common tags:
		* b - bold text
		* i - italic text
		* div - division or area on the page
		* table - creates a table
		* form - input form
	- inside <..> a tag may have properties (like href for a tag)
	- properties useful for web-scrapping are ```class``` and ```id```
		* one element (tag) can have multiple classes, and a class can be shared between elements; each element can only have one id, and an id can only be used once on a page
		* classes and ids are optional
	- python requests library is used to download the page html content
	- class and id are used by CSS to determine which style to apply

	- web-page check is done using Chrome devtools
		* Ctrl+Shift+C to open page devtools

* **Python web-scrapping**
	- commonly used libs are beautiful-soup, selenium and scrapy
	- *beautiful soup*
		* simple and efficient for quick extraction of some website data
		* needs other libs to download the page (e.g. requests)
		and to parse the selected HTML or XML element (e.g. using lxml parser for 
		XML and HTML, available e.g. in pd.read_html etc)

	- *selenium*
		* designed to automate tests for web applications (using Python, Ruby, Java etc)

	- *scrapy* - serious library for web-scraping, fast and efficient but harder to learn, 
	best for large complex projects

	- so, beautiful soup and scrapy should cover all of my needs 
















---------------------------------
# questions
- difference of ssh and http, how TCP is related
- 