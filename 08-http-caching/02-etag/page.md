---
title: ETag
status: live
---

Eine Slim Applikation bietet integrierte Unterstützung für HTTP Caching via ETag. Ein ETag ist ein eindeutiger
Identifier für die URI einer Ressource. Wurde mit Hilfe der `etag()` Methode ein ETag Header gesetzt, sendet der HTTP
Client bei jeder nachfolgenden Anfrage der entsprechenden URI einen **If-None-Match** Header mit. Stimmt der ETag
mit dem angefragten ETag im **If-None-Match** Header überein, wird Slim einen **304 Not Modified** HTTP Response
zurückliefern. Dieser HTTP Code weist den HTTP Client an, die Daten aus seinem Cache auszuliefern. Dieses Vorgehen
spart Bandbreite und verkürzt die Antwortzeit der Anfrage.

Das Setzen eines ETags mit Slim ist sehr einfach. In der Routen Callback Funktion muss lediglich die `etag()` Methode
der Slim Applikation aufgerufen werden. Der einzige Parameter ist eine eindeutige ID.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('eindeutige-id');
        echo "Dieser String ist nach dem ersten Request gecached!";
    });

Das war's. Abschließend muss sichergestellt werden, dass der ETag pro Ressource eindeutig ist. Außerdem muss darauf geachtet
werden, dass sich der ETag bei Änderung der Ressource ebenfalls ändern muss. Ansonsten kann es vorkommen, dass der HTTP
Client abgelaufene Daten zurückliefert.
