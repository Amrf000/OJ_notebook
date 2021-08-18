---
layout: post
title: Understand Routing in Vue.js With Examples
category: Vue
tags: [vue]
---

Understand Routing in Vue.js With Examples
==========================================

[![SaidHayani@](https://miro.medium.com/fit/c/56/56/0*7Y6TXmnkRoY7C7dt.jpg)](/?source=post_page-----6da96979c8e3--------------------------------)

[

SaidHayani@

](/?source=post_page-----6da96979c8e3--------------------------------)

[

Jun 7, 2018·9 min read

](/understand-routing-in-vue-js-with-examples-6da96979c8e3?source=post_page-----6da96979c8e3--------------------------------)

[](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2F6da96979c8e3&operation=register&redirect=https%3A%2F%2Fsaidhayani.medium.com%2Funderstand-routing-in-vue-js-with-examples-6da96979c8e3&source=post_actions_header--------------------------bookmark_preview-----------)

[

![](https://miro.medium.com/max/1400/1*ckpJ83fx62uqbRGUcaRrkw.jpeg)

](https://www.zeolearn.com/magazine/understand-routing-in-vuejs-with-examples)

Zeolearn copyright

![](https://miro.medium.com/max/1154/1*J3w5uzszgJjjYAgedAp6GQ.gif)

> Vue.js is a great JavaScript Framework created by [Evan You](https://twitter.com/youyuxi) ,it’s used to build Single web page and flexible components ,and it’s the most skill required in Front End Web development ,you can learn more about Vue.js [here](https://vuejs.org/) .

[Vue.js](https://vuejs.org/) provide bunch of features to build a reusable web components,Routing is one of those methods,it allow user switch between pages without page refreshing the thing that make the navigation easy and really nice in your web application ,so in this Article we are going to explain how Vue.js Routers work by building a Vue- template as example .

So, let’s **get started with our Vue.js Router** project by installing and creating a new [Vue.js](https://www.zeolearn.com/magazine/why-must-you-choose-vuejs-over-reactjs) project. We need to have node.js installed. We shall be using [vue-cli](https://github.com/vuejs/vue-cli) to generate a new Vue.js project. Follow the steps given below-

Type the following code in your terminal run:

vue init webpack vue-router//  
cd vue-router  
//  
npm run dev

Browse to [http://localhost:8080](http://localhost:8080)

![](https://miro.medium.com/max/60/1*pMSEqVQJLoUBamg7lYPOVA.png?q=20)

![](https://miro.medium.com/max/700/1*pMSEqVQJLoUBamg7lYPOVA.png)

![](https://miro.medium.com/max/1400/1*pMSEqVQJLoUBamg7lYPOVA.png)

Open the app in your text editor, inside components folder open `HellowWorld.vue` file and follow these steps:

\-rename `HellowWorld.vue` with `home.vue` ,remove all the code and replace it with this one .

<template>  
  <div class="home">  
    <h1>Home</h1>  
  </div>  
</template><script>  
export default {  
  name: 'home',  
  data () {  
    return {  
      msg: 'Welcome to Your Vue.js App'  
    }  
  }  
}  
</script><!-- Add "scoped" attribute to limit CSS to this component only -->  
<style scoped></style>

\-And go to `index.js` inside **router** folder and replace `HelloWorld` with `home`

import Vue from 'vue'  
import Router from 'vue-router'  
import home from '@/components/home'Vue.use(Router)export default new Router({  
  routes: \[  
    {  
      path: '/',  
      name: 'home',  
      component: home  
    }  
  \]  
})

`App.vue` file should look like this !

<template>  
  <div id="app">  
      
    <router-view/>  
  </div>  
</template><script>  
export default {  
  name: 'App'  
}  
</script><style>  
#app {  
    
}  
</style>

And Now let’s write our code !!

We are now going to add a [Bootswatch](https://bootswatch.com/) template. You can choose any template you like. I shall choose a [Cosmo](https://bootswatch.com/cosmo/), click Ctrl + U to view code source and just copy the `Navbar`, we just need navbar, and paste this code into App.vue component.

Here we are 😃

![](https://miro.medium.com/max/60/1*dyb8NLvPykux3UmHVMCTIg.png?q=20)

![](https://miro.medium.com/max/700/1*dyb8NLvPykux3UmHVMCTIg.png)

![](https://miro.medium.com/max/1400/1*dyb8NLvPykux3UmHVMCTIg.png)

The next is we gonna create 3 other components `Blog`,`Services` and `Contact`

Inside the components folder create new file and name it with `blog.vue` and push this code into it

<template>  
 <div class="blog">  
  <h1>{{blog}}</h1>  
 </div>  
</template>  
<script>  
 export default{  
  name:'blog',  
  data (){  
   return{  
    title:'Blog'  
   }  
  }  
 }  
</script><style scoped>  
   
</style>

If you want to do the same thing for the service and contact component, you must have these files in your component folder:

*   home.vue
*   blog.vue
*   services.vue
*   contact.vue

Routers config
==============

Now after having four components, we need to configure the routers so that we can navigate between these components.

So How we can navigate to each components using the routers?

We need to learn the rule of Routing. Now, we have to do some modifications inside the router folder, open `index.js`

![](https://miro.medium.com/freeze/max/60/1*UmueZU7FLF21xcXRHpJWzg.gif?q=20)

![](https://miro.medium.com/max/580/1*UmueZU7FLF21xcXRHpJWzg.gif)

![](https://miro.medium.com/max/1160/1*UmueZU7FLF21xcXRHpJWzg.gif)

*   First, import your components into index.js

Import all the components using `import` method.

import home from '@/components/home'  
import blog from '@/components/blog'  
import services from '@/components/services'  
import contact from '@/components/contact'

*   Second import vue and Router module from [vue-router](https://router.vuejs.org) module

import Vue from 'vue'  
import Router from 'vue-router'// use router  
Vue.use(Router)

if you have installed vue with vue-cli, you will have [vue-router](https://router.vuejs.org/) module imported by default

*   Finally, inside the router folder, we have to configure the Routers to make it work. and The Router method takes an Array of objects that takes each component’s properties:

export default new Router({  
  routes: \[  
    {  
      path: '/',  
      name: 'home',  
      component: home  
    },  
    {  
      path: '/blog',  
      name: 'blog',  
      component: blog  
    },  
    {  
      path: '/services',  
      name: 'services',  
      component: services  
    },  
    {  
      path: '/contact',  
      name: 'contact',  
      component: contact  
    }  
  \]  
})

*   `path` : mean the path of the component
*   `name`: name of the component
*   `component` : the view component

To make any component as the default component set slash(‘/’) to the path property,

path:'/'

In our example, we set the home page as default page.now when you open the project in the browser the first page will appear is the home page.

{  
path:'/',  
name:'home',  
component:home  
}

The vue-router has more advanced parameters and methods, but we are not jumping into this section in this meantime, and this is the list of properties and method that you can use with vue-router :

*   [Nested routers](https://router.vuejs.org/en/essentials/nested-routes.html)
*   [Named view](https://router.vuejs.org/en/essentials/named-views.html)
*   [Redirect and Alias](https://router.vuejs.org/en/essentials/redirect-and-alias.html)
*   [Navigation Guard](https://router.vuejs.org/en/advanced/navigation-guards.html)
*   [Router instance](https://router.vuejs.org/en/api/router-instance.html)

Now you can browse to any components by typing the name of the component!!

![](https://miro.medium.com/freeze/max/60/1*fN3T5aesSsYfqs_rH5FhrQ.gif?q=20)

![](https://miro.medium.com/max/1150/1*fN3T5aesSsYfqs_rH5FhrQ.gif)

router-link
===========

Now we are going to make the navigation through the Navbar that we created using the router-link element.

To do that we should replace `</a>` element by ‘<router-link></router/link>’ like this:

<li class="nav-item">  
  <router-link class="nav-link" to="/blog">Blog</router-link>  
</li>  
<li class="nav-item">  
  <router-link class="nav-link" to="/services">Services</router-link>  
 </li>  
<li class="nav-item">  
   <router-link class="nav-link" to="/contact">contact</router-link>  
 </li>

The router-link take `to='path'` attribute that take the path of the component as value.

Router-view
===========

You will find `<router-view>` tag in the`App.vue` file, it’s basically the view where the components are rendered, it’s like the main div that contain all the components and it return the component that matches the current route, we will have a discussion with `route-view` in the next part when we use animation transition.

Using the parameters inside the routers
=======================================

At this part we will use parameters to navigate to specific components, the parameters make The Routing dynamic.

To work with parameters we are gonna create a list of product, and an array of data, so when you click on the link of any product it will gonna take us to the page details through a parameter.

At this situation, we are not going to use a database or API to retrieve products data, so what have to do is create an Array of products that we suppose to be a database.

Inside `home.vue` component put the Array within data() method just like this:

export default {  
  name: 'home',  
  data () {  
    return {  
      title: 'Home',  
      products:\[  
      {  
        productTitle:"ABCN",  
        image       : require('../assets/images/product1.png'),  
        productId:1  
      },  
      {  
        productTitle:"KARMA",  
        image       : require('../assets/images/product2.png'),  
        productId:2  
      },  
      {  
        productTitle:"Tino",  
        image       : require('../assets/images/product3.png'),  
        productId:3  
      },  
      {  
        productTitle:"EFG",  
        image       : require('../assets/images/product4.png'),  
        productId:4  
      },  
      {  
        productTitle:"MLI",  
        image       : require('../assets/images/product5.png'),  
        productId:5  
      },  
      {  
        productTitle:"Banans",  
        image       : require('../assets/images/product6.png'),  
        productId:6  
      }  
      \]  
    }  
  }  
}

Then fetch and loop into Products Array using `v-for` directive .

<div class="row">  
      <div class="col-md-4 col-lg4" v-for="(data,index) in products" :key="index">  
        <img :src="data.image" class="img-fluid">  
         <h3>{{data.productTitle}}</h3>  
      </div>  
    </div>

The Result:

![](https://miro.medium.com/max/60/1*bqknyA8lwa42wYzN6HVYaQ.png?q=20)

![](https://miro.medium.com/max/1400/1*bqknyA8lwa42wYzN6HVYaQ.png)

To navigate to details component we have first to add a click event

<h3 [@click](http://twitter.com/click)\="goTodetail()" >{{data.productTitle}}</h3>

Then add methods

methods:{  
  goTodetail() {  
    this.$router.push({name:'details'})  
  }

if you click the title it will return undefined because we didn’t create the details component yet so let’s create one:

**details.vue**

<template>  
 <div class="details">  
  <div class="container">  
   <h1 class="text-primary text-center">{{title}}</h1>  
  </div>  
 </div>  
</template>  
<script>  
 export default{  
  name:'details',  
  data(){  
   return{  
    title:"details"  
   }  
  }  
 }  
</script>

Now we can navigate without getting an error 😃

![](https://miro.medium.com/freeze/max/60/1*VlW07YlSysTIkpXjDpb7Ng.gif?q=20)

![](https://miro.medium.com/max/1152/1*VlW07YlSysTIkpXjDpb7Ng.gif)

Now how we can browse to the details page and get the matched data while we don’t have a database ?

We gonna use the same products Array in details component, so we can match the id that comes from the URL

products:\[  
      {  
        productTitle:"ABCN",  
        image       : require('../assets/images/product1.png'),  
        productId:1  
      },  
      {  
        productTitle:"KARMA",  
        image       : require('../assets/images/product2.png'),  
        productId:2  
      },  
      {  
        productTitle:"Tino",  
        image       : require('../assets/images/product3.png'),  
        productId:3  
      },  
      {  
        productTitle:"EFG",  
        image       : require('../assets/images/product4.png'),  
        productId:4  
      },  
      {  
        productTitle:"MLI",  
        image       : require('../assets/images/product5.png'),  
        productId:5  
      },  
      {  
        productTitle:"Banans",  
        image       : require('../assets/images/product6.png'),  
        productId:6  
      }  
      \]

First, we have to set the id to `goTodetail()` method as parameter,

<h3 [@click](http://twitter.com/click)\="goTodetail(data.productId)" >{{data.productTitle}}</h3>

Then add a second parameter to the router method,

The $router method takes two parameters, first the `name` of the component, we want to navigate and the second parameter is the the `id` or any other parameter.

this.$router.push({name:'details',params:{Pid:proId}})

Add Pid as parameter in **index.js** inside `router` folder

{  
      path: '/details/:Pid',  
      name: 'details',  
      component: details  
    }

**home.vue**

methods:{  
  goTodetail(prodId) {  
    this.$router.push({name:'details',params:{Pid:proId}})  
  }  
  }

![](https://miro.medium.com/freeze/max/60/1*COQTCGCvd5N6J8JVAGBG6Q.gif?q=20)

![](https://miro.medium.com/max/1158/1*COQTCGCvd5N6J8JVAGBG6Q.gif)

To get the matched parameter use this line of code:

this.$route.params.Pid

**details.vue**

<h2>the product id is :{{this.$route.params.Pid}}</h2>

Then loop through products Array in `detalils.vue` and check the object that matches the parameter Pid and returns it data.

<div class="col-md-12" v-for="(product,index) in products" :key="index">  
     <div v-if="proId == product.productId">  
      <h1>{{product.productTitle}}</h1>  
      <img :src="product.image" class="img-fluid">  
     </div>  
    </div>///  
export default{  
  name:'details',  
  data(){  
   return{  
    proId:this.$route.params.Pid,  
    title:"details"  
     }  
}

You see now when we click any product’s link it gets us to the same product!

![](https://miro.medium.com/freeze/max/60/1*vFC4qDiz2L7quvCVU429Ng.gif?q=20)

![](https://miro.medium.com/max/1152/1*vFC4qDiz2L7quvCVU429Ng.gif)

**detail.vue** component!

<template>  
 <div class="details">  
  <div class="container">  
   <div class="row">  
    <div class="col-md-12" v-for="(product,index) in products" :key="index">  
     <div v-if="proId == product.productId">  
      <h1>{{product.productTitle}}</h1>  
      <img :src="product.image" class="img-fluid">  
     </div>  
    </div>  
   </div>  
  </div>  
 </div>  
</template>  
<script>  
 export default{  
  name:'details',  
  data(){  
   return{  
    proId:this.$route.params.Pid,  
    title:"details",  
    products:\[  
    {  
    productTitle:"ABCN",  
    image       : require('../assets/images/product1.png'),  
    productId:1  
    },  
    {  
    productTitle:"KARMA",  
    image       : require('../assets/images/product2.png'),  
    productId:2  
    },  
    {  
    productTitle:"Tino",  
    image       : require('../assets/images/product3.png'),  
    productId:3  
    },  
    {  
    productTitle:"EFG",  
    image       : require('../assets/images/product4.png'),  
    productId:4  
    },  
    {  
    productTitle:"MLI",  
    image       : require('../assets/images/product5.png'),  
    productId:5  
    },  
    {  
    productTitle:"Banans",  
    image       : require('../assets/images/product6.png'),  
    productId:6  
    }  
    \]  
       
   }  
  }  
 }  
</script>

The transition
==============

![](https://miro.medium.com/freeze/max/60/1*pgS0n47rJkVOzjBrNk5h7w.gif?q=20)

![](https://miro.medium.com/max/1160/1*pgS0n47rJkVOzjBrNk5h7w.gif)

In this part we are going to add an animation transition to component animated, will animate the transition of the components, it makes the navigation awesome and it creates some kind of UX and UI, so make an animation while the transition, put the “<router-view>” inside “<transition/>” tag and give it a name of class .

**App.vue**

<transition name="moveInUp">  
         <router-view/>  
  </transition>

To animate the transition of the component when it enters the view add `enter-active` to the name given to the transition tag, and in the leave add `leave-active` and then give it The CSS transition properties just like this below!

.moveInUp-enter-active{  
  opacity: 0;  
  transition: opacity 1s ease-in;  
}

**Using CSS3 animation :**

Now we are gonna animate using @keyframes in CSS3

**A**\- when the component enters the view

Add fade effect to the view when the component enters.

.moveInUp-enter-active{  
  animation: fadeIn 1s ease-in;  
}  
[@keyframes](http://twitter.com/keyframes) fadeIn{  
  0%{  
    opacity: 0;  
  }  
  50%{  
    opacity: 0.5;  
  }  
  100%{  
    opacity: 1;  
  }  
}

![](https://miro.medium.com/freeze/max/60/1*xRVdi3iiK8PowUjsPhI_kQ.gif?q=20)

![](https://miro.medium.com/max/1158/1*xRVdi3iiK8PowUjsPhI_kQ.gif)

**B**\- when the component leaves the view

Now we gonna make the component move in up when it leaves the view!

.moveInUp-leave-active{  
  animation: moveInUp .3s ease-in;  
}  
[@keyframes](http://twitter.com/keyframes) moveInUp{  
 0%{  
  transform: translateY(0);  
 }  
  100%{  
  transform: translateY(-400px);  
 }  
}

![](https://miro.medium.com/freeze/max/60/1*WY6Ej1YtF99oKiDP_KsDXA.gif?q=20)

![](https://miro.medium.com/max/1158/1*WY6Ej1YtF99oKiDP_KsDXA.gif)

As you see now you can create your own animation and transition for your components.

That’s it we are done!

You can Download the Source code [**here**](https://github.com/hayanisaid/Vue-router) **.**

Wrapping and Conclusion
=======================

Routing in Vue.js makes your app so much awesome when it comes to navigation and it gives it that energies of the single page web application and it create a better user experience.

You want to learn Bootstrap 4 check out my class on Skillshare with this [**referral link**](https://skl.sh/2ssg1nj) and get 2 free month access to 20000 class.

[_Originally published on zeolearn.com_](https://www.zeolearn.com/magazine/understand-routing-in-vuejs-with-examples)