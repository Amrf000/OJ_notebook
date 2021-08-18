---
layout: post
title: Understanding and using Vuex for the first time
category: Vue
tags: [vue]
---

This is your **last** free member-only story this month.

[Sign up for Medium and get an extra one](https://medium.com/m/signin?operation=register&redirect=https%3A%2F%2Fitnext.io%2Funderstanding-and-using-vuex-for-the-first-time-85054c3f1b8f&source=-----85054c3f1b8f---------------------metered_view_3-----------)

Understanding and using Vuex for the first time
===============================================

[![Nihar Raote](/md_blog/public/assets/2021-08-18/1_VSBYX46Hde8Pt_M-9T3Jdw.jpeg)](https://medium.com/@NAPOLEON039?source=post_page-----85054c3f1b8f--------------------------------)

[Nihar Raote](https://medium.com/@NAPOLEON039?source=post_page-----85054c3f1b8f--------------------------------)

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fa715828b870b&operation=register&redirect=https%3A%2F%2Fitnext.io%2Funderstanding-and-using-vuex-for-the-first-time-85054c3f1b8f&user=Nihar%20Raote&userId=a715828b870b&source=post_page-a715828b870b----85054c3f1b8f---------------------follow_byline-----------)

[Nov 27, 2019](/understanding-and-using-vuex-for-the-first-time-85054c3f1b8f?source=post_page-----85054c3f1b8f--------------------------------) · 5 min read

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2F85054c3f1b8f&operation=register&redirect=https%3A%2F%2Fitnext.io%2Funderstanding-and-using-vuex-for-the-first-time-85054c3f1b8f&source=post_actions_header--------------------------bookmark_preview-----------)

A short intro to Vuex
=====================

Vuex is a state management library that can help us manage the state of our application. Instead of multiple components handling state locally and passing it to the required components, we can have Vuex manage state for the entire application in one location for us.

It is best used with Vuejs, but is not limited to it. For example, we can [use it with Reactjs](https://github.com/dennybiasiolli/react-vuex) if we wish. Vuex is quite powerful.

This short guide explains the basics of using Vuex in a Vuejs application. I will assume you have worked with Vue applications.

State management and the store
==============================

Vuex manages state in a central location called a _store_. Also called a Vuex store, this _store_ contains _state_ as well as some other things that are very useful and make Vuex so powerful. In order to use Vuex in our application, we need to create a Vuex store, register it in the entry file where our main Vue instance is and then we’ll be able to use it freely.

Creating a store and registering it doesn’t take more than a few steps:

![](/md_blog/public/assets/2021-08-18/1_uIAZpTc4TDkoUFAbwv-6gg.png)

Creating a Vuex store

We have created a Vuex store in a separate `store.js` file.

![](/md_blog/public/assets/2021-08-18/1_TVgGOsiNYGdvYnFqbWXzRA.png)

Registering the store with our Vue instance

Here we registered it with our global Vue instance. Now let’s put some state in it:

![](/md_blog/public/assets/2021-08-18/1_8cAY00Xu6fEnZt0KMQWGKQ.png)

Adding state in our store

The Vuex store takes an object as an argument. Inside this object will be the state and other methods. We can retrieve the state using the command: `this.$store.state` in a Vue component. We can retrieve our _count_ with `this.$store.state.count`. Here, `this.$store` refers to the Vuex store.

Getters
=======

If there are any calculations we need to perform on the state before we use it, we can do it in a computed property.

Let’s say we want to double the `count` variable in our state before we display it.

![](/md_blog/public/assets/2021-08-18/1__KHZfMr13Mu_EW2uboVH0A.png)

Although this works in this case, if there are complex calculations to be performed and/or they are needed in multiple components, then it becomes inefficient. We will either have to write duplicate functions for all those components or extract the calculations in a separate function and keep importing it everywhere.

Vuex offers a better alternative — `Getters`.

![](/md_blog/public/assets/2021-08-18/1_9h1JJq4mpxu1WZoj0RYHIA.png)

Adding getters to the store

`getSqCount` is an arrow function that serves as a getter. All getters receive the state as their first argument from Vuex. We do not need to explicitly pass it when we call them.

![](/md_blog/public/assets/2021-08-18/1_Ci6loN3W3JbKpqKO2n7gKA.png)

Using getters in the Vue component

> _Note that_ `_state_` _and_ `_getters_` _are keywords and you cannot use your own names for these in the Vuex store. This also applies to mutations and actions that will follow._

Mutations
=========

We’ve set state in the store and we’ve retrieved it. To make changes in our state, we need to use something called a `Mutation`.

A mutation is similar to an event handler function. The main work of changing (mutating) state will be done inside this function.

![](/md_blog/public/assets/2021-08-18/1_HfwL7wNB_dzLlhcZ_s4svQ.png)

Adding a mutation to the store

The mutation handler function also receives the state as the first argument. As for why I said it’s similar to an event handler, it is because of how this mutation is invoked.

Even though it looks like a regular function, we do not call a mutation directly. Think of it more like an event registration. If we want to use the `increment` mutation we defined inside our store, we have to _commit_ it. We do this in the Vue component.

![](/md_blog/public/assets/2021-08-18/1_UuLQaP4XYNyjiY7v-1oK2w.png)

Using the mutation

When this method is executed, it will _commit_ a mutation called `increment`. Like how an action triggers an event and then the event handler function is executed, when the `add()` method on our Vue component is executed, it commits the `increment` mutation which is invoked.

You can also pass some data along with invoking the mutation handler.

![](/md_blog/public/assets/2021-08-18/1_-_FnZnxI8-XhJ_YxXN7mSg.png)

Passing data/payload to the mutation handler

This data or _payload_ can be used like any other function argument by our mutation handler.

![](/md_blog/public/assets/2021-08-18/1_22VehRE-GzSYKiRH5xzNcQ.png)

Our mutation using the data we passed

Mutations allow us to update the state. Any components that depend on this state will be updated automatically when this state updates.

But, mutations only allow for synchronous operations. However, asynchronous operations can still be performed with the help of `Actions`.

Actions
=======

Actions are similar to mutations but they don’t change the state directly as mutations do. Instead, they carry out asynchronous operations and then commit mutations when those operations are finished.

We can register an action on our Vuex store in the following way:

![](/md_blog/public/assets/2021-08-18/1_xDy1Lytp86OdoRUKOoonlw.png)

Registering an action on our Vuex store

Here we simulate an asynchronous operation with the help of `setTimeout`.

Registering an action gives our action handler ( `incrementAsync`) access to a `context` object.

The `context` object exposes the same set of methods and properties that the store instance does (this is the `this.$store` that we used before). We can call `context.commit` to commit a mutation or even use `context.getters` to access getters. But, using the context object is not the same as using the store instance.

Since we will be using the `context.commit` method the most, we can use [argument destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to unpack it so we can use it easily.

![](/md_blog/public/assets/2021-08-18/1_kxsJb-tYXOAoQTpDV-cs4A.png)

Using argument destructuring to unpack the commit method

Like how we _commit_ mutations in our Vue components, we _dispatch_ actions.

![](/md_blog/public/assets/2021-08-18/1_68n2r0KLpiRMcb7eKYSaPw.png)

Use the action in a Vue component

This works the same way as it did when we used this for commiting our mutation, except this time, we are dispatching an action.

Wrapping up
===========

This should be enough for you to create your first Vuex store, define state, mutations and actions in it. If you need more examples or more information you can read the [Vuex docs](https://vuex.vuejs.org/guide/). They are really good and not too complex. I have also written an article on Vuex before, [give it a read](https://dev.to/napoleon039/when-why-and-how-to-use-vuex-9fl) if you’re interested.

In my next article, I’ll explain mapping getters, mutations and actions to computed properties. Thank you for reading!

Feel free to post any questions and suggestions you have in the comments 😃

_Originally published at_ [_dev.to_](https://dev.to/napoleon039/understanding-and-using-vuex-for-the-first-time-2ngi)_._