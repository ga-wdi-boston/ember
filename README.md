![General Assembly Logo](http://i.imgur.com/ke8USTq.png)

# Ember Overview

## Lesson Details
### Foundations
By this time, students have already learned:

- How to create and render Handlebars templates.
- How to use block- and inline- Handlebars helpers.
- Using Handlebars partials.

### Objectives

By the end of this, students should be able to:

- Explain what Ember is and what kinds of applications it's used for.
- Download and install `ember-cli` and its dependencies.
- Name and describe the different parts of an Ember application.
- Explain how apps in Ember 1 differ from apps in Ember 2.

## Why Use Ember?

**Ember** is a JavaScript framework for making richly interactive front-end applications. There are many front-end frameworks out there, but Ember is one of the four most prominent (the others being **Angular**, **Backbone**, and **React**).

Why use a front-end framework instead of vanilla JavaScript, jQuery, and Handlebars/Moustache? Ultimately, it boils down to a couple of key features.

* **Routability**

  In most of the websites you've been to, you can use your browser's "back" button to go back to a page you just visited. However, as you may have noticed, this is not possible in a single-page application with only JS and jQuery - the URL of the page never changes! Most front-end frameworks provide a way to change the URL of the page and tie it to the state of the application, allowing for the use of the "back" button, bookmarking, and many other features.

* **Less AJAX**

  Having to write lots of AJAX calls can be tedious. Most front-end frameworks will abstract away the process of writing AJAX requests by creating a local copy of a back-end resource and handling all of the AJAX necessary to synchronize these two clones behind the scenes.

* **Responsiveness**

  Because of the above, your back-end resources effectively get 'cached' on the front-end, so the front-end doesn't need to make as many requests in order to have the data it needs. As a result, displaying resource data is faster, and when data gets updated locally, it doesn't need to wait until it's synched up with the back-end before showing the updated data.

Naturally, no tool is the right tool for every job. But applications in which the aforementioned features are important will probably benefit from using a framework. Additionally, of course, frameworks usually make it easier for the developer by providing libraries and generators for common tasks.

Ember, in particular, has several great things going for it.

* Of all of the more prominent frameworks, _Ember is the oldest and most mature_.
* Ember was primarily created by Yehuda Katz, one of the most significant contributors to Rails. Yehuda was also actively involved in the creation of jQuery, and is the creator of Handlebars. Consequently _Ember uses Handlebars (which you are already be familiar with) as its template engine for generating new HTML_.
* Like Rails, Ember favors convention over configuration. Although it gives you less freedom than some other frameworks (e.g. Backbone), it also provides a lot of structure, which is helpful for beginners. This also makes it possible for Ember to easily generate files when they're needed.
* Ember provides a neat feature called 'data binding'; what this means is that you can define certain values to be **_persistently related_** to other values, so that if one value gets updated, all values bound to it _automatically get updated_.
> How it does this will be briefly touched on in the lesson on `Ember.Object`; however, binding is one of the most complex topics in Ember, and we won't be diving into it too deeply this week. That said, we absolutely welcome you to explore this topic on your own time.

## Setting Up Ember

To begin building applications in Ember, you'll need to do a little setup first.

1. `ember-cli`

  `ember-cli` is a tool that will serve much the same purpose as `rails` did with Rails and `express` did with Express - spinning up new applications, generating files, running scripts, and performing tests. Install it by running
  ```bash
  npm install -g ember-cli
  ```

2. `watchman`

  `watchman` is a tool for watching files and recording when they change, allowing your Ember app to be updated _as you edit it_.
  We'll use Homebrew to download it:
  ```bash
  brew update && brew install watchman
  ```
  > Linux users will unfortunately need to download and install `watchman` from the source code. Directions for that can be found [here](https://facebook.github.io/watchman/docs/install.html#installing-from-source).

To verify that everything is working, run the command `ember -v`. You should see a response more or less like this.
```bash
version: 1.13.13
node: 5.0.0
npm: 2.14.10
os: darwin x64
```
Ember 2.0 was released in August 2015, and `ember-cli` had been planning to release its v2.0 at the same time; however, the latest release of `ember-cli` has been delayed and (as of this writing) has not yet been released; as a result the current version does not reference the most up-to-date version of Ember. Fortunately, we can get around this by manually editing some files inside our Ember projects, as we will soon see.

Now that you've installed `ember-cli`, setting up a new Ember project is easy. Simply navigate up to wherever you keep your projects and run the command `ember new <application name>` - it will generate a new application with the following structure:
```bash
.
├── app
│   ├── app.js
│   ├── components
│   ├── controllers
│   ├── helpers
│   ├── index.html
│   ├── models
│   ├── router.js
│   ├── routes
│   ├── styles
│   │   └── app.css
│   └── templates
│       ├── application.hbs
│       └── components
├── bower.json
├── config
│   └── environment.js
├── ember-cli-build.js
├── package.json
├── public
│   ├── crossdomain.xml
│   └── robots.txt
├── testem.json
├── tests
│   ├── helpers
│   │   ├── destroy-app.js
│   │   ├── module-for-acceptance.js
│   │   ├── resolver.js
│   │   └── start-app.js
│   ├── index.html
│   ├── integration
│   ├── test-helper.js
│   └── unit
└── vendor
```

As you might expect, the `app` directory is where we'll be writing most of our code.

## Parts of an Ember Application

Don't worry about retaining all of this right now - the purpose of this section is just to give you a high-level overview over all of the different pieces of an Ember application. You should refer back to this material any time that you feel yourself losing sight of the big picture.

### Ember 1.0

In the first version of Ember, Ember was built on an MVC structure. The key pieces of that structure were:

* Views (`Ember.View`)
* Templates
* The Ember Router (`Ember.Router`)
* Routes (`Ember.Route`)
* Models (`DS.Model`)
* Adapters (`DS.RESTAdapter`)
* Controllers (`Ember.Controller`)

Each of these parts had a different responsibility. **Views** were the heart of Ember's core functionality; each View represented a visible UI element in the page, and contained properties and methods (including event handlers) that related to how that UI element looked and behaved.

<!-- Add example of a View from the demo app. -->

Views could be nested inside each other, in a tree-like structure.

<!-- Add diagram of nested Views on the page mapping to a text tree of View names. -->

The HTML content for a View was provided by a corresponding **Template**. Each Template was written in Handlebars, and could access and manipulate properties in the View. In-built Handlebars helpers such as `{{#if}}` and `{{#each}}` were also available.

<!-- Add example of a Template, ideally one referencing a property in the View. -->

Of course, an application would typically need to show many different templates. The system for determining which UI elements to show is called _UI Routing_, and in Ember that job is carried out by the **Router**.

<!-- Add code snippet of the demo app's router. -->

In particular, what the Router does is associate a URL path with a particular View and Template, through an intermediary object called a **Route** object. **Not every View needs to be 'routable', but _every_ Route must refer to a View**.

A Route has three jobs: (1) parsing information contained in the URL, such as an ID or a query string, (2) linking the Router to a particular View/Template (among other things), and (3) loading the UI element's data via a method called `model`.

<!-- Add example of a Route from the demo app. -->

This data can be hard-coded, but usually it is pulled from the app's central data store (provided by library called `ember-data`) which is accessible to each Route from that Route's `store` property. The resources available from that store are defined by **Models**, which essentially served as resource-specific schemas.

<!-- Add example of a Model from the demo app. -->

Each resource can have its data stored in a different type of data storage system (e.g. `localstorage`, test fixtures, a back-end API), and the details of that resource-storage relationship are handled by a type of object called an **Adapter**.

<!-- Add example of an Adapter from the demo app. -->

In addition to a View (+ Template), a Route also links to a type of object called a **Controller**. The purpose of a Controller was to house all of the 'business logic' of our UI element - basically, any sort of CRUD actions that the UI element would need to perform on its data (which, again, was provided by the Route). A Controller would also house any additional helper properties or methods related to data manipulation.

<!-- Add example of a Controller from the demo app. -->

### Ember 2.0 and Above

All of the above was true for Ember v1. **_However, with Ember v2, a major change began_** - specifically, a move was made to replace Controllers and Views as the abstractions for a particular UI element with a more flexible type of object called a **Component**. Like Views, Components have Templates associated with them, and they hold properties and methods related to the operation of that UI element; these Templates are stored in a different location than normal Templates.

<!-- Add example of a Component from the demo app. -->

A Component can be invoked from within a Template (either a normal one or another Component's Template), and unlike a View, it does not have access to the entire scope of the Route; instead its scope is _explicitly defined_ at the location where the Component is invoked. This has the advantage of making Components very modular (and consequently, more interchangeable and re-usable).

**Where things stand now:**
The change-over from Controllers & Views to Components is in process but is not complete. Currently, both systems are supported. However, _Components are not yet 'routable'_ (though that change will probably be coming soon). The practical implications of this are that

1. **If your UI element needs a Route associated with it**, use a **_Controller and a View_** (+ a normal Template) to represent it.

2. **In all other cases**, represent your UI element with a **_Component_** (+ a Component Template).

<!-- Cite example of using a Controller + a View vs using a Component -->

At a high-level, here is a diagram illustrating how all of the different parts of an Ember application tie in when we follow this pattern.

<!-- Diagram of an Ember app's parts. -->

## Additional Resources

- [`ember-cli` User Guide](http://ember-cli.com/user-guide/)
- The [Official Ember API](http://emberjs.com/api/)
- [Ember.js Guides](http://guides.emberjs.com/v2.2.0/)
