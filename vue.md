For twig you need to do something like `{{"{{ message }}"}}` in order to beat the overlapping of brackets with vue


defining vue app in js:

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

for loop
```
<ol>
    <li v-for="loopit in for_example">
        {{"{{ loopit.text }}"}}
    </li>
</ol>
```