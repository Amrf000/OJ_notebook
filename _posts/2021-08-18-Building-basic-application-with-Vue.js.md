---
layout: post
title: Building basic application with Vue.js
category: Vue
tags: [vue]
---
**Building basic application with Vue.js**
==========================================

[![Pavel Ilin](/md_blog/public/assets/2021-08-18/2_3w1L1s_FJqFwT7nmcZOvGQ.jpeg)](https://pavel-ilin.medium.com/?source=post_page-----d8b32d0abbba--------------------------------)

[Pavel Ilin](https://pavel-ilin.medium.com/?source=post_page-----d8b32d0abbba--------------------------------)

Follow

[Jun 12, 2020](/swlh/building-basic-application-with-vue-js-d8b32d0abbba?source=post_page-----d8b32d0abbba--------------------------------) · 4 min read

[](/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fbookmark%2Fp%2Fd8b32d0abbba&operation=register&redirect=https%3A%2F%2Fmedium.com%2Fswlh%2Fbuilding-basic-application-with-vue-js-d8b32d0abbba&source=post_actions_header--------------------------bookmark_preview-----------)

Software development market is very diverse and the range of tasks could vary a lot. As developers we should be able to work with different technologies. In this post we will talk about how to build basic frontend application using Vue.js

**Installation**

First we will need to install Node on your machine. [Here](https://nodejs.org/en/download/) you can download and install it.

Next we will need to install Vue CLI library:

npm install -g @vue/cli

With this library the process of creating a new Vue project becomes very easy.

**New Project**

After installation has been completed we can create new project by running this command in the console:

vue ui

In a few seconds the visual interface will be open in your browser. Now we can create a new project.

Click on **Create** and enter the destination where the project you want to be created:

![](/md_blog/public/assets/2021-08-18/1_W53VtvyBMJdcYqENgDD70w.png)

Enter the project folder as new\_app and click **Next**.

![](/md_blog/public/assets/2021-08-18/1_dEq_0JOFVp6PufNeD5JioA.png)

Next step, select **default preset**, it will create the simplest empty template:

![](/md_blog/public/assets/2021-08-18/1_6YgPV7_y03midsbLJUbVBg.png)

And finally click **CreateProject.**

After few moments you should see this:

![](/md_blog/public/assets/2021-08-18/1_5H6nSsugfmhLtFLeOVjReg.png)

Let’s test if everything is working:

cd new\_appyarn run serve

It will run a server in **localhost:8080** by default. And if we open it in the browser we will see this:

![](/md_blog/public/assets/2021-08-18/1_FDoBuwheaAlFTw6dYxYMgw.png)

This is it, basic Vue.js application up and running!

**How Vue works**

Here the Vue file structure:

![](/md_blog/public/assets/2021-08-18/1_NyUrLV_65GwRvXwfJhlRPA.png)

If you work with something like React, it looks familiar.

*   There is **package.json** for all Node dependencies.
*   **public/index.html**: first file that loads when the application starts. This file has this: **<div id=”app”></div>**. Every component will be loaded within this div element.
*   **src/main.js**: This is where the Vue Instance is created:

new Vue({ render: h => h(App)}).$mount(‘#app’)

*   **src/App.vue**: This is a container for all Vue components.

![](/md_blog/public/assets/2021-08-18/1_yLmpQZus_UXGKEFTnsS4qA.png)

*   **src/components**: And this is a directory which contains all components. For now there is only **HelloWorld.vue** component, but we will fix that in a moment.

**New Component**

After we successfully create a basic application with Vue, let’s add a new component to our brand new app.

First we need to create NewComponent.vue in the component directory. Obviously the name of the component can be whatever you want. A \*.vue files is a custom file format that uses HTML-like syntax to describe a Vue component.

Vue component consist of the 3 sections, HTML, JavaScript and CSS:

HTML:

![](/md_blog/public/assets/2021-08-18/1_lkut2NHiJ-kQaexL7KJv4Q.png)

Simple HTML with inserted prop wrapped to the **<template>** tag.

JavaScript:

![](/md_blog/public/assets/2021-08-18/1_rqV-hUPlfUA_VO8INMj7ng.png)

In javaScript section we export component, define props and put the rest of the javascript code.

CSS:

![](/md_blog/public/assets/2021-08-18/1_bQOGKoXXXKDLr6K8C3jcmQ.png)

The CSS section is optional, if we need to style specifically this component, otherwise it will use the style of the parent.

Now, when we have a brand new component, let’s use it. In Vue we can import it into the parent component. In our case it’s App.vue.

Import and defying component:

![](/md_blog/public/assets/2021-08-18/1_E69apsOnwFD9oTAnLoj9fw.png)

Use component in the template:

![](/md_blog/public/assets/2021-08-18/1_byS89MJqrv32SmEsWfYSNw.png)

And here we are! Our brand new component appears on the DOM:

![](/md_blog/public/assets/2021-08-18/1_60ovAaNw9PNFcZfskZOWng.png)

**Conclusion**

As developers we should be able to use different technologies to build cool stuff! With Vue.js we can create a frontend very fast and easy.

For more data and software engineering insights, let’s connect on [LinkedIn](https://www.linkedin.com/in/pavel-ilin/)!