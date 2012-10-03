!SLIDE

# The ![Play logo](play-logo.png) Framework

<div markdown="1" id="logo">
<img src="ardentex-logo.png"/>
</div>

Brian Clapper

Founder: PHASE

*@bclapper*

*bmc@ardentex.com*

!SLIDE smbullets incremental transition=fade

# Why am I qualified to talk about Play?

* I've been doing Ruby on Rails development for awhile now. I've also done 
  a lot of work with Django. (This _is_ actually relevant.)
* I've done my share of traditional Java web development.
* I'm in the process of becoming a Typesafe-certified Play trainer.
* I've played with Play...

!SLIDE smbullets incremental transition=fade

# Talk Outline

* Overview of Play 2.0
* Demonstration of Sample Application

!SLIDE smbullets incremental transition=fade

# What is Play?

## Play, version 2 is:

* a modern, _lightweight_ MVC web framework
* conceptually similar to Ruby on Rails, Grails, and Django
* _productive_. (I'll explain that shortly.)
* _fast_.
* _stateless_.
* _type safe_ (unlike Rails, Grails or Django).

!SLIDE smbullets incremental transition=fade

# MVC: Quick review

* MVC: Model, View, Controller
* Common web architecture. Used by Spring, Rails, Grails, many others
* Model = Layer that interacts with data store, contains business logic
* View = Templates
* Controller = Interacts with models, renders templates

!SLIDE smbullets incremental transition=fade

# Lightweight

* Bundled with its own HTTP server. No external container (e.g., Tomcat)
  is required.
* No deployment necessary _at all_ during development.
* _Run your code right where you edit it._
* Web API is less abstract, more HTTP-aware (than, for instance, Java Servlets)
* No XML configuration, in most cases. (Yay!)

!SLIDE smbullets incremental transition=fade

# Productive

* During development, Play automatically recompiles templates and code whenever
  you change them.
* No more _compile, test, deploy_.
* Just change the code, and refresh your browser.
* Rails, Grails and Django all work this way, too.

!SLIDE smbullets incremental transition=fade

# Fast

* Non-blocking, event-driven, NIO-based architecture
* Bundled with JBoss Netty
* Asynchronicity is built right in
* Native support for Akka, allowing easy implementation of highly distributed
  systems

!SLIDE smbullets incremental transition=fade

# Type Safe

* An unusual trait, in these kinds of frameworks
* Models and controllers are compiled to byte code (of course)...
* ...but _so are the templates_.
* Nice by-product:
  * Change the name of a field in a model
  * Reload browser
  * Templates are recompiled
  * Templates that used the old field name are flagged automatically,
    _at compile-time_

!SLIDE smbullets incremental transition=fade

# Deployment

* Also lightweight.
* No WAR file necessary for deployment.
* No additional container required, because Play is bundled with Netty.
* Can deploy the directory, as is, as long as Play is installed on server.
* Play can bundle up a self-contained zip file with all necessary components.
* There's a plug-in to generate a WAR file, if you **must** have one.

!SLIDE smbullets incremental transition=fade

# Bundled Technologies

* Javascript and CoffeeScript
* CSS and LESS (LESS is compiled on the back end)
* jQuery
* Twitter Bootstrap helpers

!SLIDE smbullets incremental transition=fade

# Getting started

* Follow the installation instructions on the web site.
* Then, use Play to generate a new application.

!SLIDE smbullets incremental transition=fade

# Getting started

    $ play new myapp
           _            _ 
     _ __ | | __ _ _  _| |
    | '_ \| |/ _' | || |_|
    |  __/|_|\____|\__ (_)
    |_|            |__/ 
                 
    play! 2.0.4-RC2, http://www.playframework.org
    
    The new application will be created in
    /home/bmc/src/mystuff/play/myapp
    
    What is the application name? 
    > myapp

    Which template do you want to use for this new application? 

      1 - Create a simple Scala application
      2 - Create a simple Java application
      3 - Create an empty project

    > 1

    OK, application myapp is created.

    Have fun!

!SLIDE bullets incremental transition=fade

# Default Application Layout

    $ tree myapp

    myapp
    ├── app
    │   ├── controllers
    │   │   └── Application.java
    │   └── views
    │       ├── index.scala.html
    │       └── main.scala.html
    ├── conf
    │   ├── application.conf
    │   └── routes
    ├── project
    │   ├── build.properties
    │   ├── Build.scala
    │   └── plugins.sbt
    ├── public
    │   ├── images
    │   │   └── favicon.png
    │   ├── javascripts
    │   │   └── jquery-1.7.1.min.js
    │   └── stylesheets
    │       └── main.css
    └── README
    
    9 directories, 12 files

!SLIDE smbullets incremental transition=fade

# My Usual Layout

I usually add the following directories, as well:

    myapp
    ├── app
    │   ├── assets
    │   │   ├── javascripts
    │   │   │   └── bootstrap
    │   │   │        └── ...
    │   │   └── stylesheets
    │   │       ├── main.less
    │   │       └── bootstrap
    │   │            └── ...
    │   ├── models
    │   ├── controllers
    │   ├── views

!SLIDE smbullets incremental transition=fade

# Models

* Play doesn't really care how you implement your models.
* They can be static.
* They can use an ORM.
* They can manufacture random objects out of thin air.
* Play _does_ come with out-of-the-box support for databases, however.

!SLIDE smbullets incremental transition=fade

# Models: Scala

* Play 2.0.x for Scala ships with Anorm: thin layer over raw SQL.
* Has the advantages of direct SQL:
  * Close to the actual database
  * No intervening ORM language to learn
* Has all the disadvantages, too:
  * Potentially RDBMS-specific
  * Can be fragile and _really_ ugly
* You can use other database APIs (e.g., ScalaQuery, Squeryl)
* Play 2.1.x will ship with Typesafe Slick, not Anorm

!SLIDE smbullets incremental transition=fade

# Models: Java

* Play 2.0.x for Java uses EBean, by default
* EBean supports JPA annotations
* True JPA support is available, as well

!SLIDE smbullets incremental transition=fade

# Controllers

A simple "hello, world" controller, in Java:

    @@@ java
    public class MyApp extends Controller {
        public static Result index() {
            return ok("Hello, world!")
        }

In Scala:

    @@@ scala
    object Application extends Controller {
      def index() = Action {
        Ok("Hello, world!")
      }
    }

!SLIDE smbullets incremental transition=fade

# Controllers

There are other action verbs, besides `ok`. Examples, in Java:

* `notFound`
* `badRequest`
* `status`
* `internalServerError`
* `redirect`
* These all map pretty closely to HTTP status codes

!SLIDE smbullets incremental transition=fade

# Controllers

With a redirect, in Java:

    @@@ java
    public class MyApp extends Controller {
        public static Result index() {
            return redirect(controllers.routes.MainController.index());
        }

In Scala:

    @@@ scala
    object Application extends Controller {
      def index() = Action {
        Redirect(routes.MainController.index)
      }
    }

!SLIDE smbullets incremental transition=fade

# Controllers

Now, with template-rendering goodness. In Java:

    @@@ java
    public class MyApp extends Controller {
        public static Result index() {
            return ok(index.render());
        }

In Scala:

    @@@ scala
    object Application extends Controller {
      def index() = Action {
        Ok(views.html.index());
      }
    }

!SLIDE smbullets incremental transition=fade

# Routes? WTF are those?

* Routes define mappings between an incoming URL path and a controller
* If you're used to Tomcat, you're used to specifying these things in some
  ugly XML file.
* ... and they're not very flexible.

!SLIDE smbullets incremental transition=fade

# Routes? WTF are those?

* In Play, route mapping is done in a simple text file, `conf/routes`
* The `routes` file is converted to code and compiled.
* A "reverse route" source file is also produced.
* Reverse routes allow programmatic access to URLs, without hardcoding.
* e.g.:
  * `controllers.routes.MainController.index()` (Java)
  * `routes.MainController.index` (Scala)

!SLIDE

# Sample route file

    @@@ text
    GET     /                    controllers.Application.index

    POST    /sign-in             controllers.Auth.authenticate
    GET     /login               controllers.Auth.login
    GET     /logout              controllers.Auth.logout

    GET     /sites               controllers.SiteController.index
    POST    /sites/list          controllers.SiteController.list
    GET     /site/new            controllers.SiteController.makeNew
    POST    /site/create         controllers.SiteController.create
    GET     /site/:id/edit       controllers.SiteController.edit(id: Long)
    GET     /site/$id<\d+>       controllers.SiteController.show(id: Long)
    GET     /site/$id<\d+>/json  controllers.SiteController.showJSON(id: Long)
    POST    /site/$id<\d+>       controllers.SiteController.update(id: Long)
    GET     /sites/download      controllers.SiteController.download

    # Assumes that "q" is passed as a query string parameter.
    GET     /site/search         controllers.SiteController.search(q)

    POST    /site/:id/delete     controllers.SiteController.delete(id: Long)

!SLIDE smbullets incremental transition=fade

# Templates

* Templates are HTML files, with snippets of Scala code
* A template _always_ starts with a parameter list
* To pass objects to a template, you pass them as parameters

!SLIDE

# Simple template

    @@@ html
    @(currentUser: User)

    @main("You've logged in!", currentUser) {
      <div class="todo-items">
        Your to-do items follow.
        <ul>
          @for(item <- currentUer.toDoItems) {
            <li>@item.text()</li>
          }
        </ul>
      </div>
    }

!SLIDE

# Simple template (2)

Main template (in `views/main.scala.html`):

    @@@ html
    @(title: String, currentUser: User)(content: Html)

    <!DOCTYPE html>
    <html lang="en">
      <head>
        <title>@title</title>
      </head>
      <body>
        ...
        <div id="content">
          @content
        </div>
      </body>
    </html>

!SLIDE smbullets incremental transition=fade

# Let's see an example

(demonstration of sample application)

!SLIDE smbullets incremental transition=fade

# For more information

* This presentation will be posted on my web site, _www.ardentex.com_
* The code for the *PasswordThing* demo application is in my GitHub repo,
  at `https://github.com/bmc/passwordthing-scala`
* Once I've finished converting the Scala version to Java, you'll find
  a Java version of the demo application at
  `https://github.com/bmc/passwordthing-java`

!SLIDE smbullets incremental transition=fade

# For more information

* Play Framework: _www.playframework.org_
* Manning has two Play books, both in early access:
  * _Play for Scala_: http://www.manning.com/hilton/
  * _Play for Java_: http://www.manning.com/leroux/
* Stack Overflow is also a good resource for answers to Play questions.

!SLIDE smbullets incremental transition=fade

# Speaking of questions

Are there any?
