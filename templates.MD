# Templates

###### Adding templates - into templates dir (twig)

###### Using filters:
```
{{ title|upper }}
```

###### Child using parent template block code:
```
{{ parent() }}
```

###### Including other templates:
```
{{ include('article/article_details.html.twig', { 'article': article }) } - path then parameters
```

###### Adding a link:
```
<a href="{{ path('welcome') }}">Home</a>
```
OR for route:
```
article_show:
    path:       /article/{slug}
    controller: App\Controller\ArticleController::show
```    
do:
```
{% for article in articles %}
    <a href="{{ path('article_show', {'slug': article.slug}) }}">
        {{ article.title }}
    </a>
{% endfor %}
```

###### Assets linking
```:
<img src="{{ asset('images/logo.png') }}" alt="Symfony!" />
<link href="{{ asset('css/blog.css') }}" rel="stylesheet" />
```

In <script>:
```
<script>
var route = "{{ path('blog_show', {'slug': 'my-blog-post'})|escape('js') }}";
</script>
```

In main template:
```
{% block stylesheets %}
	<link href="{{ asset('css/main.css') }}" rel="stylesheet" />
{% endblock %}

{% block javascripts %}
	<script src="{{ asset('js/main.js') }}"></script>
{% endblock %}
child template override:
{% block stylesheets %}
    {{ parent() }}

    <link href="{{ asset('css/contact.css') }}" rel="stylesheet" />
{% endblock %}
```

###### XSS: 
Output escaping is on automatically.
```
{{ description }} <!-- I &lt;3 this product -->
```

Disable output escaping with the raw filter.
```
{{ description|raw }} <!-- I <3 this product -->
```

###### Accessing app:
```
<p>Username: {{ app.user.username }}</p>
{% if app.debug %}
    <p>Request method: {{ app.request.method }}</p>
    <p>Application Environment: {{ app.environment }}</p>
{% endif %}
app.session
```