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

* **Abstracting Away of the Back-End**

  <!-- fill in later -->

* **Responsiveness**

  <!-- fill in later -->

Naturally, no tool is the right tool for every job. But applications in which the aforementioned features are important will probably benefit from using a framework. Additionally, of course, frameworks usually make it easier for the developer by providing libraries and generators for common tasks.

Ember, in particular, has several great things going for it.

* Of all of the more prominent frameworks, Ember is the oldest and most mature.
* Ember was primarily created by Yehuda Katz, one of the most significant contributors to Rails. Yehuda was also actively involved in the creation of jQuery, and is the creator of Handlebars. Consequently...
* Ember uses Handlebars (which you should already be familiar with) as its template engine for generating new HTML.
* Like Rails, Ember favors convention over configuration. Although it gives you less freedom than some other frameworks (e.g. Backbone), it also provides a lot of structure, which is helpful for beginners. This also makes it possible for Ember to easily generate files when they're needed.

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

## Parts of An Ember Application

In the first version of Ember, Ember was built on an MVC structure. The key pieces of that structure were:

* Views (`Ember.View`)
* Templates
* The Ember Router (`Ember.Router`)
* Models (`DS.Model`)
* Routes (`Ember.Route`)
* Controllers (`Ember.Controller`)

Each of these parts had a different responsibility. **Views** were the heart of Ember's core functionality; each View represented a visible UI element in the page, and contained properties and methods (including event handlers) that related to how that UI element looked and behaved.

<!-- Add example of a View from the demo app. -->

The HTML content for a View was provided by a corresponding **Template**. Each Template was written in Handlebars, and could access and manipulate properties in the View. In-built Handlebars helpers such as `{{#if}}` and `{{#each}}` were also available.

<!-- Add example of a Template, ideally one referencing a property in the View. -->

Of course, an application would typically need to show many different templates. The system for determining which UI elements to show is called _UI Routing_.




## Additional Resources

List additional related resources such as videos, blog posts and official documentation.

- Item 1
- Item 2
- Item 3
