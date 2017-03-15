[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Ember

**Ember** is a JavaScript framework for making richly interactive front-end
applications. There are many front-end frameworks out there, but Ember is one
of the four most prominent (the others being **Angular**, **Backbone**, and
**React**).

## Prerequisites

-   [ga-wdi-boston/handlebars](https://github.com/ga-wdi-boston/handlebars)
-   [ga-wdi-boston/ember-study](https://github.com/ga-wdi-boston/ember-study)

## Objectives

By the end of this, developers should be able to:

-   Explain what Ember is and what kinds of applications it's used for.
-   Create new applications with [ga-wdi-boston/ember-template](https://github.com/ga-wdi-boston/ember-template).
-   Name and describe the different layers of an Ember application.

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

## NOTE: Install `ember-cli` and Dependencies

You should've already installed `ember-cli`, `bower`, and
`watchman` from the `ember-study`. If you haven't, please do so.

## Starting a New Ember Application

Similarly to `rails`, you can type `ember new` to generate new
Ember applications. However, just like `rails`, we have
several custom configurations and tasks available in [ga-wdi-boston/ember-template](https://github.com/ga-wdi-boston/ember-template), so you'll follow the installation instructions there to start new applications.

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
├── app/
│   ├── app.js
│   ├── application/
│   │   ├── adapter.js
│   │   ├── serializer.js
│   │   └── template.hbs
│   ├── components/
│   ├── helpers/
│   ├── index.html
│   ├── resolver.js
│   ├── router.js
│   └── styles/
│       └── app.scss
├── bower.json
├── config/
│   └── environment.js
├── ember-cli-build.js
├── package.json
├── public/
│   ├── crossdomain.xml
│   ├── favicon.ico
│   └── robots.txt
├── testem.js
├── tests/
└── vendor/
```

### Lab: Become Familiar with Ember File Structure

Match the generated structure to the description of the layers found in the
[overview](http://ember-cli.com/user-guide/#folder-layout) and [resolver
documentation](https://ember-cli.com/user-guide/#module-directory-naming-structure).

1.  In which folder will mainly you be working?
1.  Where is the default HTML layout defined?
1.  Where will you find the ready-to-deploy files?

As with Rails, naming conventions are important. File names are linked to
variable references, and if either is misspelled, you might experience
frustration. Familiarize yourself with the [naming
conventions](http://ember-cli.com/user-guide/#naming-conventions).

For reference:

![Ember Core Concepts](https://guides.emberjs.com/v2.10.0/images/ember-core-concepts/ember-core-concepts.png)

## Layers of an Ember Application

Don't worry about retaining all of this right now - the purpose of this section
is just to give you a high-level overview over all of the different pieces of an
Ember application. You should refer back to this material any time that you feel
yourself losing sight of the big picture.

### Ember 2.0

The key parts of an Ember application are:

-   The Ember Router (`Ember.Router`)
-   Routes (`Ember.Route`)
-   Templates
-   Models (`DS.Model`)
-   Components (`Ember.Component`)
-   Adapters (`DS.RESTAdapter`)

#### Ember Router
```js
const Router = Ember.Router.extend({
  location: config.locationType,
});

Router.map(function () {
});
```

In particular, what the Router does is associate a URL path with a particular
Template, through an intermediary object called a **Route** object.

#### Ember Route
`app/lists/route.js`
```js
export default Ember.Route.extend({
  model () {
    return this.get('store').findAll('list');
  },
});
```

A Route has three jobs: (1) parsing information contained in the URL, such as an
ID or a query string, (2) linking the Router to a particular Component/Template
(among other things), and (3) loading the UI element's data via a method called
`model`.

#### Ember Model
`app/list/model.js`
```js
export default DS.Model.extend({
  title: DS.attr('string'),
  hidden: DS.attr('boolean'),
  items: DS.hasMany('item'),
});
```
This data can be hard-coded, but usually it is pulled from the app's central
data store (provided by library called `ember-data`) which is accessible to each
Route from that Route's `store` property. The resources available from that
store are defined by **Models**, which essentially served as resource-specific
schemas.

#### Ember Template
`app/lists/template.hbs`
```js
{{#each model as |list|}}
  {{listr-list/card list=list}}
{{/each}}
```
The HTML content for Route or Component is provided by a corresponding **Template**. Each Template was written in Handlebars, and could access and manipulate properties
in the Component or Route. In-built Handlebars helpers such as `{{#if}}` and `{{#each}}` are also available. Templates can reference other Components by name,
and pass information from one Component to another.


Of course, an application would typically need to show many different templates.
The system for determining which UI elements to show is called _UI Routing_, and
in Ember that job is carried out by the **Router**.

#### Ember Components
<!-- Add example of a Component from the demo app. -->

A Component can be invoked from within a Template (either a normal one or
another Component's Template), and unlike a View, it does not have access to the
entire scope of the Route; instead its scope is _explicitly defined_ at the
location where the Component is invoked. This has the advantage of making
Components very modular (and consequently, more interchangeable and re-usable).

The changeover from Controllers and Views (Ember 1.0) to Components (Ember 2.0)
 is in process but is not complete. Both Controllers and Views are deprecated,
 but _Components are not yet 'routable'_ (though that change will probably be
 coming soon). The work-around is straightforward:

1.  Represent all your UI elements with a Component.
1.  **If your view state needs a Route associated with it**, load it in a
    normally-named template. All of your code will either go in a Route or the Component itself.

This newer structure is now [much
simpler](https://guides.emberjs.com/v2.10.0/getting-started/core-concepts/).

#### Ember Adapter

Each resource can have its data stored in a different type of data storage
system (e.g. `localstorage`, test fixtures, a back-end API), and the details of
that resource-storage relationship are handled by a type of object called an
**Adapter**.

### Ember 1.0

Make sure you use docs for Ember 2.0+. If it says Ember 1.x, you're probably in the wrong place.

## Additional Resources

-   [`ember-cli` User Guide](http://ember-cli.com/user-guide/)
-   The [Official Ember API](http://emberjs.com/api/)
-   [Ember.js Guides](http://guides.emberjs.com/)

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
