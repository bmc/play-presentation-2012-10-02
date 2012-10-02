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

# What is Play?

* Play is a modern, _lightweight_ MVC web framework
* Play is conceptually similar to Ruby on Rails, Grails, and Django
* Play is _iterative_. (I'll explain that shortly.)
* Play is _type safe_ (unlike Rails, Grails or Django).
* Play is _stateless_.
* Play is _fast_.

!SLIDE smbullets incremental transition=fade

# MVC: Quick review

* MVC: Model, View, Controller
* Common web architecture. Used by Spring, Rails, Grails, many others
* Model = Layer that interacts with data store, contains business logic
* View = Templates
* Controller = Interacts with models, renders templates

!SLIDE smbullets incremental transition=fade

# Lightweight

* Bundled with Netty. No external container (e.g., Tomcat) required.
* No deployment necessary _at all_ during development.
* _Run your code right where you edit it._
* No WAR file necessary for deployment.
* _Can deploy the directory, as is, as long as Play is installed on server._
* _Play can bundle up a self-contained zip file with all necessary components._
* _There's a plug-in to generate a WAR file, if you **must** have one._

!SLIDE smbullets incremental transition=fade

# Iterative

* During development, Play automatically recompiles templates and code whenever
  you change them.
* No more _compile, test, deploy_.
* Just change the code, and refresh your browser.

!SLIDE smbullets incremental transition=fade

!SLIDE smbullets incremental transition=fade

!SLIDE smbullets incremental transition=fade


