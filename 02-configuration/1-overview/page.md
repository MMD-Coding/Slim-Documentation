---
title: Konfigurationsübersicht
status: live
---

Es gibt zwei Möglichkeiten Slim einzustellen. Die erste ist während der Instanziierung der Slim-Anwendung und die zweite
nach der Instanziierung. Alle Einstellungen können während der Instanziierung durch die Übergabe eines assoziativen Arrays
getätigt werden. Ebenso können alle Einstellungen nach der Instanziierung abgefragt und verändert werden. Beachte jedoch, dass
manche von ihnen nicht über die config-Methode der Anwendung eingestellt werden können. Die Sonderfälle werden im weitern Verlauf
demonstriert. Bevor ich die Liste aller Konfigurationsmöglichkeiten aufzeige möchte ich das generelle Vorgehen zur Festlegung und Abfrage
der Einstellungen vorstellen.

### Bei der Instanziierung

Um während der Instanziierung die Einstellungen festzulegen übergebe ein assoziatives Array an den Konstruktor.

    <?php
    $app = new Slim(array(
        'debug' => true
    ));

### Nach der Instanziierung

Nach der Instanziierung können die meisten Einstellungen über die config-Methode festgelegt werden. Das erste
Argument ist der Name der Einstellung, das zweite der einzustellende Wert.

    <?php
    $app->config('debug', false);

Mit einem assoziativen Array können auch mehrere Einstellungen gleichzeitig gemacht werden:

    <?php
    $app->config(array(
        'debug' => true,
        'templates.path' => '../templates'
    ));

Um den Wert einer Einstellung abzufragen wird genauso die config-Methode der Anwendung verwendet. Dabei wird jedoch nur
ein einziges Argument übergeben - der Name der Einstellung. Sollte die Einstellung nicht existieren, wird `null` zurückgeliefert.

    <?php
    $settingValue = $app->config('templates.path'); //returns "../templates"

Du bist nicht auf die nachfolgenden Einstellungen beschränkt, es ist genauso möglich eigene Werte zu definieren.
