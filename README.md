[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Ember

**Ember** is a JavaScript framework for making richly interactive front-end
applications. There are many front-end frameworks out there, but Ember is one
of the four most prominent (the others being **Angular**, **Backbone**, and
**React**).

## Prerequisites

-   [ga-wdi-boston/handlebars](https://github.com/ga-wdi-boston/handlebars)

## Objectives

By the end of this, developers should be able to:

-   Explain what Ember is and what kinds of applications it's used for.
-   Download and install `ember-cli` and its dependencies.
-   Create new applications with [ga-wdi-boston/ember-template](https://github.com/ga-wdi-boston/ember-template).
-   Name and describe the different layers of an Ember application.
-   Contrast the layers of Ember 1 and Ember 2 applications.

## Preparation

1.  [Fork and clone](https://github.com/ga-wdi-boston/meta/wiki/ForkAndClone)
    this repository.
1.  Install dependencies with `npm install` and `bower install`.

## Ember's Purpose

Why use a front-end framework instead of vanilla JavaScript, jQuery, and
Handlebars/Moustache? Ultimately, it boils down to a couple of key features.

-   Routability

    In most of the websites you've been to, you can use your browser's "back"
    button to go back to a page you just visited. However, as you may have
    noticed, this is not possible in a single-page application with only JS and
    jQuery - the URL of the page never changes! Most front-end frameworks
    provide a way to change the URL of the page and tie it to the state of the
    application, allowing for the use of the "back" button, bookmarking, and
    many other features.

-   Less AJAX

    Having to write lots of AJAX calls can be tedious. Most front-end frameworks
    will abstract away the process of writing AJAX requests by creating a local
    copy of a back-end resource and handling all of the AJAX necessary to
    synchronize these two clones behind the scenes.

-   Responsiveness

    Because of the above, your back-end resources effectively get 'cached' on
    the front-end, so the front-end doesn't need to make as many requests in
    order to have the data it needs. As a result, displaying resource data is
    faster, and when data gets updated locally, it doesn't need to wait until
    it's synched up with the back-end before showing the updated data.

Naturally, no tool is the right tool for every job. But applications in which
the aforementioned features are important will probably benefit from using a
framework. Additionally, of course, frameworks usually make it easier for the
developer by providing libraries and generators for common tasks.

Ember, in particular, has several great things going for it.

Of all of the more prominent frameworks, _Ember is the oldest and most mature_.

Ember was primarily created by Yehuda Katz, one of the most significant
contributors to Rails. Yehuda was also actively involved in the creation of
jQuery, and is the creator of Handlebars. Consequently _Ember uses Handlebars
(which you are already be familiar with) as its template engine for generating
new HTML_.

Like Rails, Ember favors convention over configuration. Although it gives you
less freedom than some other frameworks (e.g. Backbone), it also provides a lot
of structure, which is helpful for beginners. This also makes it possible for
Ember to easily generate files when they're needed.

Ember provides a neat feature called 'data binding'; what this means is that you
can define certain values to be _persistently related_ to other values, so that
if one value gets updated, all values bound to it _automatically get updated_.

How it does this will be briefly touched on in
[ga-wdi-boston/ember-object](https://github.com/ga-wdi-boston/ember-object);
however, binding is one of the most complex topics in Ember, and we won't be
diving into it too deeply this week. That said, we absolutely welcome you to
explore this topic on your own time.

## Install `ember-cli` and Dependencies

To begin building applications in Ember, you'll need to do a little setup first.

`ember-cli` is a tool that will serve much the same purpose as `rails` did with
Rails and `express` did with Express - spinning up new applications, generating
files, running scripts, and performing tests. Install it by running

```sh
npm install -g ember-cli
```

We also need `bower`. If you aren't sure whether it's installed, or to update:

```sh
npm install -g bower
```

`watchman` is a tool for watching files and recording when they change, allowing
your Ember app to be updated _as you edit it_. We'll use Homebrew to download
it:

```bash
brew update && brew install watchman
```

Linux users will unfortunately need to download and install `watchman` from the
source code. Directions for that can be found [in the Watchman
docs](https://facebook.github.io/watchman/docs/install.html#installing-from-source).

To verify that everything is working, run the command `ember -v`. You should see
a response more or less like this.

```bash
version: 2.4.2
node: 4.2.2
os: darwin x64
```

### Gotchas

> Note, there exists a similarly named npm package (watchman) which is not the
> intended installation. If you have this package installed you may see the
> following warning:
>
> ```bash
> invalid watchman found, version: [2.9.8] did not satisfy [^3.0.0], falling back to NodeWatcher
> ```
>
>  — <http://ember-cli.com/user-guide/#watchman>

> Lastly, when Watchman is not installed, a notice is displayed when invoking
> various commands. You can safely ignore this message:
>
> ```bash
> Could not find watchman, falling back to NodeWatcher for file system events
> ```
>
>  — <http://ember-cli.com/user-guide/#watchman>

You may receive `watchman` errors if your Ember applications become large
enough. This will happen sooner on OS X than on linux. It's a great idea to go
ahead and take care of this. See [Linux inotify
limits](https://facebook.github.io/watchman/docs/install.html#linux-inotify-limits)
and [Mac OS X File Descriptor
Limits](https://facebook.github.io/watchman/docs/install.html#max-os-file-descriptor-limits).
Instructions for adjusting these limits is included for Mac OS X. For Linux, see
[this doc from
guard](https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers).

## Starting a New Ember Application

We won't be using `ember new` to generate new Ember applications. We have
several custom configurations and tasks available in [ga-wdi-boston/ember-template](https://github.com/ga-wdi-boston/ember-template),
so you'll follow the installation instructions there to start new applications.

A new, up-to-date Ember application has been provided for you in this
repository.

## Ember Application Structure

If you'd like to see the basic structure of a new Ember application, run the
below command:

```bash
brew install tree
```

If you then run `tree`, we see the basic structure of a new Ember application.
An abbreviated version:

```bash
.
├── README.md
├── app
│   ├── app.js
│   ├── application
│   │   ├── adapter.js
│   │   ├── serializer.js
│   │   └── template.hbs
│   ├── components
│   ├── helpers
│   ├── index.html
│   ├── resolver.js
│   ├── router.js
│   └── styles
│       └── app.scss
├── bower.json
├── config
│   └── environment.js
├── ember-cli-build.js
├── package.json
├── public
│   ├── crossdomain.xml
│   ├── favicon.ico
│   └── robots.txt
├── testem.js
├── tests
└── vendor
```

### Lab: Become Familiar with Ember File Structure

Match the generated structure to the description of the layers found in the
[overview](http://ember-cli.com/user-guide/#folder-layout) and [resolver
documentation](http://ember-cli.com/user-guide/#using-modules).

1.  Where will you be working?
1.  Where is the default HTML layout defined?
1.  Where will you find the ready-to-deploy files?

As with Rails, naming conventions are important. File names are linked to
variable references, and if either is misspelled, you might experience
frustration. Familiarize yourself with the [naming
conventions](http://ember-cli.com/user-guide/#naming-conventions).

## Layers of an Ember Application

Don't worry about retaining all of this right now - the purpose of this section
is just to give you a high-level overview over all of the different pieces of an
Ember application. You should refer back to this material any time that you feel
yourself losing sight of the big picture.

### Ember 1.0

In the first version of Ember, Ember was built on an MVC structure. It is
important to understand prior Ember conventions since some documentation and
tutorials you find will use the older structure. We see how the layers changed
between Ember 1.0 and Ember 2.0 shortly.

The key pieces of the older structure were:

-   Views (`Ember.View`)
-   Templates
-   The Ember Router (`Ember.Router`)
-   Routes (`Ember.Route`)
-   Models (`DS.Model`)
-   Adapters (`DS.RESTAdapter`)
-   Controllers (`Ember.Controller`)

Each of these parts had a different responsibility. **Views** were the heart of
Ember's core functionality; each View represented a visible UI element in the
page, and contained properties and methods (including event handlers) that
related to how that UI element looked and behaved.

<!-- Add example of a View from the demo app. -->

Views could be nested inside each other, in a tree-like structure.

<!-- Add diagram of nested Views on the page mapping to a text tree of View
names. -->

The HTML content for a View was provided by a corresponding **Template**. Each
Template was written in Handlebars, and could access and manipulate properties
in the View. In-built Handlebars helpers such as `{{#if}}` and `{{#each}}` were
also available.

<!-- Add example of a Template, ideally one referencing a property in the
View. -->

Of course, an application would typically need to show many different templates.
The system for determining which UI elements to show is called _UI Routing_, and
in Ember that job is carried out by the **Router**.

<!-- Add code snippet of the demo app's router. -->

In particular, what the Router does is associate a URL path with a particular
View and Template, through an intermediary object called a **Route** object.
**Not every View needs to be 'routable', but _every_ Route must refer to a
View**.

A Route has three jobs: (1) parsing information contained in the URL, such as an
ID or a query string, (2) linking the Router to a particular View/Template
(among other things), and (3) loading the UI element's data via a method called
`model`.

<!-- Add example of a Route from the demo app. -->

This data can be hard-coded, but usually it is pulled from the app's central
data store (provided by library called `ember-data`) which is accessible to each
Route from that Route's `store` property. The resources available from that
store are defined by **Models**, which essentially served as resource-specific
schemas.

<!-- Add example of a Model from the demo app. -->

Each resource can have its data stored in a different type of data storage
system (e.g. `localstorage`, test fixtures, a back-end API), and the details of
that resource-storage relationship are handled by a type of object called an
**Adapter**.

<!-- Add example of an Adapter from the demo app. -->

In addition to a View (+ Template), a Route also links to a type of object
called a **Controller**. The purpose of a Controller was to house all of the
'business logic' of our UI element - basically, any sort of CRUD actions that
the UI element would need to perform on its data (which, again, was provided by
the Route). A Controller would also house any additional helper properties or
methods related to data manipulation.

<!-- Add example of a Controller from the demo app. -->

### Ember 2.0

All of the above was true for Ember v1. **_However, with Ember v2, a major
change began_** - specifically, a move was made to replace Controllers and Views
as the abstractions for a particular UI element with a more flexible type of
object called a **Component**. Like Views, Components have Templates associated
with them, and they hold properties and methods related to the operation of that
UI element; these Templates are stored in a different location than normal
Templates.

<!-- Add example of a Component from the demo app. -->

A Component can be invoked from within a Template (either a normal one or
another Component's Template), and unlike a View, it does not have access to the
entire scope of the Route; instead its scope is _explicitly defined_ at the
location where the Component is invoked. This has the advantage of making
Components very modular (and consequently, more interchangeable and re-usable).

The change-over from Controllers and Views to Components is in process but is
not complete. Both Controllers and Views are deprecated, but _Components are not
yet 'routable'_ (though that change will probably be coming soon). The
work-around is straight-forward:

1.  Represent all your UI elements with a Component.
1.  **If your view state needs a Route associated with it**, load it in a
    normally-named template. You should **not** need to generate a View or
    Controller, since your code will either go in a Route or the Component
    itself.

This newer structure is now [much
simpler](https://guides.emberjs.com/v2.4.0/getting-started/core-concepts/).

## Code-Along: Start an Application with Generators

We'll be working with a list-making app, Listr, throughout our journey with
Ember. We have a client [client](https://github.com/ga-wdi-boston/listr-client)
and [api](https://github.com/ga-wdi-boston/listr-api) for demostration purposes.

Let's try using a few generators and a little custom code to begin building our
own versions of Listr.

```bash
ember generate route lists
```

## Additional Resources

-   [`ember-cli` User Guide](http://ember-cli.com/user-guide/)
-   The [Official Ember API](http://emberjs.com/api/)
-   [Ember.js Guides](http://guides.emberjs.com/)

## [License](LICENSE)

Source code distributed under the MIT license. Text and other assets copyright
General Assembly, Inc., all rights reserved.
