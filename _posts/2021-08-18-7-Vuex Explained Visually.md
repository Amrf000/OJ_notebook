---
layout: post
title: Vuex Explained Visually
category: Vue
tags: [vue]
---

Vuex Explained Visually
=======================

[![Adam Jahr](/md_blog/public/assets/2021-08-18/1_X_KFqGqc6lZ3yybxQEBmuQ.png)](/@adamjahr?source=post_page-----f17c8c76d6c4--------------------------------)

[Adam Jahr](/@adamjahr?source=post_page-----f17c8c76d6c4--------------------------------)

Follow

[Nov 13, 2018](/vue-mastery/vuex-explained-visually-f17c8c76d6c4?source=post_page-----f17c8c76d6c4--------------------------------) · 5 min read

[](/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Ff17c8c76d6c4&operation=register&redirect=https%3A%2F%2Fmedium.com%2Fvue-mastery%2Fvuex-explained-visually-f17c8c76d6c4&source=post_actions_header--------------------------bookmark_preview-----------)

![](/md_blog/public/assets/2021-08-18/1_RmXMYqp-2TpQqC-TTwnejA.png)

Managing state in an application full of components can be difficult. Facebook discovered this the hard way and created the Flux pattern, which is what Vuex is based upon. Vuex is Vue’s own state management pattern and library.

In this tutorial from Vue Mastery’s [Mastering Vuex](https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex) course, we’ll look at why an application might need Vuex, and how it can enhance your app.

A lesson from Mastering Vuex- full course at VueMastery.com

⚠️ The Case for State Management
================================

When we talk about state, we mean the data that your components depend on and render. Things like blog posts, to-do items, and so on. Without Vuex, as your app grows, each Vue component might have its own version of state.

![](/md_blog/public/assets/2021-08-18/0_Z4BWPeaDXOob_qFs.png)

But if one component changes its state, and a distance relative component needs access to that new state value, we need a way for these two components to communicate.

We could communicate that state up the component tree using events, and communicate it back down the tree by passing along props… but that can become overly complicated as our app scales.

![](/md_blog/public/assets/2021-08-18/0_UeFfKsm6fvgtXoKz.png)

Over time, this “family tree” of components may get quite large, creating a mental mess trying to maintain and track the state throughout your growing application.

Instead of each of our components having its own local state, we can consolidate **all** of our state into one place. One global location that contains the current state of our entire application.

One **single source of truth**.

**Global State: A Single Source of Truth**
------------------------------------------

Vuex provides that single source of truth for us. As we begin to store state within it, our state becomes a lot cleaner, and a lot easier to reason about. Now, every component that relies on our Global State can have direct access to it. No more jumbled mess of passing state up, over, and down.

Because Vuex is written with Vue, **Vuex State is reactive** — just like the Vue instance’s data.

When one component updates the Vuex State, other components can be listening for when that State changes, then they can reactively respond based off that state-change (and the new State value they receive).

![](/md_blog/public/assets/2021-08-18/0_p45Yk1OoJkXFTFjy.png)

But just consolidating state into a single source of truth doesn’t fully solve the problems of State Management. For example, what happens when many components alter the State in different ways, from different locations?

Changes to our State could be unpredictable and untraceable. We need some more standardization.

**A State Management Pattern**
------------------------------

This is why Vuex provides a full state management pattern for a simple and standardized way to make state changes. And if you’re familiar with Vue, Vuex should look quite similar.

![](/md_blog/public/assets/2021-08-18/0_tnE4Xhot4A2XGZNT.png)

Just as Vue provides a root Vue instance created with `new Vue`, Vuex offers a store created with `new Vuex.Store`.

While the Vue instance has a _data_ property, the Vuex store has **State**. Both are reactive.

And while the instance has _methods_, which among other things can update data, the Vuex store has **Actions**, which can help handle updating the State.

And while the instance has _computed properties_, the Vuex store has **Getters**, which allow us to access filtered, derived, or computed State.

The difference with the Vuex store is that it also has **Mutations**. The reason I said Actions “can _help_ handle updating the State” is because Actions are essentially methods that call (or commit) **Mutations**. And **Mutations** are what actually update the Vuex State.

Mutations also allow us to _track_ our State changes. And if we are using the Vue DevTools, in the Vuex tab we can even get a time-stamped record of all the Mutations that were committed throughout the lifecycle of our app. This is called **time-travel debugging**, and the DevTools even show us what the State was at those given points in time.

Mutations within Actions
------------------------

Putting our Mutations within Actions allows us to wrap some business logic around our Mutation calls.

For example: We might want to run some conditional logic to determine whether a State change needs to happen or not… If not, we might not run the Mutation. We might even default to a second Mutation instead. So as you can see, Actions allow us to wrap multiple mutations within the same logic. This is essentially our way to give Vuex the logic it needs to determine how it’s handling our State changes at the application level.

A Vuex Store
------------

Now let’s take a look at an example Vuex Store:

![](/md_blog/public/assets/2021-08-18/1_7PdgBj12sBfqsruoohda1A.png)

In our **State**, we have a loadingStatus property, along with an array for todos.

Below that, the SET\_LOADING\_STATUS **Mutation** allows us to update our loadingStatus State. And the SET\_TODOS **Mutation** sets our State with the todos that we’ll receive from an API call in our Action below.

Our **Action** here has multiple steps:

First, it’ll commit the SET\_LOADING\_STATUS Mutation to set the loadingStatus to ‘loading’.

Then it’ll make an API call…

…and when the response returns, it will commit the SET\_LOADING\_STATUS Mutation again to set the isLoading status to ‘notLoading’.

Finally it’ll commit the SET\_TODOS Mutation to set the state of our todos equal to the response we got back from our API.

![](/md_blog/public/assets/2021-08-18/1_YyAzxZauX0gU6PjYkFkMvw.png)

Now, if we needed the ability to only retrieve the todos that are labeled done, we can use a Getter for that, which can be programmed to filter our todos State and retrieve only the specific state that we want.

Now that we’ve explored the Vuex pattern, let’s look at it in motion.

Vuex in Motion
==============

![](/md_blog/public/assets/2021-08-18/0_5BcWxyQW7ai1JsVd.gif)

To Continue Learning…
=====================

Hopefully you now see the power of Vuex and how it can enhance your application by providing a single source of truth for your State, along with a full State Management pattern including Actions, Mutations and Getters. To continue learning, check out our full [Mastering Vuex](https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex) course at VueMastery.com.

You can also head over to the official [Vuex docs](https://vuex.vuejs.org/), and you can subscribe for more content below:

_Originally published at_ [_www.vuemastery.com_](https://www.vuemastery.com/courses/mastering-vuex/intro-to-vuex)_._