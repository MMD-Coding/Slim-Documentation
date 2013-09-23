---
title: Rendering
status: live
---

Um ein Template von der aktuellen View aus mit verschiedenen Variablen zu rendern, kann die `render()` Methode
der Slim Applikation verwendet werden. Der von der `render()` Methode erzeugte Output der View wird von einem
Output Buffer vorgehalten und automatisch an den Body des Response Objektes angehängt. Dieses Verhalten ändert
nichts daran, wie das Template gerendert wird - es wird trotzdem an das View Objekt delegiert.

    <?php
    $app = new \Slim\Slim();
    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('myTemplate.php', array('id' => $id));
    });

Sollen Daten aus der Callback Funktion der Route in eine View übergeben werden, müssen diese der Methode `render()` als
zweitem Parameter und als Array übergeben werden. Beispiel:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' )
    );

Außerdem kann beim Rendern eines Templates der HTTP Response Status gesetzt werden:

    <?php
    $app->render(
        'myTemplate.php',
        array( 'name' => 'Josh' ),
        404
    );
