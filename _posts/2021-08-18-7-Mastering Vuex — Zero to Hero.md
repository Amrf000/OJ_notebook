---
layout: post
title: Mastering Vuex — Zero to Hero
category: Vue
tags: [vue]
---

Mastering Vuex — Zero to Hero
=============================

[![Sanath Kumar](/md_blog/public/assets/2021-08-18/0_PVNAdCWaHsElI0ns_.jpg)](/@msanathkumar?source=post_page-----e0ca1f421d45--------------------------------)

[Sanath Kumar](/@msanathkumar?source=post_page-----e0ca1f421d45--------------------------------)

Follow

[Jul 23, 2018](/dailyjs/mastering-vuex-zero-to-hero-e0ca1f421d45?source=post_page-----e0ca1f421d45--------------------------------) · 7 min read

[](/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Fe0ca1f421d45&operation=register&redirect=https%3A%2F%2Fmedium.com%2Fdailyjs%2Fmastering-vuex-zero-to-hero-e0ca1f421d45&source=post_actions_header--------------------------bookmark_preview-----------)

![](/md_blog/public/assets/2021-08-18/1_e0QaKNqJ3A465rLrnGGMgA.jpeg)

Original photo by [Nikita Kachanovsky](https://unsplash.com/photos/OVbeSXRk_9E?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/search/photos/computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

![](/md_blog/public/assets/2021-08-18/1_4877k4Hq9dPdtmvg9hnGFA.jpeg)

The official documentation of Vuex defines it as a **state management pattern** + library for Vue.js applications. _But what does this mean? What is a state management pattern?_

Imagine working on a large web app with hundreds of routes and components. Wouldn't it be easier if we could store all the data we ever need inside the app, in one centralized storage location?

![](/md_blog/public/assets/2021-08-18/1_HWBipJ4YFcEGrBoJA3jhuQ.jpeg)

Every component or route inside our application will request data from the Vuex state and commits modified data back to the state.

In essence, the Vuex state can be viewed as a single source of truth for the entire application.

Data is stored inside the state as a single JSON object. For example :

state : {  
    name : “John Doe”,  
    age : “28”,  
}

But how can our components and routes access the data stored in our state? We define **Getters** inside our Vuex store which returns the data from our store back to our components. Let’s see how a simple **Getter**, to retrieve the name stored in our state looks like.

getters : {  
  NAME : state => {  
    return state.name  
  }  
}

Notice that, we have capitalized the name of the getter. This is just a recommended coding convention and it’s not absolutely necessary for you to follow the same if you are not a fan of it.

Now that we have defined a getter for the name, it’s incredibly easy to fetch the value of name inside our component, as shown in the snippet below.

let name = this.$store.getters.NAME

We have figured out how to **get** data from the state, let’s see how we can **set** data into our state. We define setters, right? Except, Vuex setters are named slightly different. We define **a Mutation** to set data into our Vuex state.

mutations : {  
  SET\_NAME : (state,payload) => {  
    state.name = payload,  
  }  
}

What the heck is a payload? A **payload** is simply the data passed to our mutation from the component committing the mutation. How do we do that ? Simple…

this.$store.commit(“SET\_NAME”,your\_name)

This snippet of code will mutate the state and set whatever value that is assigned to your\_name, to the name property inside our Vuex state.

> Mutations are synchronous

Imagine we have a list of names, stored in a database on a remote server. The server provides us an API endpoint that returns an array of names, which can be consumed in our Vue.js application. Of course, we can use **Axios** to make a get request to the API endpoint and retrieve the data.

let { data } = await Axios.get(‘https://myapiendpoint.com/api/names')

We could then commit the returned array in to our Vuex store via mutation. Simple.. right? Well, not so much. Mutations are synchronous and we cannot run asynchronous operations such as API calls inside a mutation.

So what do we do now. ? We create **Actions.**

Actions are similar to mutation, but instead of mutating the state directly they commit a mutation. Confused? Let’s inspect an action declaration.

actions : {  
  SET\_NAME : (context,payload){  
     context.commit("SET\_NAME",payload);  
  }  
}

We have defined an action called SET\_NAME which accepts context and payload as parameters. The action commits the mutation SET\_NAME created earlier with the payload passed to it, that is **your\_name**.

Now instead of committing the mutation directly, our components dispatch an action SET\_NAME, with the new name as payload as follows:

this.$store.dispatch("SET\_NAME",your\_name)

The action then commits the mutation with the payload passed to it, that is your\_name.

But why ?
---------

You might be wondering why an action declaration is required when we could simply commit our mutations with the new value directly from our components. As mentioned above mutations are synchronous but actions are not.

In the above example, consider a case when you have to update the value of name, not just in your state but also on a database running on a remote server. I am pretty sure this is how you are going to use Vuex in a real project 99% of the time. Take a look at the following code snippet.

The code itself is self-explanatory. We use Axios to post the name to an API end-point. If the POST request is successful that is the value of the field name has been successfully changed in the server, we commit the SET\_ NAME mutation to update the value of name inside our state as well.

> Make it a practice to never commit your Mutations directly. Always use Actions to commit your mutations

Setting up a Vuex store in Vue.JS
---------------------------------

Let’s dive in deeper and learn how we can actually implement Vuex in a real application.

**Setp 1. Install Vuex**

npm install --save vuex

**Step 2. Creating a Vuex Store**

1.  Create a folder named **store** inside your root directory.
2.  Create an **index.js** file inside the newly added store folder and use the snippet below to create a new store.

**Step 3. Add Vuex store to our Vue.Js application**

1.  Import the **store** inside main.js file.

import { store } from './store'

2\. Attach the **store** to our Vue instance as shown below.

new Vue({  
  el: '#app',  
 ** _store_**,  
  router,  
  render: h => h(App)  
})

And we are done. Now we can add **state variables**, **getters**, **mutations** and **actions** inside our Vuex store.

**An Example**
--------------

Take a look at the Vuex store of a simple to-do list application. “Not another TODO list !!” Right? Well, don’t worry. By the end of this article, you will be well equipped to use Vuex in all its might and glory.

Adding a new item to the to-do list
-----------------------------------

Inside your component, dispatch an action **SAVE\_TODO** with the to-do item as payload as shown in the code snippet below.

let item = "Get groceries"  
this.$store.dispatch('SAVE\_TODO',item)

The action **SAVE\_TODO** makes a POST request to your API end-point and then commits a **mutation ADD\_TODO**, which pushes the to-do list item to the state variable **todos**.

Fetching your to-do list
------------------------

Inside the **mounted()** block in your component, dispatch the second action **GET\_TODO**, which fetches all the to-do items from your API end-point and saves it to the state variable todos, by committing a mutation SET\_TODO

mounted(){  
    this.$store.dispatch('GET\_TODO')  
}

Accessing the to-do list inside your component
----------------------------------------------

Create a computed property as shown in the snippet below, to access the todos item inside your component.

computed : {  
  todoList(){  
     return this.$store.getters.TODOS  
  }  
}

Inside your component you can access the computed property as shown below.

<div class="todo-item" v-for="item in todoList"></div>

Using Map Getters method
------------------------

There is an even simpler way of accessing your todos list inside you component using the mapGetters method provided by Vuex.

import {mapGetters} from 'vuexcomputed : {  
...mapGetters(\['TODOS'\]),  
  //Other computed properties  
}

You might have already guessed this, but the code inside your template definition have to modified as shown in the snippet below.

<div class="todo-item" v-for="item in TODOS"></div>

Notice how we have used the ES6 spread operator \[ **…** \] inside our computed properties.

> A Vuex store is not just a single source of truth in your application, it is also designed to be that single point which should alter this truth.

This needs a little bit of explanation. We already learned to define Actions to **get** and **set** the todos item in our state. What if we had to update the item and mark it complete ? Where do we run the code for this ?

You might find contrasting opinions on the subject all over the Internet, and there is no clear guidelines specified in the documentation as well.

I would recommend keeping all your API calls inside **Actions** in your Vuex store. This way every change that gets committed to your state only comes from inside the store and makes it easier for you to debug and make the code easier to understand. It also has the added benefit of making edits in your code easier.

Now, how do we delete and update an item from the todos list ? Try implementing an action and mutation to update and remove items from your todos list and let me know in the comments below.

Organizing your code
--------------------

Saving all your state variables, getters, actions, and mutations in one single file will quickly become cumbersome once you start working on medium to large sized real-world applications. Let’s see how we can organize our store into multiple files as modules.

Create a new folder inside your store called modules. Add a new file called **todos.js** inside the modules folder.

const state = {}  
const getters = {}  
const mutations = {}  
const actions = {}export default{  
    state,getters,mutations,actions  
} 

Now you can move your state variables, getters, mutations and actions from **index.js** into **todos.js** file. Don’t forget to import **Axios**. All we need to do now is let Vuex know we have created a store module and where to find it. Your new index.js file should look something like this.

And your **todos.js** file will be as shown in the gist below.

Important Takeaways
-------------------

1.  The state of your app is stored as a single large JSON object.
2.  **Getters** are used to access values stored in your state.
3.  **Mutations** update your state. It is to be remembered that mutations are synchronous.
4.  All asynchronous operations must be executed inside **Actions**. Actions alter the state by committing a mutation.
5.  Make it a practice to always commit a **Mutation** only through an **Action**.
6.  **Modules** can be used to organize your store into multiple smaller store files.

![](/md_blog/public/assets/2021-08-18/1_4877k4Hq9dPdtmvg9hnGFA.jpeg)

Vuex makes working with Vue so much easier and fun. If you are a beginner there might be instances where it’s tough for you to decide if you need to use Vuex or not in certain areas of your application. Follow your gut. You will be up-to-speed pretty quick.