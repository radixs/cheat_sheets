Adding controllers: php bin/console make:controller Default
+ adding crud: php bin/console make:crud Default

example: route /lucky/number
controller:
class LuckyController
{
    public function number()
    {
        $number = mt_rand(0, 100);

        return new Response(
            '<html><body>Lucky number: '.$number.'</body></html>'
        );
    }
}
return $this->json(array('username' => 'jane.doe'));
return $this->file('/path/to/some_file.pdf');
    // load the file from the filesystem
    $file = new File('/path/to/some_file.pdf');

    return $this->file($file);

    // rename the downloaded file
    return $this->file($file, 'custom_name.pdf');

    // display the file contents in the browser instead of downloading it
    return $this->file('invoice_3241.pdf', 'my_invoice.pdf', ResponseHeaderBag::DISPOSITION_INLINE);

routes.yaml:
app_lucky_number:
    path: /lucky/number
    controller: App\Controller\LuckyController::number

another routing example:
blog_list:
    path:      /blog/{page}
    controller: App\Controller\BlogController::list
	defaults:
        page: 1
    requirements:
        page: '\d+'
{page} is the parameter for the controller method
requirements is a filter for that parameter

generating urls in controllers:
        $url = $this->generateUrl(
            'blog_show',
            ['slug' => 'my-blog-post']
        );
		
redirect:
return $this->redirectToRoute('homepage');
return $this->redirectToRoute('app_lucky_number', ['max' => 10]);
return $this->redirect('http://symfony.com/doc'); //external

Errors/missing pages:
    $product = ...;
    if (!$product) {
        throw $this->createNotFoundException('The product does not exist');

        // the above is just a shortcut for:
        // throw new NotFoundHttpException('The product does not exist');
    }
 
Access to the request data:
public function index(Request $request, $firstName, $lastName)
{
    $page = $request->query->get('page', 1);

    // ...
}
    $request->isXmlHttpRequest(); // is it an Ajax request?

    $request->getPreferredLanguage(array('en', 'fr'));

    // retrieves GET and POST variables respectively
    $request->query->get('page');
    $request->request->get('page');

    // retrieves SERVER variables
    $request->server->get('HTTP_HOST');

    // retrieves an instance of UploadedFile identified by foo
    $request->files->get('foo');

    // retrieves a COOKIE value
    $request->cookies->get('PHPSESSID');

    // retrieves an HTTP request header, with normalized, lowercase keys
    $request->headers->get('host');
    $request->headers->get('content_type');

Access to sessions: must be enabled in config/packages/framework.yaml
public function index(SessionInterface $session)
{
    // stores an attribute for reuse during a later user request
    $session->set('foo', 'bar');

    // gets the attribute set by another controller in another request
    $foobar = $session->get('foobar');

    // uses a default value if the attribute doesn't exist
    $filters = $session->get('filters', array());
}

Flash messages: notice, warning, error; use peek() or peekAll() to get the message but not delete it
        $this->addFlash(
            'notice',
            'Your changes were saved!'
        );
{# you can read and display just one flash message type... #}
{% for message in app.flashes('notice') %}
    <div class="flash-notice">
        {{ message }}
    </div>
{% endfor %}

{# ...or you can read and display every flash message available #}
{% for label, messages in app.flashes %}
    {% for message in messages %}
        <div class="flash-{{ label }}">
            {{ message }}
        </div>
    {% endfor %}
{% endfor %}