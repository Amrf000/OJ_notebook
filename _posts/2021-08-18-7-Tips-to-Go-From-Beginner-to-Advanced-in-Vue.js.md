---
layout: post
title: 7 Tips to Go From Beginner to Advanced in Vue.js
category: Vue
tags: [vue]
---

7 Tips to Go From Beginner to Advanced in Vue.js
================================================

Level up your Vue.js game
-------------------------

[

![Aris Pattakos](/md_blog/public/assets/2021-08-18/1_ltupnWeMgY_r3K06lBQnpg.jpeg)

](https://aris-pattakos.medium.com/?source=post_page-----af7ca56ea31d--------------------------------)

[Aris Pattakos](https://aris-pattakos.medium.com/?source=post_page-----af7ca56ea31d--------------------------------)

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2F38947f334fde&operation=register&redirect=https%3A%2F%2Fbetterprogramming.pub%2F7-tips-to-go-from-beginner-to-advanced-in-vue-js-af7ca56ea31d&user=Aris%20Pattakos&userId=38947f334fde&source=post_page-38947f334fde----af7ca56ea31d---------------------follow_byline-----------)

[Nov 19, 2020](/7-tips-to-go-from-beginner-to-advanced-in-vue-js-af7ca56ea31d?source=post_page-----af7ca56ea31d--------------------------------) · 9 min read

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Faf7ca56ea31d&operation=register&redirect=https%3A%2F%2Fbetterprogramming.pub%2F7-tips-to-go-from-beginner-to-advanced-in-vue-js-af7ca56ea31d&source=post_actions_header--------------------------bookmark_preview-----------)

![Pencil on a notebook](/md_blog/public/assets/2021-08-18/1_6agYMMQSm3gFqAPLlUCH1Q.png)

