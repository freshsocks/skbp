Some type of boilerplate...
===========================

##Scaffolding

```
# Make sure Yeoman & generator-express installed
npm install -g yo
npm install -g generator-express

# Build the foundation
mkdir myapp && cd myapp
touch README.md
yo express
    > Basic
    > EJS
npm install node-sass --save
mkdir sass
touch sass/main.scss
```

I'm using EJS templates instead of Jade because I want to add Polymer and other web components in the future, and EJS plays nice with vanilla HTML. I also don't like using Jade with Polymer because Polymer elements tend to have a bunch of attributes. It is often more readable to put each attribute on a newline; however, Jade is very strict about newlines and spacing, plus the syntax expects comma-separated attributes - it doesn't make for a pretty Polymer element.

I'm using node-sass to render `.scss` files into css.

##Modifying app.js

Add node-sass at the top `var sass = require('node-sass');`

Add middleware for node-sass:
```
app.use(
    sass.middleware({
          src: __dirname + '/sass'
        , dest: __dirname + '/public/css'
        , debug: true
        , outputStyle: 'compressed'
        , prefix: '/css'
    })
);
// make sure node-sass comes BEFORE static middleware
```

Enable livereload for scss files: [line 39 of Gruntfile.js]
```
//...
      css: {
        files: [
          'public/css/*.css',
          'sass/*.scss'      // Add our sass file directory to css watch files
        ],
        options: {
          livereload: reloadPort
        }
      },
//...
```

##Start app

Use `grunt` to start the app.

Go to _http://localhost:3000_ in your browser.

Edit your _style.scss_ file and save; watch the bowser automatically reflect your changes!

##Back it up

Now would be a good time to save the working version we have with git.

```
git init
git add .
git commit -m "initial commit: sass added"
git push -u origin master

---------------------------

Another resoruce:

http://www.thecrumb.com/2014/03/15/using-grunt-for-live-reload/

Shows you how to auto-launch browser with livereload and how to use grunt for express settings.
