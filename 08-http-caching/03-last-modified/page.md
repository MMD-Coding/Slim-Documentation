---
title: Last Modified
status: live
---

Eine Slim Applikation bietet integrierte Unterstützung für HTTP Caching über das lastmodified (letzte Änderung) Datum
der Ressource. Wird das Datum der letzten Änderung gesetzt, meldet Slim dem HTTP Client das Datum und die Zeit der letzten
Ressourcenänderung. Der HTTP Client wird dann bei allen folgenden HTTP Requests den **If-Modified-Since** Header für die
entsprechende Ressource URI mitsenden. Stimmt das gesetzte Datum der letzten Änderung mit dem mitgesendeten **If-Modified-Since**
Header überein, sendet Slim einen **304 Not Modified** HTTP Response. Dieser HTTP Code weist den HTTP Client an, die Daten aus seinem Cache
auszuliefern. Dieses Vorgehen spart Bandbreite und verkürzt die Antwortzeit der Anfrage.

Das Setzen des entsprechenden Headers ist sehr einfach. Der `lastModified()` Methode in der Routen Callback Funktion
muss lediglich der UNIX Datumsstempel der letzten Änderung der entsprechenden Ressource übergeben werden. Es muss darauf
geachtet werden, dass sich bei Änderung der Ressource auch das Datum der letzten Änderung ändert. Ansonsten kann es vorkommen,
dass der HTTP Client abgelaufene Daten zurückliefert.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->lastModified(1286139652);
        echo "Dieser String ist nach dem ersten Request gecached!";
    });
