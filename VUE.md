---
title: Vuejs
description: 
published: true
date: 2020-09-15T19:14:34.945Z
tags: javascript, vue, framework, frontend, webdevelopment
editor: markdown
dateCreated: 2020-06-07T09:47:48.694Z
---

![vue](/logo[1].png =100x100){.align-left}[Vue.js](https://vuejs.org/) is a community driven frontend framework,
it has taken up his postion with the other 2 'big' frameworks:
Angular (Google) and React (Facebook)

---

# Overview

Vue 2.x is almost end of life.
Vue 3 is from the ground up new version with some fundamental changes. The newest version makes VUE; easier, quicker and faster.

---

Basic Template:

```js
<template>
// HTML 
</template>
  
<script>
// Imports
  
export default {
  name: xxx, // Instance Name
  components: {
 	// loaded from the import
  },
  setup() {
  // vue 3 style with setup() .
  // you dont have to break it down into 'data()', 'computed()'
  
  // return your variables to use it in the HTLM
  	return {
  		// components
  	};
  },
};
</script>
 
<style>
// CSS style or with lang="sccs" you can use SASS
// scoped means the style can only be used inside this component
</style>
```

# Directives
## V-ON
[v-on](https://vuejs.org/v2/api/#v-on) is equal to the @ sign:
usefull with the modifiers as .prevent which call event.preventDefault() on a Form.

```js
v-on:click
// or:
@click

```


# Vue 3 Lifecycle Hooks
it is possible to call functions on certains `build` steps.
Vue build the application by ordered instructions, on each instruction you can 'manipulate' the data/outcome.

## Hooks

| Name        | Explanation          
| :------------- |:-------------| 
| `onBeforeMount` | called before mounting begins |
| `onMounted` | called when component is mounted | 
| `onBeforeUpdate` | called when reactive data changes and before re-render |
| `onUpdated` | called after re-render | 
| `onBeforeUnmount` | called before the Vue instance is destroyed |
| `onUnmounted` | called after the instance is destroyed | 
| `onActivated` | called when a kept-alive component is activated |
| `onDeactivated` | called when a kept-alive component is deactivated | 
| `onErrorCapturd` | called when an error is captured from a child component|

## Code

```js
import { onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onBeforeUnmount, onUnmounted, onActivated, onDeactivated, onErrorCaptured } from 'vue'

export default {
  setup() {
    onBeforeMount(() => {
      // ... 
    })
    onMounted(() => {
      // ... 
    })
    onBeforeUpdate(() => {
      // ... 
    })
    onUpdated(() => {
      // ... 
    })
    onBeforeUnmount(() => {
      // ... 
    })
    onUnmounted(() => {
      // ... 
    })
    onActivated(() => {
      // ... 
    })
    onDeactivated(() => {
      // ... 
    })
    onErrorCaptured(() => {
      // ... 
    })
  }
}
```

> Source: https://learnvue.co/2020/03/how-to-use-lifecycle-hooks-in-vue3/

# Watch(er) function
Don't use a console.log (to debug) right in the first line of this function.

#### Example
```js
    watch(user, () => {
      // Error code: console.log(user.value.status.inGame);
      if (!user.value) {
        router.push('/');
      }
      if (user.value && user.value.status.inGame === true) {
        console.log(
          'This is the watcher of user: if inGame has been init: Push to /questions route',
        );
        router.push('/questions');
      }
    });
```

# Vuex
> Stores a Single Source of Truth inside the **Vuex** *Store*.
> and can be accessed from every component.
> ```js
> test code:
>     watch(user, () => {
>      // Error code: console.log(user.value.status.inGame);
>      if (!user.value) {
>        router.push('/');
>      }
>      if (user.value && user.value.status.inGame === true) {
>        console.log(
>          'This is the watcher of user: if inGame has been init: Push to /questions route',
>        );
>        router.push('/questions');
>      }
>    });
> ```
> {.is-success}

## Vue 2.x
### Commands:

```js
mapState
```

```js
mapGetters
```

```js
mapMutations
```

```js
mapActions
```

---

## Vue 3
### Vuex-hooks
> with [@u3u/vue-hooks](https://github.com/u3u/vue-hooks) the commands start with `use` instead of `map`
can be used in comibation with the composition API (VUE 3).


### Commands:

***Netlify:***
`useDate` — Using dayjs to process date. [useDate](https://vue-hooks.netlify.com/?path=/story/usedate--docs)
`useWindowSize` — Tracks window dimensions. [useWindowSize](https://vue-hooks.netlify.com/?path=/story/usewindowsize--docs)
`useCounter` — Tracks state of a number. [useCounter](https://vue-hooks.netlify.com/?path=/story/usecounter--docs)
`usePrevious` — Returns the previous state or props [usePrevious](https://vue-hooks.netlify.com/?path=/story/useprevious--docs).

---

***Vue-Router:***
`useRouter` — A hook for [vue-router](https://github.com/vuejs/vue-router).

---

***Vuex***
`useStore` — A hook for [vuex](https://github.com/vuejs/vuex).
`useState` — A hook for [mapState](https://vuex.vuejs.org/api/#mapstate).
`useGetters` — A hook for [mapGetters](https://vuex.vuejs.org/api/#mapgetters).
`useMutations` — A hook for [mapMutations](https://vuex.vuejs.org/api/#mapmutations).
`useActions` — A hook for [mapActions](https://vuex.vuejs.org/api/#mapactions).

---

### Example:
```js
const { destructured } = useSomething('vueStore/module', [
  'storeFunction',
  'storeValue',
]);
```

---
## Feathers-Vuex
is a first class integration of the Feathers Client and Vuex.
It implements many Redux best practices under the hood, eliminates a lot of boilerplate code, and still allows you to easily customize the Vuex store.


```js
npm install feathers-vuex @vue/composition-api --save
````

---

>  #### `Auth Plugin user Not Reactive New API in 3.2.0`
> 
> Due to changes in how reactivity is applied to service state (it's now using Vue.set under the hood), the user state of the auth module is no longer reactive. To fix this issue, two getters have been added to the auth state. They are available when a userService is provided to the makeAuthPlugin options.
> 
> - user: returns the reactive, logged-in user from the userService specified in the 		options.
>- isAuthenticated: a easy to remember boolean attribute for if the user is logged in.
> 
> If you depend on a reactive, logged-in user in your apps, here is how to fix the reactivity:
>
> - Replace any reference to store.state.auth.user with store.getters['auth/user'].
>{.is-info}



> Because the user state is no longer reactive, it is logical for it to be removed in the next version. It will likely be replaced by a `userId` attribute in **Feathers-Vuex 4.0.**
{.is-danger}


---


