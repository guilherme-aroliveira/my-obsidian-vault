# What is Flask

Is a [[Python]] <strong style="color: #d79921">web micro-framework</strong> with minimal to no dependence on external libraries that can create web applications. Flask is a very light framework, while Django is a full-stack framework.

Flask only provides the basic dependencies needed to create a web application.

--> does not bind the user to a specific set of tools.

Created in 2004 by Armin Ronacher as an April fool's joke.

##### Features

built-in web server that runs applications in development mode
has a debugger to help debug applications
uses standard Python logging for application logs
has built-in unit testing
enables request and response classes
enables exposure to python functions as APIs

provides static asset support like CSS files, JavaScript files, and images.
Flask provides tags to load static files in the templates.

The developer can choose other extensions that provide additional features.

ou can also develop dynamic pages using Jinja templating framework and  these dynamic pages can display information that may change for each request or may check if the user is logged in.

Flask supports CRUD requests by making Post, Put, Get, Update, and Delete requests

Flask provides routing and supports dynamic URLs that are extremely useful for RESTful services, you can create routes for different HTTP methods and  provide redirection in your application

Flask is not opinionated about what database or template engine to use, it is a good choice for RESTful APIs

it supports user session management. Some of the popular community extensions that can be added to your application are the following: Slask-SAL

To build websites, Flask has features like debugging servers,  routing, templates, and error handling.
###### Extensions

Flask-SQLAlchemy --> add support for ORM (SQLAlchemy to Flask)
		- Flask-Mail --> set up an SMTP mail serve
		- Flask-Admin --> add admin interfaces
		- Flask-CORS
		- Flask-Migrate --> adds database migrations
		- Flask-User --> management activities (e.g. user authentication)
		- Marshmallow --> adds object serialization and deserialization
		- Celery --> task queue

###### Built-in dependencies

Werkzeug: implements web server gateway interface (WSGI)
		- Jinja: Template language
		- MarkupSafe: Provides security features in templates
		- ItsDangerous: Signing library for session cookies
		- Click: framework for writing command-line applications
##### Set up 

- Python virtual environment (recommended)
	- `python3 -m venv venv`
	- `source ./venv/bin/activate`
- Install Flask
	- `pip install Flask==2.2.2`
- Fask Dependencies
	- pip freeze -->  see the built-in dependencies
	- use the pip freeze command in the virtual environment,
##### Workflow

**Create a Server - app.py**

```python
# import modules
from flask import Flask 

# instantiate an object of the Flask class as the app
app = Flask(__name__) # object of the Flask class
```

This name is used to find the resources on the file system and by extensions to provide debugging information

>  Obs: most applications use the reference name "app" for clarity purposes. This name is used to find resources on the filesystem and by extensions to provide debugging information.

**Adding routes**

```python
@app.route('/') # route

# method that will be invoked when this route is accessed.
def hello_world():
	return "<b>My first Flask application in action!</b>"
```

> Note: When a request it not specified, by default, Get is requested

**Add a condition**

```python
if __name__ = "__main__":
	app.run(debug=True)
```

> By default "__name__" is set to "__main__" unless it is explicitly changed

**Running Flask**

```python
# Export settings (system environment variables)

export FLASK_APP=app.py
export FLASK_ENV=developmet # deprecated in Flask 2.3
```

- Three ways to run the Flask app
	- `$ flask run`
	- `$ flask --app server --debug run`
		- `--app`: identifies the Python file to run
		- `--debug`: start the debug mode.
			- automatic restarts in file change
	- `python3 <app.py>`
Browse to `http://localhost:5000`

Returnin Json

```python
@app.route('/')
def index():
	return {"message": "Hello WWorld"}
```

If you return a more complex object like a class, ensure that it can be serialized

```python
@app.route('/')
def index():
	return jsonify{message="Hello WWorld"}
```

configuration options

##### Decorators

`@app` --> used to define a route.

The decorator takes the path as an argument. It can return text or HTML from the method.

`@app.route` --> used to create URL handlers
 it provides to assign URLs in the app to functions easily
			- also take `method` as a second parameter, which can be set to the type of HTTP methods, the route will support.
			- The route decorator can also be more specific --> `@app.route("/userdetails/<userid>")`
@app.route("/") --> map root URL.
`@app.errorhandler` -->
##### Dynamic Routes

Dynamic routes can be used to create RESTful endpoints.

Callint external APIs:

To call an external API in Flask, the easiest way is to use the Python requests library.

Return JSON as a dictionary to the caller.

```python
from flask import Flask, escape 
import requests

app = Flask(__name__)

@app.route("/")
def get_author():
    res = requests.get("https://openlibrary.org/search/authors.JSON?q=Michael Crichton")
    if res.status_code == 200:
      return {"message": res.JSON()}
    elif res.status_code == 400:
      return {"message": "Something wen wrong!"}, 404
    else:
      return {"message": "Server error!"}, 500
```


##### Error Handling
## Tips



