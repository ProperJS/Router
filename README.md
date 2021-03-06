ProperJS // Router
==================

> Lightweight JS router with History.



### Installation
```shell
npm i properjs-router --save-dev
```


### Usage
Alone this utility is quite useful, but it's fully realized in [ProperJS/PageController](https://github.com/ProperJS/PageController).
```javascript
import Router from "properjs-router";

// Router is fully utilized with PageController
// @see: https://github.com/ProperJS/PageController
const router = new Router({
    // Use XHR
    async: true, // Default
    // Keeps response caches for requests
    caching: true, // Default
    // Handle 404s and 500s
    handle404: true, // Default
    handle500: true, // Default
    // Pass options to Historia
    // @see: https://github.com/ProperJS/Historia
    historyOptions: {},
    // Run Router as a proxy (false by default)
    // proxy: {
    //     domain: "https://your.proxy.domain",
    // },
});

// Bind router to page
router.bind();

// Some routes to match, same style as MatchRoute
// @see: https://github.com/ProperJS/MatchRoute
const routes = [
    // Known route
    "some/route",

    // Unknown route
    "another/:slug",

    // Enforce Number on last URI segment
    "also/:slug/:num!num",
];

// Apply the GET listener to routes
routes.forEach(( route ) => {
    router.get( route, ( data ) => {
        console.log( "route data", data );
    });
});

// Bind to preget events
// Fires when the route is matched before the request begins
router.on( "preget", ( data ) => {
    console.log( "preget", data );
});

// Bind to popget events
// Fires when Historia fires a popstate event
router.on( "popget", ( data ) => {
    console.log( "popget", data );
});
```


#### Files
Router will ignore links deemed to be `files`.


#### Event metaKey
Router will honor the metaKey property on matched nodes allowing `Command+click`.


#### Ignore Links
Router will ignore all links with a `js-router--ignore` className.
