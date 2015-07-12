Building a static - isomorphic react blog engine
================================================

TODO: Explain what static - isomorphic means

Step 1
------

I'm going to create an isomorphic app using the react-router.

`GET /2015-07-12/blog-post-title` will result in:

  1.  Fetching the file stored as `/content/src/2015-07-12/blog-post-title`
  2.  Rendering it's contents inside a react component
  3.  Sending results to the client

Step 2
------

I'm going to prepare a build system, that:

  1.  Starts the app
  2.  For each file in `/src/**/*.md` makes a relevant request and stores the resulting body as an HTML file in `/content/`, e.g. `/content/2015-07-12/blog-post-title`.

That way each blog post will be stored in an HTML file that can be served directly by an HTTP server like Nginx. Each file will contain a frontend script with whole application logic necessary to fetch other posts from `/content/src/` and  render it in the client.
