---
title: Response Helpers
status: live
---

Das Response Objekt stellt Helper Methoden bereit, die die Interaktion und Inspektion des darunterliegenden HTTP
Response vereinfachen.

### Finalize

Die `finalize()` Methode des Response Objektes liefert ein numerisches Array von `[status, header, body]`. Der Status
ist ein Integer-Wert, der Header eine iterierbare Datenstruktur und der Body ein String. Um Status, Header und Body
für den darunterliegenden HTTP Response zu erzeugen, muss die `finalize()` Methode an der Stelle aufgerufen werden, an der ein
`Slim\Http\Response` Objekt generiert wird (z.B. Slim application oder Middleware).

    <?php
    /**
     * Neues Response Objekt vorbereiten
     */
    $res = new \Slim\Http\Response();
    $res->setStatus(400);
    $res->write('You made a bad request');
    $res->headers->set('Content-Type', 'text/plain');

    /**
     * Finalize
     * @return [
     *     200,
     *     ['Content-type' => 'text/plain'],
     *     'You made a bad request'
     * ]
     */
    $array = $res->finalize();

### Redirect

Um einen **3xx Redirect** Header zu setzen, müssen der `redirect()` Methode des Response Objektes der Status
und die **Location:** übergeben werden.

    <?php
    $app->response->redirect('/foo', 303);

### Status Selbstprüfung

Das Response Objekt stellt weitere Helper Methoden zur Verfügung, um den aktuellen Status au überprüfen.
Alle folgenden Werte liefern einen booleschen Wert zurück.

    <?php
    $res = $app->response;

    //Ist es ein informativer Response?
    $res->isInformational();

    //Ist es ein 200 OK Response?
    $res->isOk();

    //Ist es ein erfolgreicher 2xx Response?
    $res->isSuccessful();

    //Ist es ein 3xx Weiterleitungs Response?
    $res->isRedirection();

    //Ist es ein spezifischer Weiterleitungs Response? (301, 302, 303, 307)
    $res->isRedirect();

    //Ist es ein verbotener Response?
    $res->isForbidden();

    //Ist es ein "not found" Response?
    $res->isNotFound();

    //Ist es ein "client error" Response?
    $res->isClientError();

    //Ist es ein "server error" Response?
    $res->isServerError();
