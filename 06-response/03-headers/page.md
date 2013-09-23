---
title: Response Headers
status: live
---

Der HTTP Response, der an den Client gesendet wird, besitzt einen Header. Der Header ist eine Liste aus Keys und Values
und enthält Metadaten über den HTTP Response. Über das Response Objekt in der Slim application kann der Header des
Response Objektes gesetzt werden. Das Response Objekt besitzt eine öffentliche Eigenschaft `headers`. Diese ist eine Instanz
von `Slim\Helper\Set` und bietet eine einfache und standardisierte Schnittstelle zum Manipulieren des HTTP Response Headers.

    <?php
    $app = new \Slim\Slim();
    $app->response->headers->set('Content-Type', 'application/json');

Außerdem können die Header über das Response Objekt ausgelesen werden:

    <?php
    $contentType = $app->response->headers->get('Content-Type');

Ist kein Header zum übergebenen Namen vorhanden, wird `null` zurückgegeben. Die Header können in Groß-, Klein- Oder
Gemischtschreibweise geschrieben werden.
