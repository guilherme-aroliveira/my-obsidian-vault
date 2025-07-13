Flask is a [[Computer Science/Programming/Python]] <strong style="color: #d79921">web micro-framework</strong> with minimal to no dependence on external libraries that can create web applications. Flask is a very light framework, while Django is a full-stack framework.

It was created in 2004 by Armin Ronacher as an April fool's joke.

Flask only provides the basic dependencies needed to create a web application, and it does not bind the user to a specific set of tools.

The developer can choose other extensions that provide additional features.

Flask is not opinionated about what database or template engine to use, it is a good choice for RESTful APIs
###### <strong style="color: #689d6a">Features</strong>

Flask has a built-in web server that runs applications in development mode, a built-in unit testing and also has has a debugger to help debug applications.

It uses standard Python logging for application logs

enables request and response classes
enables exposure to python functions as APIs

provides static asset support like CSS files, JavaScript files, and images.
Flask provides tags to load static files in the templates.

ou can also develop dynamic pages using Jinja templating framework and  these dynamic pages can display information that may change for each request or may check if the user is logged in.

Flask supports CRUD requests by making Post, Put, Get, Update, and Delete requests

Flask provides routing and supports dynamic URLs that are extremely useful for RESTful services, you can create routes for different HTTP methods and  provide redirection in your application

it supports user session management. Some of the popular community extensions that can be added to your application are the following: Slask-SAL

To build websites, Flask has features like debugging servers,  routing, templates, and error handling.
###### <strong style="color: #689d6a">Extensions</strong>

- Flask-SQLAlchemy --> add support for ORM (SQLAlchemy to Flask)
- Flask-Mail --> set up an SMTP mail serve
- Flask-Admin --> add admin interfaces
- Flask-CORS
- Flask-Migrate --> adds database migrations
- Flask-User --> management activities (e.g. user authentication)
- Marshmallow --> adds object serialization and deserialization
- Celery --> task queue
###### <strong style="color: #689d6a">Built-in dependencies</strong>

- Werkzeug: implements web server gateway interface (WSGI)
- Jinja: Template language --> way to evalute functions as python 
- MarkupSafe: Provides security features in templates
- ItsDangerous: Signing library for session cookies
- Click: framework for writing command-line applications
###### <strong style="color: #c6554f">Set up</strong>

<span style="color:#98971a">Python virtual environment</span> (recommended)
- `python3 -m venv .venv`
- `source ./venv/bin/activate`

<span style="color:#98971a">Install Flask</span>
- `pip install Flask==2.2.2`
- `flask -app <filename> run` --> run flask
	- `--debug` --> to run in debug mode

<span style="color:#98971a">Flask Dependencies</span>
- `pip freeze` <span style="color: #3588E9">--></span>  see the built-in dependencies
- use the pip freeze command in the virtual environment
###### <strong style="color: #c6554f">Workflow</strong>

<strong style="color:#98971a">Create a Server - app.py</strong>

>[!example] Example - server
>```python
># import modules
>from flask import Flask
>
># instantiate an object of the Flask class as the app
>app = Flask(__name__) # object of the Flask class
>```
>Obs: most applications use the reference name "app" for clarity purposes. This name is used to find resources on the filesystem and by extensions to provide debugging information.

<strong style="color:#98971a">Adding routes</strong>

>[!example] Example - Route
>```python
>@app.route('/') # route
>
># method that will be invoked when this route is accessed.
>def hello_world():
>	return "<b>My first Flask application in action!</b>"
>```
>When a request it not specified, by default, Get is requested

<strong style="color:#98971a">Add a condition</strong>

>[!example] Example - condition
>```python
>if __name__ = "__main__":
>	app.run(debug=True)
>```
>By default "__name__" is set to "__main__" unless it is explicitly changed

<strong style="color:#98971a">Running Flask</strong>

>[!example]
>```python
># Export settings (system environment variables)
>
>export FLASK_APP=app.py
>export FLASK_ENV=development # deprecated in Flask 2.3
>```
>---
>```shell
>$ flask run
>$ flask --app server --debug run
>```
>`--app`: identifies the Python file to run
>`--debug`: start the debug mode <span style="color: #3588E9">--></span> automatic restarts in file change
>```shell
>$ python3 app.py
>```
>

<strong style="color:#98971a">Returning JSON</strong>

>[!example]
>```python
>@app.route('/')
>def index():
>	return {"message": "Hello World"}
>```
>To return a more complex object like a class, ensure that it can be serialized
>```python
>@app.route('/')
>def index():
>	return jsonify{message="Hello World"}
>```
###### <strong style="color: #d79921">Decorators</strong>

The decorator takes the path as an argument. It can return text or HTML from the method.

`@app` --> used to define a route.

`@app.route` --> used to create URL handlers
- it provides to assign URLs in the app to functions easily
- also take `method` as a second parameter, which can be set to the type of HTTP methods, the route will support.
- The route decorator can also be more specific --> `@app.route("/userdetails/<userid>")`

