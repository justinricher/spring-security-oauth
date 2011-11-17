# Tutorial

## Introduction

There's a good [getting started guide](http://www.hueniverse.com/hueniverse/2007/10/beginners-gui-1.html) that illustrates OAuth
1.0 by describing two different (but related) services.  One is a photo-sharing application.  The other is a photo-printing
application.  In OAuth terms, the photo sharing application is the OAuth _provider_ and the photo printing application
is the OAuth _consumer_ or _client_.

For this tutorial, we will see OAuth for Spring Security in action by deploying a photo-sharing application and a
photo-printing application on our local machine.  We'll name the photo-sharing application "Sparklr" and the
photo-printing application "Tonr".  A user named "Marissa" (who has an account at both Sparkr and Tonr) will use Tonr
to access her photos on Sparklr without ever giving Tonr her credentials to Sparklr.

There is a Sparklr application for both OAuth 1.0 and for OAuth 2.0, likewise Tonr. Download the pair for the spec that you'd like to to see
in action:

OAuth 1.0|OAuth 2.0
---------|---------
[Sparklr 1](http://static.springsource.org/spring-security/oauth/sparklr.zip) | [Sparklr 2](http://static.springsource.org/spring-security/oauth/sparklr2.zip)
[Tonr 1](http://static.springsource.org/spring-security/oauth/tonr.zip) | [Tonr 2](http://static.springsource.org/spring-security/oauth/tonr2.zip)

Each application is a standard [Maven](http://maven.apache.org/) project, so you will need Maven installed. Each application
is a standard Spring MVC application with Spring Security integrated. Presumably, you're familiar with Spring and Spring Security so
the configuration files will look familiar to you.

## Setup

Unzip the Sparklr and Tonr applications, and take a look around. Note especially the Spring configuration files in `src/main/webapp/WEB-INF`.
  
For Sparklr, you'll notice the definition of the OAuth provider mechanism and the consumer/client details along with the
[standard spring security configuration](http://static.springsource.org/spring-security/site/docs/3.0.x/reference/ns-config.html) elements.  For Tonr,
you'll notice the definition of the OAuth consumer/client mechanism and the resource details.  For more information about the necessary
components of an OAuth provider and consumer, see the [[developers guide|devguide]].

You'll also notice the Spring Security filter chain in `applicationContext.xml` and how it's configured for OAuth support.

### Deploy Sparklr

```
cd sparklr
mvn jetty:run
```

Sparklr should be started on port 8080.  Go ahead and browse to [http;//localhost:8080/sparklr](http;//localhost:8080/sparklr). Note the basic
login page and the page that can be used to browse Marissa's photos. Logout to ensure Marissa's session is no longer valid.  (Of course,
the logout isn't mandatory; an active Sparklr session will simply bypass the step that prompts for Marissa's credentials before
confirming authorization for Marissa's protected resources.)

### Start Tonr.

```
cd tonr
mvn jetty:run
```

Tonr should be started on port 8888.  Browse to [http://localhost:8888/tonr](http://localhost:8888/tonr). Note Tonr's home page.

### Observe...

Now that you've got both applications deployed, you're ready to observe OAuth in action.

1. Login to Tonr.

   Marissa's credentials are already hardcoded into the login form.

2. Click to view Marissa's Sparklr photos.

   You will be redirected to the Sparklr site where you will be prompted for Marissa's credentials.

3. Login to Sparklr.

   Upon successful login, you will be prompted with a confirmation screen to authorize access to Tonr
   for Marissa's pictures.
    
4. Click "authorize".
  
   Upon authorization, you should be redirected back to Tonr where Marissa's Sparklr photos are displayed
   (presumably to be printed).
