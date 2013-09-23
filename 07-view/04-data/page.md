---
title: View Daten
status: live
---

<div class="alert alert-info">
    <strong>Heads Up!</strong> Selten werden Daten direkt an das View Objekt angehängt.
    Normalerweise werden diese Daten mit Hilfe der `render()` Methode der Slim Applikation
    weitergereicht. Siehe <a href="/pages/view-rendering-templates">Rendering Templates</a>.
</div>

Die Methoden `setData()` und `appendData()` des  View Objektes übergeben Daten direkt an das View Objekt.
Die übergebenen Daten sind somit in den View Templates verfügbar. Die Daten werden intern als key-value Array
gehalten.

### Daten setzen

Die `setData()` Methode des View Objektes überschreibt existierende Daten in der View. Die Methode wird verwendet, um einer
einzelnen Variable einen bestimmten Wert zuzuweisen:

    <?php
    $app->view->setData('color', 'red');

Die Daten der View enthalten nun einen Schlüssel ”color” mit dem Wert ”red”. Die `setData()` Methode kann auch verwendet
werden, um mehrere Daten als Array zu setzen:

    <?php
    $app->view->setData(array(
        'color' => 'red',
        'size' => 'medium'
    ));

Achtung: Die `setData()` Methode ersetzt bereits gesetzte Daten.

### Daten anhängen

Um Daten an das View Objekt anzuhängen kann die `appendData()` Methode verwendet werden, die lediglich ein Array als Parameter
akzeptiert.

    <?php
    $app->view->appendData(array(
        'foo' => 'bar'
    ));