`@app.route("/")` --> map root URL

`@app.errorhandler` -->
###### <strong style="color: #d79921">Dynamic Routes</strong>

Dynamic routes can be used to create RESTful endpoints.

<strong style="color:#98971a">Callint external APIs</strong>

To call an external API in Flask, the easiest way is to use the Python requests library.

>[!example]
>```python
>from flask import Flask, escape 
>import requests
>
>app = Flask(__name__)
>
>@app.route("/")
>def get_author():
>	res = requests.get("https://openlibrary.org/search/authors.JSON?q=Michael Crichton")
>	if res.status_code == 200:
>		return {"message": res.JSON()}
>	elif res.status_code == 400:
>		return {"message": "Something wen wrong!"}, 404
>	else:
>		return {"message": "Server error!"}, 500
>```
>Return JSON as a dictionary to the caller.

<strong style="color:#98971a">Parameters</strong>

RESTful API requires resource ID in the URL

>[!example] Example - Dynamic routing
>```python
>@app.route("/book/isbn")
>def get_author(isbn):
>	res = requests.get("https://openlibrary.org/isbn/{escape(isbn)}.JSON")
>	
>	if res.status_code == 200:
>		return {"message": res.JSON()}
>	elif res.status_code == 400:
>		return {"message": "Something wen wrong!"}, 404
>```
>This example creates an endpoint that returns book information by International Standard Book Number (ISBN), but instead of hard coding the ISBN, the client send it as part of the URL.

Flask  also allows to set the parameter type. The framework uses this information to validate incoming requests. Example: create an endpoint of terminals and SFO to get the number of terminals at the San Francisco airport.
- `@app.route("terminal/<string:airport_code">)` --> triggers if the user sends a string at the end of the URL
Mime type --> browsers use it to determine how to process a URL, it looks to the content-type.
multipurpose internet mail extensions 

Parameter Types:
- string --> any String
- int --> `/person/<int:age_min>`
- float --> `/person/`
- path --> indicate a web path or a folder path `/main/test/sub`
- uuid --> indicate a unique id like GUID `/network/<uuid:uuid>`

Globally Unique Identifier 
###### <strong style="color: #d79921">Error Handling</strong>

Every HTTP response contains a three-digit code indicating different error and success status.

<span style="color:#98971a">Returning status (implicit):</span>

Flask automatically returns 200 by default when a string or dict is returned

200 also returned when `jsonify()` is used


>[!example]
>```python
>from flask import Flask, escape
>import requests
>
>app = Flask(__name__)
>@app.route('/'):
>def hello_world():
>	return "<b> My first Flask application in action! </b>"
>```

<span style="color:#98971a">Returning status (explicity):</span>

Return tuple with response as first value and status as the second value:

>[!example]
>```python
>@app.route('/')
>def hello_world():
>	return ("<b> My first Flask application in action! </b>", 200)
>```

use the `make_reponse()` to explicitly set the status code:

>[!example]
>```python
>@app.route('/')
>def hello_world():
>	res = make_response("<b> My first Flask application in action! </b>")
>	res.status_code = 200
>	return res
>```

<span style="color:#98971a">Returning error code:</span>

The application needs to return the appropriate code

>[!example]
>```python
>@app.route('/')
>def search_reponse():
>	query = request.args.get("q")
>
>	if not query:
>		return {"error_message": "Input parameter missing"}, 422
>
>	# fetch the resouce from the database
>	resource = fetch_from_database(query)
>	
>	if resource:
>		return: {"message":" resource"}
>	else:
>		return {"error_message": "Resource not found"}, 404
>```

Resource found: `curl -X GET -i http://localhost:5000?q=Resource777`

Resource Not Found: `curl -X GET -i http://localhost:5000?q=Resource888`
###### <strong style="color: #689d6a">Tips</strong>

It is recommended to pin the version number of the dependencies in the application. This ensures that the application can be reproduced from scratch in different environments.

The Requests library is designed to simplify the process of sending HTTP requests.

UUID stand for Universal Unique Identifier.

The Flask application is run by default on port 5000

`render_template()` --> function that comes with flask, it allows to send html files. 

`url_for('static', filename='style.css')` --> allow to pass static files

<strong style="color:#98971a">Return JSON from the application:</strong>

>[!example] Example - serializable obect
>```python
>@app.route('/') 
>def index():
>	return {"message": "Hello World"}
>```
>Test the app:
>```shell
>$ curl -X GET -i localhost:5000
>```

>[!example] Example - `jsonify()` method
>```python
>from flask import Flask, jsonify
>app = Flask(__name__)
>
>@app.route('/')
>def index():
>	# Pass key-value pairs
>	return jsonify(message="Hello World") 
>```

<strong style="color:#98971a">To check if the current sctipt is the main program:</strong>

