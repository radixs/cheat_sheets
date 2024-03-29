# Guides

* https://vuejs.org/v2/guide/ - main page
* https://vuejs.org/v2/guide/components-registration.html - how component system works in vue
* https://vuejs.org/v2/guide/single-file-components.html - how vue files are to be structured
* https://vuejs.org/v2/api/#Global-Config
* http://www.javascripttutorial.net/es6/es6-modules/ - modules import/export tutorial
* https://babeljs.io/docs/en/learn - ES6 feature list
* https://cli.vuejs.org/guide/ - vue cli


For twig you need to do something like `{{"{{ message }}"}}` in order to beat the overlapping of brackets with vue

# Basics

### in html:

Just a dynamic text variable link. To disable ability to reactively change it add `v-once` directive to holding element.
```
<div>
    {{ message }}
</div>

<div>
    {{ reversedMessage }}
</div>
```

for html strings do:
```
<span v-html="message"></span></p>
```


and add dynamic binding:
```
<input v-model="message">
```

attribute value binding (shorthand for `v-bind:title` is `:title`)
```
<span v-bind:title="message2">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
</span>
```

value binding for classes (determined byt truthiness):
```
<div class="static"  v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
```
or define in data:
```
data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```
array bind:
```
<div v-bind:class="[activeClass, errorClass]"></div>
```


element toggle, conditionals
```
<span v-if="seen">Now you see me</span>

<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```

for loop
```
<ol>
    <li v-for="loopit in for_example">
        {{ loopit.text }}
    </li>
</ol>
```

events and actions on DOM, you can add `.prevent` modifier for `preventDefault` functionality. Shorthand for `v-on:click` is `@click`:
```
<div">
    <p>{{ message3 }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```


### defining vue app in js (primitives in `data`, complex in `computed`, functions in `methods`):

```
new Vue({
    el: '#app',
    components: {Example},
    data: {
        message: 'Hello world!',
        message2: 'blah blah blah',
        seen: true.
        for_example: [
            {text: "one"},
            {text: "two"},
            {text: "three"}
        ],
        activeClass: 'active',
        errorClass: 'text-danger'
    },
    methods: {
        reverseMessage: function () {
            this.message = this.message.split('').reverse().join('')
        }
    },
    computed: {
        // a computed getter
        reversedMessage: function () {
            // `this` points to the vm instance
            return this.message.split('').reverse().join('')
        }
    }
});
```
computed can also have setters:
```
// ...
computed: {
    fullName: {
        // getter
        get: function () {
            return this.firstName + ' ' + this.lastName
        },
        // setter
        set: function (newValue) {
            var names = newValue.split(' ')
            this.firstName = names[0]
            this.lastName = names[names.length - 1]
        }
    }
}
// ...
```



watchers can also be used, however it is better to use coputed:
```
var vm = new Vue({
    el: '#demo',
    data: {
        firstName: 'Foo',
        lastName: 'Bar',
        fullName: 'Foo Bar'
    },
    watch: {
        firstName: function (val) {
            this.fullName = val + ' ' + this.lastName
        },
        lastName: function (val) {
            this.fullName = this.firstName + ' ' + val
        }
    }
})
```


# API

### instance methods:
```
// $watch is an instance method
vm.$watch('a', function (newValue, oldValue) {
  // This callback will be called when `vm.a` changes
})
```
### hooks:
beforeUpdate, updated

# Components

### defining inside main Vue component:
```
new Vue({
    el: '#app',
    components: {SomeFunComponent},
});
```

you need the component defined in `SomeFunComponent.vue` in `components` directory relative to your main app.js:
```
<template>
    <div>
        <p>This is an example of a new components in VueJs</p>
    </div>
</template>

<script>
    export default {
        name: "example"
    }
</script>

<style scoped>

</style>

```

and finally put it soemwhere in the DOM to wtite it in:
```
<somefuncomponent></somefuncomponent>
```

To pass in some values into a component do:
```
//js
Vue.component('blog-post', {
  props: ['title'],
  template: '<h3>{{ title }}</h3>'
})

//template
<blog-post title="My journey with Vue"></blog-post>
<blog-post title="Blogging with Vue"></blog-post>
<blog-post title="Why Vue is so fun"></blog-post>
```
or from data:
```
//js
new Vue({
  el: '#blog-post-demo',
  data: {
    posts: [
      { id: 1, title: 'My journey with Vue' },
      { id: 2, title: 'Blogging with Vue' },
      { id: 3, title: 'Why Vue is so fun' }
    ]
  }
})

//template:
<blog-post
  v-for="post in posts"
  v-bind:key="post.id"
  v-bind:title="post.title"
></blog-post>
```


