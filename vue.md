defining vue app in js:

```
new Vue({
    el: '#app',
    components: {Example},
    data: {
        message: 'Hello world!',
        message2: 'blah blah blah',
        seen: true
    }
});
```

then in html:

Just a dynamic variable link.
```
<div>
    {{"{{ message }}"}}
</div>
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