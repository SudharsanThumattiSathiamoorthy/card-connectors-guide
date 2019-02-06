Deploying a Mobile Flows Connector is not too different from deploying any other public facing service.  Here we will detail the general requirements and provide an example.


## General Deployment Requirements

Connectors can be written in any language (if you write one in [MUMPS](http://mumps.sourceforge.net/docs.html) we would love to see it), and a variety of deployment methods/tools can be selected.  We will not attempt to go over all of the options for deployment.  Instead, we will discuss the general requirements and follow this up with a step-by-step example in which we *will* use specific deployment tools.


A deployed connector requires the following:

* HTTPS Connections *only*
* Publicly Available and Reasonable Connectivity
* Awareness of external host and protocol.

### HTTPS

Data between Connectors and Mobile Flows Platform will generally be sensitive data.  Connector configuration in Unified Endpoint Management will *require* HTTPS protocols in any URLs.


All connector URLs *should* use the HTTPS protocol. This includes any URL that will be used to call back into the connector: API exposed in discovery, URLs embedded in connector responses for action resolution, etc.

### Host and Protocol

It is important that connectors are able to correctly build URLs for calling back into the connector.  We want to avoid a situation where connectors are returning this:

```
http://localhost:4242/myConnector/API
```

instead of this:

```
https://external.net/myConnector/API
```

Notice that both the host and protocol are incorrect.  It may be necessary  to check that x-forwarded-proto and x-forwarded-host headers are being handled correctly if the wrong protocol or host are observed.

### Availability and Connectivity

All interactions between applications and connectors will go through the Mobile Flows Server hosted in the cloud on AWS.  Connector endpoints must be publicly available for the Mobile Flows Server to access them.


Requests to Mobile Flows will sometimes involve single requests that must be sent to multiple connectors.  Mobile Flows would then aggregate the set of connector responses into a single response.  Connector interactions will timeout after a short amount of time to avoid a single poorly behaving connector blocking responses.  


A deployed connector that takes several seconds to respond may timeout.

## Heroku Deployment Example

This example is targeted for taking an existing connector and quickly making it publicly available.  This is **not** intended to be explicit directions for going to production.  Follow these steps to be able to see a connector in action.  A connector deployed in this way can be configured in Unified Endpoint Management and tested in live products!


Tools and Resources:

* Node JS
* [Weather Connector](https://github.com/vmwaresamples/card-connectors-guide/tree/master/samples/node)
* Heroku

Prerequisites:

* Heroku Account ([Free Tier](https://www.heroku.com/free) available)
  * Take care when considering your usage with a free tier account.  Make sure a free tier connector is not deployed in such a way that an application is able to keep it alive indefinitely.
*  [Heroku CLI installed](https://devcenter.heroku.com/articles/getting-started-with-nodejs#set-up)


In general, these steps should be transferable to any other Node JS connector. These steps will be based on the Heroku guide found [here](https://devcenter.heroku.com/articles/getting-started-with-nodejs).  You are encouraged to work through the Heroku deployment guide for their sample Node JS application before attempting with a connector.

### Getting Setup

Start with a fresh clone of the Weather Connector:

```
$git clone https://github.com/vmwaresamples/card-connectors-guide.git
$cd card-connectors-guide/samples/node
$npm install
```

This is our home directory.  We will be working from here unless otherwise specified.


You already have enough to deploy the connector locally.  Go ahead and try it:

```
$heroku local

...

3:05:13 PM web.1 |  > node connector.js "--port=5000"
3:05:13 PM web.1 |  Connector listening on port 5000.
```
Test it by navigating to `localhost:5000`, paying attention to your console output in case another port was used.  A few more steps are required to deploy to Heroku's cloud.

### Preparing for cloud deploy

We will be following [these steps](https://devcenter.heroku.com/articles/getting-started-with-nodejs#deploy-the-app) of the Heroku Guide.


We need to create an app on Heroku:

```
$git init
$heroku create
Creating app... done, ⬢ random-name-4242
https://random-name-4242.herokuapp.com/ | https://git.heroku.com/random-name-4242.git
```

The Weather Connector listens to port 3000 by default, but we need it to listen to the port Heroku wants to use.  In the Weather Connector repository you should notice a Procfile in the root directory with this line:

```
$web: npm start -- --port=$PORT
```
This lets Heroku know how to start our web process and passes the PORT environment variable to be used.


Try opening the application in the cloud:

```
$heroku open
```

Navigate to the Weather Connectors image ref to see that it is working.  You should see:


![Weather Connector Icon](https://github.com/vmwaresamples/card-connectors-guide/blob/master/samples/node/public/images/connector.png?raw=true)

<!--- Add link to UEM configuration guide -->

Congratulations!  Enjoy your deployed connector.