- <strong style="color: red">Framework</strong>
	- ==Dynamic Routes==
	  collapsed:: true
		- Dynamic routes can be used to create RESTful endpoints.
		- Callint external APIs:
		  id:: 66148dc6-e9ca-4409-add7-bdb055bb526f
		  collapsed:: true
			- To call an external API in Flask, the easiest way is to use the Python requests library.
			- Return JSON as a dictionary to the caller.
			- ```python
			  from flask import Flask, escape 
			  import requests
			  
			  app = Flask(__name__)
			  
			  @app.route("/")
			  def get_author():
			      res = requests.get("https://openlibrary.org/search/authors.JSON?q=Michael Crichton")
			      if res.status_code == 200:
			        return {"message": res.JSON()}
			      elif res.status_code == 400:
			        return {"message": "Something wen wrong!"}, 404
			      else:
			        return {"message": "Server error!"}, 500
			  ```
		- Parameters
		  collapsed:: true
			- RESTful API requires resouce ID in the URL
			- Dynamic routing
			- ```python
			  # This example creates an endpoint that returns book information by International Standard Book Number (ISBN), 
			  # but instead of hard coding the ISBN, we want the client to send it as part of the URL.
			  
			  @app.route("/book/<isbn>")
			  def get_author(isbn):
			      res = requests.get("https://openlibrary.org/isbn/{escape(isbn)}.JSON")
			      
			      if res.status_code == 200:
			        return {"message": res.JSON()}
			      elif res.status_code == 400:
			        return {"message": "Something wen wrong!"}, 404
			  ```
			- Flask also allows to set the parameter type. The framework uses this information to validate incoming requests. Example: create an endpoint of terminals and SFO to get the number of terminals at the San Francisco airport.
				- `@app.route("terminal/<string:airport_code">)` --> triggers if the user sends a string at the end of the URL
			- Parameter Types:
				- string --> any String
				- int --> `/person/<int:age_min>`
				- float --> `/person/<float: height_max>`
				- path --> indicate a web path or a folder path `/main/test/sub`
				- uuid --> indicate a unique id like Globally Unique Identifier (GUID) `/network/<uuid:uuid>`
	- ==Error Handling==
	  collapsed:: true
		- Every HTTP response contains a three-digit code indicating different error and success status.
		- Returning status (implicity):
			- Flask automatically returns 200 by default when a string or dict is returned
			- 200 also returned when jsonify() is used
			- ```python
			  from flask import Flask, escape
			  import requests
			  
			  app = Flask(__name__)
			  
			  @app.route('/')
			  def hello_world():
			      return "<b> My first Flask application in action! </b>"
			  ```
		- Returning status (explicity):
			- Return tuple with reponse as first value and status as the second value:
			  collapsed:: true
				- ```python
				  @app.route('/')
				  def hello_world():
				      return ("<b> My first Flask application in action! </b>", 200)
				  ```
			- use the make_reponse() to explicitly set the status code:
			  collapsed:: true
				- ```python
				  @app.route('/')
				  def hello_world():
				      res = make_response("<b> My first Flask application in action! </b>")
				      res.status_code = 200
				      return res
				  ```
		- Returning error code:
			- The application needs to return the appropriate code
				- ```python
				  @app.route('/')
				  def search_reponse():
				      query = request.args.get("q")
				      
				      if not query:
				          return {"error_message": "Input parameter missing"}, 422
				        
				      # fetch the resouce from the database
				      resource = fetch_from_database(query)
				      
				      if resource:
				          return: {"message":" resource"}
				      else:
				          return {"error_message": "Resource not found"}, 404
				  ```
			- Resource found: `curl -X GET -i http://localhost:5000?q=Resource777`
			- Resource Not Found: `curl -X GET -i http://localhost:5000?q=Resource888`
- ==Tips==
  collapsed:: true
	- --> it is recommended to pin the version number of the dependencies in your application. This ensures that the application can be reproduced from scratch in different environments.
	- The Requests library is designed to simplify the process of sending HTTP requests.
	- UUID stand for Universal Unique Identifier.
	- Check for dependencies:
	  collapsed:: true
		- <code>pip freeze</code>
	- The Flask application is run by default on port 5000
	- To pass arguments to the Flask executable:
	  collapsed:: true
		- `$ flask -app app --debug run`
	- Return JSON from the application:
	  collapsed:: true
		- serializable obect:
			- ```python
			  @app.route('/') 
			  def index():
			      return {"message": "Hello World"}
			  ```
			- To test: `$ curl -X GET -i localhost:5000`
		- jsonify() method:
			- ```python
			  from flask import Flask, jsonify
			  app = Flask(__name__)
			  
			  @app.route('/') 
			  def index():
			      return jsonify(message="Hello World") # Pass key-value pairs
			  ```
	- To check if the current sctipt is the main program:
		- ```python
		  # Run the Flask app
		  if __name__ == "__main__":
		      app.run(debug=True) # start the Flask development server with debug mode enabled
		  ```
		  > The "debug mode" allow to view detailed error messages in the browser if something goes wrong
