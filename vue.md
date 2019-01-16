For twig you need to do something like `{{"{{ message }}"}}` in order to beat the overlapping of brackets with vue

# Basics

### in html:

Just a dynamic variable link.
```
<div>
    {{"{{ message }}"}}
</div>
```

and add dynamic binding:
```
<input v-model="message">
```


title link
```
<span v-bind:title="message2">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
</span>
```

element toggle
```
<span v-if="seen">Now you see me</span>
```

for loop
```
<ol>
    <li v-for="loopit in for_example">
        {{"{{ loopit.text }}"}}
    </li>
</ol>
```

events and actions on DOM:
```
<div">
    <p>{{"{{ message3 }}"}}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```


### defining vue app in js:

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
        ]
    },
    methods: {
        reverseMessage: function () {
            this.message = this.message.split('').reverse().join('')
        }
    }
});
```
# API

### instance methods:
```
// $watch is an instance method
vm.$watch('a', function (newValue, oldValue) {
  // This callback will be called when `vm.a` changes
})
```

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