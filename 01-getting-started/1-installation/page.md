---
title: Installation
status: live
---

### Composer Installation

Installiere Composer in dein Projekt:

    curl -s https://getcomposer.org/installer | php

Erstelle eine `composer.json`-Datei in deinem Projektverzeichnis:

    {
        "require": {
            "slim/slim": "2.*"
        }
    }

Führe das Composer-Install-Skript aus:

    php composer.phar install

Füge diese Zeile in die `index.php` deiner Anwendung ein:

    <?php
    require 'vendor/autoload.php';

### Manuelle Installation

Das Slim Framework in dein Projektverzeichnis herunterladen und entpacken.
Anschließend über `require` in deine `index.php` einbinden. Außerdem muss der Autoloader von Slim registriert werden.

    <?php
    require 'Slim/Slim.php';
    \Slim\Slim::registerAutoloader();
