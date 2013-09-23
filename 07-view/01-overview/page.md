---
title: View Übersicht
status: live
---

Eine Slim Applikation delegiert das Rendern der Templates an sein View Objekt. Eine Slim View ist eine Subklasse
von `Slim\View` und implementiert dieses Interface:

    <?php
    public render(string $template);

Die `render()` Methode muss den gerenderten Content des entsprechenden Templates (spezifiziert durch `$template`)
zurückliefern.
