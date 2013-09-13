---
title: Hello World
status: live
---

Eine Instanz von Slim erstellen:

    $app = new \Slim\Slim();

Eine HTTP GET Route definieren:

    $app->get('/hello/:name', function ($name) {
        echo "Hello, $name";
    });

Die Slim-Anwendung ausführen:

    $app->run();
