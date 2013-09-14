---
title: Expires
status: live
---

Ergänzend zu den Methoden `etag()` oder `lastModified()` der Slim Applikation setzt die Methode `expires()` im HTTP Response
einen Header **Expires**. Dieser besagt, wann der Cache für die angefragte Ressource beim HTTP Client abläuft. Der HTTP Client
wird solange die im Cache gespeicherten Daten ausliefern, bis das gesetzte Ablaufdatum erreicht ist.

Die `expires()` Methode akzeptiert einen Parameter: Einen UNIX Zeitstempel (Integer) oder einen String, der von `strtotime()`
geparsed werden kann.

    <?php
    $app->get('/foo', function () use ($app) {
        $app->etag('unique-resource-id');
        $app->expires('+1 week');
        echo "Dieser String ist nach dem ersten Request gecached!";
    });