Photo by [ASHLEY EDWARDS](https://unsplash.com/@westwardwayphotography?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pencil?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText).

Vue.js is my framework of choice for front-end development, and there are many reasons for that. I enjoy the simplicity, the powerful features, and the great performance it provides.

I started out with Vue because I found it easy at first. I kept using it because I loved it.

My tips on mastering Vue can help make you a better front-end developer and allow you to find better job opportunities in the future. I’ll go through these tips one by one, explaining what you have to learn to become advanced.

1\. Fully Understand Reactivity
===============================

How reactivity works
--------------------

Reactivity is a simple concept in front-end development libraries and frameworks. Understanding how it works at a deep level, though, can be hard. But it is well worth your time.

Here’s a small example:

<h1>{{ name }}</h1>

When the value of `name` changes, the UI will be updated accordingly. This is a very basic way to explain reactivity, but there are many more advanced examples to help you understand how it works.

Where reactivity goes wrong
---------------------------

Things can go wrong if you’re accessing a property within an object, as explained in this example:

In the example above, we define `myObject` as an empty object in the data method. Later, we give `myObject.message` a value.

This results in `{{ myObject.message }}` never displaying anything even though it receives a value at some point. Why is that?

That is basically because Vue does not know of the existence of the `myObject.message` property and therefore cannot react to changes in its value.

**How do I fix this?**
----------------------

There are a couple of ways to make sure that Vue reacts to changes in the `myObject.message` property. The most simple is to initialize it with an empty or null value:

myObject: {  
  message: ''  
}

If `myObject.message` exists in the data method, then Vue will listen and react to changes in its value and update the UI accordingly.

Another way to make sure the UI is updated is to update the full `myObject` object this way:

this.myObject = {message: 'Hello'}

Since Vue listens and reacts to changes in `myObject`, it will pick up this change and update the UI accordingly.

In short, Vue doesn’t listen to property changes in an object unless it knows these properties. Properties need to be defined in the data method or you need to update the whole object instead of the properties to make sure Vue tracks changes.

Learn more about reactivity by reading the “[Reactivity in depth](https://vuejs.org/v2/guide/reactivity.html)” section of the official documentation.

By understanding reactivity well, you can:

*   Debug scenarios where the UI doesn’t update when you expect it to.
*   Identify when views are updated and re-rendered.
*   Understand how computed properties are calculated.
*   Measure the cost of reactive values that require some CPU effort for calculations (e.g. form conditions).

2\. Optimal Parent-Child Communication
======================================

A question that I had all the time as a newbie was how to pass down data from a child to a parent component. Or how do I make sure that a child component is updated when something changes in the parent component?

These questions relate to how components should communicate with each other. The most basic way to do this is to use props. Props pass down data from parent to child. They are immutable and can be of many types such as strings, booleans, arrays, etc.

<component :message="myObject.message" />

Props form a one-way data flow, which means that whenever `myObject.message` changes in the parent component, the `message` prop will be updated accordingly. The opposite is _not true_.

You’re not supposed to change the value of props in child components, as they are immutable. Updating them will cause a Vue warning and it won’t trigger an update in the parent component.

So if props go “down,” how do you make values go “up”? To make values go up, you need to use events. You can easily remember this by noting the following: Props down, events up.

You can use props to pass down values to child components, as you saw in the previous example. If you need to pass values up from a child component to a parent component, you can emit events. Here’s an example that illustrates how it’s done:

You can use `$emit` to emit values or events from child components to parent components. You can listen to the events from the parent components using `v-on:` or `@` along with the name of the event (`@button-clicked` in this case). With `$emit`, you can pass one or more values and they can be of any type.

If you’re ever wondering how to pass values between parent and child components, just remember the “props down, events up” strategy and you’ll be able to make it work in a clean way.

3\. Learn About Performance Bottlenecks
=======================================

Slow applications are a pain in the ass. Our job as software developers is to make sure our applications run smoothly. It’s easy to fall into certain traps when writing Vue apps, so to go from beginner to advanced, you will need to understand them well and be able to handle them.

Memory leaks
------------

Memory leaks are a common performance issue in web applications. Even though Vue itself won’t cause memory leaks for no reason, it can happen by incorporating third-party libraries or writing faulty code. It’s especially important to avoid memory leaks when creating Single Page Applications (SPAs) because, by design, the users do not refresh their browser, so the app has to do all of the garbage collection.

Without going into too much detail, Vue has an official guide on how to [avoid memory leaks](https://vuejs.org/v2/cookbook/avoiding-memory-leaks.html). If you’re a developer who’s trying to master Vue, I highly suggest reading it.

Rendering costs
---------------

Front-end libraries and frameworks such as React and Vue are making us “lazy.” We don’t see exactly what’s going on when it comes to rendering. We just use a `v-for` and expect things to work. And that’s great — more power to us!

The problem is that it’s hard to understand how much rendering “costs.” There are many unexpected ways that a Vue application might have high rendering costs:

*   Too many DOM elements are being produced.
*   The page is being updated too frequently.
*   Third-party components are used that need a lot of time to render.

There are many possible scenarios where your app has high rendering costs, and as a result, your users will experience lag. In [this article](https://medium.com/better-programming/6-ways-to-speed-up-your-vue-js-application-2673a6f1cde4), I go a lot deeper into how you can handle performance issues in Vue.

Optimize event handling
-----------------------

This relates more to JavaScript than strictly Vue, but it’s important to note regardless. There are certain events that may be triggered too often. If you add a scroll listener or a `@mouseover` event, then the event handler may be called many times.

If the event handler doesn’t do a lot, then it might not be a problem. But if your event handler does a lot of computations and takes time to run, then it can cause serious slowdowns in your application. The reason why this happens is that scroll, mouseover, and other events can trigger the event handler dozens of times every second.

The solution to this is using a `throttle` or `debounce` function in your event handler that limits the number of times your event handler does actual computations. [Lodash](http://lodash.com/) includes both functions and provides an easy way to use them. I highly suggest trying it out.

Knowing about this will help you write better JavaScript for the browser in general, but since it’s an issue that can easily occur in Vue, it’s important to learn about it during your journey towards Vue mastery.

4\. Learn the Vue Ecosystem
===========================

To become advanced in Vue development, you’ll have to learn about the packages and components that make up the Vue ecosystem. Most applications will require at least one of the following, but to master the framework, I believe you should familiarize yourself with all three.

Vuex
----

Most modern front-end applications, especially SPAs, rely on some sort of state management. [Vuex](https://vuex.vuejs.org/) is the official state management library for Vue applications and integrates well with the official Vue dev tools.

It serves as a centralized store that all the components can access to fetch or mutate global application data. Components can and should have local data, but using state management is a must for applications as they become more complex and multiple components rely on the same global data.

Vue Router
----------

Using Vue without [Vue Router](https://router.vuejs.org/) might be rare, but I’ve seen it in certain projects. Since most people here will already be familiar with Vue Router, I won’t go into too much detail. I will just mention that learning `vue-router` is a must for creating SPAs, and SPAs are the way to go for most modern front-end applications.

Vue SSR
-------

To truly make yourself stand out, you should learn SSR by either using the official [Vue library](https://ssr.vuejs.org/) or by learning [Nuxt.js](https://nuxtjs.org/). The need for server-side rendering usually arises when the performance of a browser app starts degrading or when you can’t rely on the user’s device to handle the rendering and it’s preferable to do it on the server side. It helps optimize time-to-content — especially on slow devices or slow internet — and it’s also useful for SEO reasons.

Since most jobs and freelancing projects will require at least two of the three above, I believe learning them is a one-way street for Vue developers.

5\. Use Components the Right Way
================================

One of the things I see go wrong with inexperienced Vue developers is how they structure components. Many times, Vue applications contain just one or a few mega-components that do all the work. This, of course, is not the right way to structure your components.

The more experienced you become, the more you will realize the importance of structuring your application into smaller components where each one does one (or a few) things well. There are many reasons why using smaller components helps your application:

*   You can reuse small components throughout your application.
*   Your code is cleaner and more organized.
*   Vue can render child components more efficiently in `v-for` loops.

If you have a Vue interview coming up and you’re asked to do a test project, delivering an application that’s well-organized will surely impress your interviewers!

6\. Make Mixins Your Best Friends
=================================

I really love Mixins in Vue and use them throughout my projects. Unfortunately, I see many developers who don’t even use them and it’s a shame. Mixins allow you to:

*   Reuse code throughout your project.
*   Write code just once (DRY principle).
*   Refactor and maintain your code more easily.

Mixins offer a lot of freedom and you’re allowed to use them however you like. For example, you might have a group of components with similar features, so you might want to create a mixin that includes all of the common features, components, and computed properties. Or you might have certain actions, filters, or conditions that are used a lot throughout your application so you can create a small mixin to include them.

The possibilities are endless, but the lesson is clear: You need to start using mixins to become an advanced Vue developer.

7\. Learn Advanced Directives
=============================

Aside from `v-for` , `v-if`, and other common directives, Vue has some directives that are less common but still very useful to know.

v-once
------

You can use `v-once` to output a value once and make it non-reactive. This means that on subsequent changes, the value won’t be rendered again. This can help you optimize performance in certain scenarios:

<span v-once>{{ name }}</span>

Event directive modifiers
-------------------------

For `v-on` events, there are some very handy modifiers that you can use. One that I personally use often is `@click.prevent`, which automatically calls `preventDefault()` on the click event.

<a href="#" @click.prevent="processClick">Click me</a>

You can see a [full list of event modifiers](https://vuejs.org/v2/guide/events.html#Event-Modifiers) in the documentation.

Custom directives
-----------------

Vue allows you to register your own custom directives, as explained in the [documentation](https://vuejs.org/v2/guide/custom-directive.html). If you find yourself replicating the same behavior again and again throughout your application, it might make sense to create a custom directive that you can reuse.

Additionally, many third-party packages will introduce their own custom directives that you can use.

The key when it comes to custom directives is to only create them when you need them and avoid going overboard with custom directives that are used just once or twice.

Keep Practicing
===============

You can start by reading more about all of the concepts that I’ve outlined or you can read a section of the official documentation that you have not read. Read, learn, and make sure that you put in the practice. Even if you only make a small step towards Vue mastery today, it can go a long way if you keep it up consistently.