# spa-boot-angular
A Basic Spring Boot web application configured for an AngularJS single page client application.

Why is this so hard? Seriously?!

The end result is really simple but getting to this point is really not. Don't believe me? Well you're here
aren't you. Just try and work it all out yourself before looking at this code, you'll understand the misery.

This project uses AngularJS, using ReactJS or any other client framework should be very similar.

If you're looking for an equivalent ReactJS version, check out [spa-boot-react](https://github.com/caprica/spa-boot-react).

If you're looking for an equivalent VueJS version, check out [spa-boot-vue](https://github.com/caprica/spa-boot-vue).

Anyway, here it is, a skeleton project for a single page web application using SpringMVC for the middle tier.

Key features:

 * The web application is mapped to the root "/" context
 * All static resources are under the "/assets/" path
 * A request for "index.html" will redirect to "/" for a nicer URL in the address bar
 * All web-service API are under an "/api/" path
 * A request for an unknown API will have a catch-all that maps to a BAD_REQUEST response
 * Any other request, including deep-link requests, will map to the single page web application for client
   routing
 * Does NOT rely on ugly hashes '#' in URLs or the address bar

The names for the path prefixes used are arbitrary and can be changed to whatever you prefer.

There is no cache control for the static resources, you might like to consider that.

You can run this project from a shell/terminal, simply type:

```
mvn spring-boot:run
```

To change the port number used by Jetty:

```
mvn spring-boot:run -Dspring-boot.run.arguments=--server.port=8085
```

Then open your browser at the following URLs to prove it's all configured properly:

```
http://localhost:8080
http://localhost:8080/index.html
http://localhost:8080/api/users
http://localhost:8080/api/users/boss
http://localhost:8080/api/users/emo
http://localhost:8080/api/users/emma
http://localhost:8080/api/version
http://localhost:8080/api/anything-else-does-not-exist
http://localhost:8080/assets/css/index.css
http://localhost:8080/assets/img/star.png
http://localhost:8080/assets/js/app.js
```

It can still be useful to route to static assets on the server - e.g. images or scripts that not part of the client
application itself.

This project also has client-side routing enabled. These are deep links that will be routed to the client index
page where the React router will take over:

```
http://localhost:8080/users
http://localhost:8080/users/boss
http://localhost:8080/users/emo
http://localhost:8080/users/emma
http://localhost:8080/a/not/found/page
```

Full refreshes will work and be routed correctly.

Everything else is just like any other AngularJS application.

If you want to disable source maps, look in the package.json for the scripts section and make the following
change:

```
  "scripts": {
    "ng": "ng",
    "start": "ng serve --proxy-config proxy.conf.json",
    "build": "ng build --source-map=false",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```

Proxying API requests also works just the same as before, add the following to a proxy.conf.json file in the
same directory as package.json (this has already been applied in this project):

```
{
  "/api": {
    "target": "http://localhost:8080",
    "secure": false
  }
}
```

You may need to adjust the port number, in this case 8080 is the port number used by the Jetty container launched
by the aforementioned maven command.

You also need to tweak the scripts section in package.json to specify the proxy configuration file:

```
  "scripts": {
    "ng": "ng",
    "start": "ng serve --proxy-config proxy.conf.json",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e"
  },
```

And then as usual to run the development version of the application (use port 4200 by default rather than 8080):

```
cd src/main/app
yarn start
```

You're welcome.
