Introdução
==========

Silex é um microframework para o PHP 5.3. Ele é construído baseado no `Symfony2`_
e no `Pimple`_ e também inspirado pelo `Sinatra`_.

O Silex pretende ser:

* *Conciso*: O Silex expõe uma API intuitiva e concisa.

* *Extensível*: O Silex tem um sistema de extensão baseado em torno do micro
service-container Pimple que torna mais fácil conectar bibliotecas de 
terceiros.

* *Testável*: O Silex usa o HttpKernel do Symfony2 que abstrai o request e response. 
Isso facilita os testes das aplicações e do próprio framework. O Silex também respeita
a especificação HTTP e incentiva o uso adequado da especificação.

Em poucas palavras, você define os controllers e os mapeia em rotas em uma única
etapa.

Utilização
----------

.. code-block:: php

    <?php

    // web/index.php
    require_once __DIR__.'/../vendor/autoload.php';

    $app = new Silex\Application();

    $app->get('/hello/{name}', function ($name) use ($app) {
        return 'Hello '.$app->escape($name);
    });

    $app->run();

Tudo o que é necessário para ter acesso ao Framework é incluir o
autoloader.

Em seguida definimos uma rota para ``/hello/{name}`` que corresponde para a 
requisição ``GET`` definida.
Quanto a rota é encontrada, a função é executada e o valor de retorno é 
enviado de volta ao cliente.

Finalmente, o aplicativo é executado. Visite ``/hello/world`` para ver o resultado.
É realmente muito fácil!

Instalar o Silex é tão fácil quanto baixá-lo. Faça `Download`_ e extraia o arquivo, 
e você está pronto!

.. _Symfony2: http://symfony.com/
.. _Pimple: http://pimple.sensiolabs.org/
.. _Sinatra: http://www.sinatrarb.com/
