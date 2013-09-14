---
title: Benutzerdefinierte Views
status: live
---

Eine Slim Applikation delegiert das Rendern der Templates an sein View Objekt. Eine Slim View ist eine Subklasse
von `Slim\View` und implementiert dieses Interface:

    <?php
    public render(string $template);

Die `render()` Methode muss den gerenderten Content des entsprechenden Templates (spezifiziert durch `$template`)
zurückliefern. Wird die `render` Methode der benutzerdefinierten View aufgerufen, wird dieser der verlangte Pfadname
(Relativ zur “templates.path” Einstellung der Slim Applikation) des Templates als Argument übergeben.
Folgend ein Beispiel einer benutzerdefinierten View:

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            return 'The final rendered template';
        }
    }

Die benutzerdefinierte View kann eine beliebige interne Funktionalität enthalten. Sie muss lediglich den gerenderten
Content des Templates als String zurückliefern. Eine benutzerdefinierte View vereinfacht die Integration von populären
PHP Templatesystemen wie Twig oder Smarty.

<div class="alert alert-info">
    <strong>Heads Up!</strong> A custom view may access data passed to it by the Slim application’s
    <code>render()</code> method with <code>$this->data</code>.
</div>

Benutzerdefinierte "ready-to-use" Views, die mit den populären Templatesystemen von PHP zusammenarbeiten, finden sich auf Github
im Slim-Extras Repository.

### Beispiel View

    <?php
    class CustomView extends \Slim\View
    {
        public function render($template)
        {
            // $template === 'show.php'
            // $this->data['title'] === 'Sahara'
        }
    }

### Beispiel Integration

Kann die benutzerdefinierte View nicht von einem registrierten Autoloader gefunden werden, muss diese vor Instanzierung
der Slim Applikation eingebunden (require) werden.

    <?php
    require 'CustomView.php';

    $app = new \Slim\Slim(array(
        'view' => new CustomView()
    ));

    $app->get('/books/:id', function ($id) use ($app) {
        $app->render('show.php', array('title' => 'Sahara'));
    });

    $app->run();