---
- <strong style="color: red">Application</strong>
	- ==Setup==
	  collapsed:: true
		- <span style="color:#98971a">Custom routes</span>`@app.route("/path")` --> defaults to the GET method
			- use <strong>methods</strong> argument to only allow specific HTTP methods
			- ```python
			  @app.route("/health") 
			  
			  def health():
			      return jsonify(dict(status="OK")), 200
			  ```
			- ```python
			  @app.route("/health", methods=["GET", "POST"]) 
			  
			  def health():
			      if request.method == "GET": return jsonify(status="OK", method="GET"), 200 
			    
			      if request.method == "POST": return jsonify(status="OK", method="POST"), 200 
			  ```
		- <span style="color:#98971a">Request Object</span>
		  collapsed:: true
			- All HTTP calls to Flask contain the request object created from the Flask.Request class.
			- Common attributes:
			  collapsed:: true
				- server address --> in the form of a tuple, host, port
				- headers
				- URL --> resource asked by request
				- access_route --> lists all the IP addresses for requests that are forwarded multiple times
				- full_path --> complete path of the request, including any query string
				  id:: 66146d8c-6d3e-4749-91d2-d11efca070f7
				- is_secure --> true if a client makes a request using HTTPS or WSS protocol
				- is_JSON --> true if the request contains JSON data
				- Cookies dict --> contains any cookies sent with the request
			- Data from the header:
			  collapsed:: true
				- Cache-Control: holds information on how to cache in browsers
				- Accept: informs the browser what kind of content type is understood by the client
				- Accept-Encoding: indicates the code content
				- User-Agent: identifies the client, application, operating system, or version
				- Accept-Language: requests for a specific language and locale
				- Host: specifies the host and port number of the requested server
			- Methods:
			  collapsed:: true
				- `get_data` --> Get POST data from the request as bytes
				- `get_JSON` --> Parses POST data from the request as JSON
			- Parsed data:
			  collapsed:: true
				- args: MultiDict[str, str] --> gives query parameters as a dictionary
				- JSON: Optional[Any] --> parse the data into a dictionary
				- files: ImutableMultiDict[str, FileStorage] --> provides user uploaded file
				- form: ImutableMultiDict[str, str] --> contains all values posted in a form submission
				- values: CombinedMultiDict[str, str] --> combine the args data with the form data
			- Access values:
			  collapsed:: true
				- <p>--> it's possible to get values from MultiDit, ImmutableMultiDic and CombinedMultiDict as from a Python Dictionary using indexing or the GET method.</p>
				- ```python
				  from flask import Flask, request
				  app = Flask(__name__)
				  
				  @app.route('/')
				  def hello_world():
				      course = request.args["course"]
				      rating = request.args.get["rating"]
				      return {"message": f"{course} with rating {rating}"}
				  ```
		- <span style="color:#98971a">Response Object</span>
		  collapsed:: true
			- Common Attributes:
				- status_code indicates the success or failure of the request
				- headers give more information about the response
				- content_type shows the media type of the requested resource
				- content_length is the size of the response message body
				- content_encoding indicates any encoding applied to the response
				- mime-type sets the media type of the response
				- expires contains the date or time after which the response is considered expired
			- Common Methods:
			  collapsed:: true
				- `set_cookie` --> sets a browser cookie on the client
				- `delete_cookie` --> deletes a cookie on the client
			- Usage:
			  collapsed:: true
				- success reponse from `@app.route` method
				- `JSONify()` --> creates a Response object automatically
				- `make_response()` --> create a custom response
				- `redirect()` --> return a 302 status-code and redirect the client to another URL
				- `abort ()` --> return a response with an error condition
	- ==Configurations==
	  collapsed:: true
		- Options:
			- ENV – Indicates the environment
			- DEBUG – enables the debug mode
			- TESTING – enables the testing mode
			- SECRET_KEY – used to sign the session cookie
			- SESSION_COOKIE_NAME – the name of the session cookie
			- SERVER_NAME – binds the host and port
			- JSONIFY – defaults to 'application/JSON.'
		- Loading configuration:
		  collapsed:: true
			- config object
				- `app.config['SECRET_KEY'] = "random-secret-key"`
			- environment variable
			  collapsed:: true
				- `app.config["VARIABLE_NAME"]`
				- `app.config.from_prefixed_env()`
			- python file
			  collapsed:: true
				- `app.config.from_file("path_to_config_file)`
	- ==Structure==
	  collapsed:: true
		- Example of directory structure of the application:
		  collapsed:: true
			- <pre>
			  +-- config.json
			  +-- setup.py
			  +-- src
			  |   +-- static
			  |   |   +-- css
			  |   |       +-- main.css        
			  |   +-- templates
			  |       +-- index.html
			  +-- tests
			  |    +-- test_site.py
			  +-- venv     
			  </pre>
			  > By default, the Flask application looks for the templates in a directory called templates under the root directory
			- module direcory --> main source code
			- configuration file
			- static --> image, CSS and JS.
			- templates --> dinamic content
			- venv --> virtual environment
		- Web app structure:
			- CREATE -->
			- READ -->
			- UPDATE -->
			- DELETE -->
		- The dynamic pages usually have information that is filled in dynamically for each request, these pages are often based on the values passed as arguments. The arguments can either be passed through the URL or be passed as request parameters.