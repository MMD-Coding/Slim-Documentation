---
title: Response Body
status: live
---

Der HTTP Response, der an den Client gesendet wird, besitzt einen Body. Der HTTP Body ist der eigentliche Content,
der an den Client ausgeliefert wird. Du kannst das Slim application Response Objekt benutzen, um den Body des HTTP
Response zu bearbeiten:

    <?php
    $app = new \Slim\Slim();

    // Overwrite response body
    $app->response->setBody('Foo');

    // Append response body
    $app->response->write('Bar');

Wenn Du den Body überschreibst oder etwas anhängst, wird die **Content-Length** automatisch auf die Größe der Bytes des
aktuellen gesetzten Response Body gesetzt.

Du erhälst den Body des Response Objektes folgendermaßen:

    <?php
    $body = $app->response->getBody();

Normalerweise muss der Response Body nie mit Hilfe der Methoden `setBody()` oder `write()` gesetzt werden. Dies übernimmt
die Slim App automatisch. Wann immer Du innerhalb einer Routen Callback Funktion content via `echo()` ausgibst, wird der
ausgegebene Content in einem Output Buffer gehalten und an den Response Body, der an den Client gesendet wird, angehängt.
