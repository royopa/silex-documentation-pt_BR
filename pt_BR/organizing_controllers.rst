Organizando os Controllers
==========================

Quando sua aplicação começa a definir muitos controllers, você pode querer agrupá-los
de forma lógica::

    // define controllers para um blog
    $blog = $app['controllers_factory'];
    $blog->get('/', function () {
        return 'Blog home page';
    });
    // ...

    // define controllers para um forum
    $forum = $app['controllers_factory'];
    $forum->get('/', function () {
        return 'Forum home page';
    });

    // define controllers "globais"
    $app->get('/', function () {
        return 'Main home page';
    });

    $app->mount('/blog', $blog);
    $app->mount('/forum', $forum);

.. note::

    ``$app['controllers_factory']`` é uma factory que retorna uma nova instância 
    da classe ``ControllerCollection`` quando usada.

O método ``mount()`` prefixa todas as rotas com o dado prefixo e mescla essas
rotas na aplicação principal. Então, a rota ``/`` será mapeada para a página inicial
principal, ``/blog/`` será mapeada para a página inicial do blog e ``/forum/`` 
será mapeada para a página inicial do fórum.

.. caution::

    Ao montar uma coleção de roteamento abaixo de ``/blog``, não é possível 
    definir uma rota para a URL ``/blog``. A menor URL possível é ``/blog/``.

.. note::

    Ao chamar os métodos ``get()``, ``match()``, ou qualquer outro método HTTP
    na Aplicação, você está na verdade chamando uma instância padrão da classe
    ``ControllerCollection`` (armazenada in ``$app['controllers']``).

Outro benefício é a capacidade de aplicar configurações para um conjunto de 
controllers muito facilmente. Com base no exemplo da seção middleware, veremos
abaixo como você garantiria segurança para os controllers da coleção backend::

    $backend = $app['controllers_factory'];

    // garante que todos os controllers exigem usuários logados
    $backend->before($mustBeLogged);

.. tip::

    Para uma melhor legibilidade, você pode dividir cada coleção em um arquivo
    separado::

        // blog.php
        $blog = $app['controllers_factory'];
        $blog->get('/', function () { return 'Blog home page'; });

        return $blog;

        // app.php
        $app->mount('/blog', include 'blog.php');

    Ao invés exigir um arquivo, você pode também criar um :doc:`Controller
    provider </providers#controllers-providers>`.