>[!example]
>```python
># Run the Flask app
>if __name__ == "__main__":
>	# start the Flask development server with debug mode enabled
>	app.run(debug=True)
>```
>The "debug mode" allow to view detailed error messages in the browser if something goes wrong
##### <strong style="color: #c6554f">Application</strong>

###### <strong style="color: #d79921">Setup</strong>

<span style="color:#98971a">Custom routes</span>

`@app.route("/path")` --> defaults to the GET method

use <strong>methods</strong> argument to only allow specific HTTP methods

>[!example]
>```python
>@app.route("/health")
>def health():
>	return jsonify(dict(status="OK")), 200
>```
>---
>```python
>@app.route("/health", methods=["GET", "POST"]) 
>def health():
>	if request.method == "GET": return jsonify(status="OK", method="GET"), 200
>	if request.method == "POST": return jsonify(status="OK", method="POST"), 200
>```

<span style="color:#98971a">Request Object</span>

All HTTP calls to Flask contain the request object created from the Flask.Request class.

- Common attributes:
	- server address --> in the form of a tuple, host, port
	- headers
	- URL --> resource asked by request
	- access_route --> lists all the IP addresses for requests that are forwarded multiple times
	- full_path --> complete path of the request, including any query string
	- is_secure --> true if a client makes a request using HTTPS or WSS protocol
	- is_JSON --> true if the request contains JSON data
	- Cookies dict --> contains any cookies sent with the request
- Data from the header:
	- Cache-Control: holds information on how to cache in browsers
	- Accept: informs the browser what kind of content type is understood by the client
	- Accept-Encoding: indicates the code content
	- User-Agent: identifies the client, application, operating system, or version
	- Accept-Language: requests for a specific language and locale
	- Host: specifies the host and port number of the requested server
- Methods:
	- `get_data` --> Get POST data from the request as bytes
	- `get_JSON` --> Parses POST data from the request as JSON
- Parsed data:
	- args: MultiDict[str, str] --> gives query parameters as a dictionary
	- JSON: Optional[Any] --> parse the data into a dictionary
	- files: ImutableMultiDict[str, FileStorage] --> provides user uploaded file
	- form: ImutableMultiDict[str, str] --> contains all values posted in a form submission
	- values: CombinedMultiDict[str, str] --> combine the args data with the form data

Access values:

It's possible to get values from `MultiDit`, `ImmutableMultiDic` and `CombinedMultiDict` as from a Python Dictionary using indexing or the GET method.

>[!example]
>```python
>from flask import Flask, request
>app = Flask(__name__)
>
>@app.route('/')
>def hello_world():
>	course = request.args["course"]
>	rating = request.args.get["rating"]
>	return {"message": f"{course} with rating {rating}"}
>```

<span style="color:#98971a">Response Object</span>

- Common Attributes:
	- status_code indicates the success or failure of the request
	- headers give more information about the response
	- content_type shows the media type of the requested resource
	- content_length is the size of the response message body
	- content_encoding indicates any encoding applied to the response
	- mime-type sets the media type of the response
	- expires contains the date or time after which the response is considered expired
- Common Methods:
	- `set_cookie` --> sets a browser cookie on the client
	- `delete_cookie` --> deletes a cookie on the client
- Usage:
	- success reponse from `@app.route` method
	- `JSONify()` --> creates a Response object automatically
	- `make_response()` --> create a custom response
	- `redirect()` --> return a 302 status-code and redirect the client to another URL
	- `abort ()` --> return a response with an error condition
###### <strong style="color: #d79921">Configurations</strong>

<span style="color:#98971a">Options:</span>
- ENV – Indicates the environment
- DEBUG – enables the debug mode
- TESTING – enables the testing mode
- SECRET_KEY – used to sign the session cookie
- SESSION_COOKIE_NAME – the name of the session cookie
- SERVER_NAME – binds the host and port
- JSONIFY – defaults to 'application/JSON.'

<span style="color:#98971a">Loading configuration:</span>
- config object
	- `app.config['SECRET_KEY'] = "random-secret-key"`
- environment variable
	- `app.config["VARIABLE_NAME"]`
	- `app.config.from_prefixed_env()`
- python file
	- `app.config.from_file("path_to_config_file)`
###### <strong style="color: #d79921">Structure</strong>

>[!example] Example - directory structure
>```text
>+-- config.json
>+-- setup.py
>+-- src
>|   +-- static
>|   |   +-- css
>|   |       +-- main.css
>|   +-- templates
>|       +-- index.html
>+-- tests
>|    +-- test_site.py
>+-- venv
>```
>By default, the Flask application looks for the templates in a directory called templates under the root directory

- module directory --> main source code
- configuration file
- static --> image, CSS and JS.
- templates --> dinamic content
- venv --> virtual environment

The dynamic pages usually have information that is filled in dynamically for each request, these pages are often based on the values passed as arguments. The arguments can either be passed through the URL or be passed as request parameters.