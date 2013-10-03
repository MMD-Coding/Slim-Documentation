---
title: Einstellungen der Applikation
status: live
---

### mode

Das ist der Bezeichner für den aktuellen Zustand (mode) der Applikation. Der gewählte Zustand beeinflusst nicht die internen
Funktionsabläufe von Slim. Stattdessen erlaubt es dir bestimmte Teile deines Codes mithilfe der `configMode()`-Methode in Abhängigkeit
von dem gewählten Zustand auszuführen.

Der Zustand wird während der Instanziierung entweder über eine Umgebungsvariable oder als Argument des Konstruktors festgelegt.
Es kann im weiteren Verlauf nicht mehr verändert werden. Der Zustand kann ein beliebiger von dir festgelegter Wert sein — "development",
"test" und "production" sind üblich, du kannst aber auch etwas anderes nehmen (z.B. "foo").

    <?php
    $app = new \Slim\Slim(array(
        'mode' => 'development'
    ));

Datentyp
: string

Standardwert
: "development"

### debug

<div class="alert alert-info">
    <strong>Aufgepasst!</strong> Slim wandelt Fehler in `ErrorException`-Instanzen um.
</div>

Wenn der debug-Modus aktiviert ist, wird Slim mit dem eingebauten error handler nähere Infos zu nicht abgefangenen
Exceptions anzeigen. Wenn der debug-Modus deaktiviert ist, wird Slim stattdessen den benutzerdefinierten error handler
aufrufen und ihm die nicht abgefangene Exception als erstes und einziges Argument übergeben.

    <?php
    $app = new \Slim\Slim(array(
        'debug' => true
    ));

Datentyp
: boolean

Standardwert
: true

### log.writer

Du kannst einen benutzerdefinierten Logger (log writer) dazu verwenden die Log-Nachrichten an eine geeignete Stelle umzuleiten.
Standardmäßig schreibt Slim die Logs nach `STDERR`. Ein benutzerdefinierter log writer muss das folgende Interface implementieren:

    public write(mixed $message, int $level);

Die `write()`-Methode ist für das Schreiben der Log-Nachricht (nicht zwingend einer Zeichenkette) an die entsprechende Stelle
(z.B. Text-Datei, Datenbank oder ein remote Web-Service) zuständig.

Um einen benutzerdefinierten Logger nach der Instanziierung festzulegen musst du auf Slims Logger direkt zugreifen und dessen `setWriter()`-Methode verwenden:

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'log.writer' => new \My\LogWriter()
    ));

    // Nach der Instanziierung
    $log = $app->getLog();
    $log->setWriter(new \My\LogWriter());

Datentyp
: mixed

Standardwert
: \Slim\LogWriter

### log.level

<div class="alert alert-info">
    <strong>Aufgepasst!</strong> Benutze die Konstanten aus `\Slim\Log` anstelle von Integern.
</div>

Slim hat folgende Log-Stufen:

* \Slim\Log::EMERGENCY
* \Slim\Log::ALERT
* \Slim\Log::CRITICAL
* \Slim\Log::ERROR
* \Slim\Log::WARN
* \Slim\Log::NOTICE
* \Slim\Log::INFO
* \Slim\Log::DEBUG

Die Einstellung der Log-Stufe legt fest welche Meldungen verarbeitet und welche ignoriert werden.
Sollte die `log.level`-Einstellung zum Beispiel auf `\Slim\Log::INFO` gesetzt sein, so würden debug-Nachrichten ignoriert
und info, warn, error und fatal-Nachrichten geloggt werden.

Um die Log-Stufe nach der Instanziierung zu ändern musst du auf Slims Logger direkt zugreifen und dessen `setLevel()`-Methode verwenden:

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'log.level' => \Slim\Log::DEBUG
    ));

    // Nach der Instanziierung
    $log = $app->getLog();
    $log->setLevel(\Slim\Log::WARN);

Datentyp
: integer

Standardwert
: \Slim\Log::DEBUG

### log.enabled

Diese Einstellunge schaltet den Logger an oder aus. Um sie nach der Instanziierung zu ändern musst du auf Slims
Logger direkt zugreifen und dessen `setEnabled()`-Methode verwenden:

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'log.enabled' => true
    ));

    // Nach der Instanziierung
    $log = $app->getLog();
    $log->setEnabled(true);

Datentyp
: boolean

Standardwert
: true

### templates.path

Relativer oder absoluter Pfad zu dem Ordner mit Template-Dateien der Slim-Applikation.
Dieser Pfad wird von Slims View verwendet um Templates zu laden und zu rendern.

Um den Pfad nach der Instanziierung zu ändern musst du auf Slims View direkt zugreifen und dessen `setTemplatesDirectory()`-Methode verwenden:

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'templates.path' => './templates'
    ));

    // Nach der Instanziierung
    $view = $app->view();
    $view->setTemplatesDirectory('./templates');

Datentyp
: string

Standardwert
: "./templates"

### view

Die von Slim verwendete View-Klasse. Um diese Einstellung nach der Instanziierung zu ändern
musst du Slims `view()`-Methode verwenden:

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'view' => new \My\View()
    ));

    // Nach der Instanziierung
    $app->view(new \My\View());

Datentyp
: string|\Slim\View

Standardwert
: \Slim\View

### cookies.encrypt

Legt fest ob Slim dessen HTTP-Cookies verschlüsseln soll.

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true
    ));

Datentyp
: boolean

Standardwert
: false

### cookies.lifetime

Legt die Lebensdauer von HTTP-Cookies der Slim-Applikation fest. Wenn der Wert ein Integer ist, muss es ein
gültiger UNIX-Timestamp sein, an dem der Cookie verfällt. Wenn der Wert ein String ist, dann wird es mithilfe der
`strtotime()`-Funktion geparst um einen UNIX-Timestamp zu bekommen, an dem der Cookie verfällt.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.lifetime' => '20 minutes'
    ));

    // Nach der Instanziierung
    $app->config('cookies.lifetime', '20 minutes');

Datentyp
: integer|string

Standardwert
: "20 minutes"

### cookies.path

Legt den standardmäßig verwendeten Pfad des HTTP-Cookies fest, wenn beim Aufruf von `setCookie()` oder
`setEncryptedCookie()` keiner explizit angegeben wird.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.path' => '/'
    ));

    // Nach der Instanziierung
    $app->config('cookies.path', '/');

Datentyp
: string

Standardwert
: "/"

### cookies.domain

Legt den standardmäßig verwendete Domain des HTTP-Cookies fest, wenn beim Aufruf von `setCookie()` oder
`setEncryptedCookie()` keine festgelegt wird.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.domain' => 'domain.com'
    ));

    // Nach der Instanziierung
    $app->config('cookies.domain', 'domain.com');

Datentyp
: string

Standardwert
: null

### cookies.secure

Legt fest ob Cookies ausschließlich über HTTPS übertragen werden. Dieser Wert kann beim Aufruf von `setCookie()` oder
`setEncryptedCookie()` überschrieben werden.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.secure' => false
    ));

    // Nach der Instanziierung
    $app->config('cookies.secure', false);

Datentyp
: boolean

Standardwert
: false

### cookies.httponly

Determines whether or not cookies are delivered only via the HTTP protocol. You may override this setting when invoking
the Slim application's `setCookie()` or `setEncryptedCookie()` methods.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.httponly' => false
    ));

    // Nach der Instanziierung
    $app->config('cookies.httponly', false);

Datentyp
: boolean

Standardwert
: false

### cookies.secret_key

Der Schlüssel, der zur Verschlüsselung des Cookies verwendet wird. Diese Einstellung sollte unbedingt geändert 
werden wenn du verschlüselte HTTP-Cookies verwendest.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.secret_key' => 'secret'
    ));

    // Nach der Instanziierung
    $app->config('cookies.secret_key', 'secret');

Datentyp
: string

Standardwert
: "CHANGE_ME"

### cookies.cipher

Das verwendete mcrypt-Verschlüsselungsverfahren zum Verschlüsseln des HTTP-Cookies. Siehe [verfügbare Verfahren](http://php.net/manual/de/mcrypt.ciphers.php).

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.cipher' => MCRYPT_RIJNDAEL_256
    ));

    // Nach der Instanziierung
    $app->config('cookies.cipher', MCRYPT_RIJNDAEL_256);

Datentyp
: integer

Standardwert
: MCRYPT_RIJNDAEL_256

### cookies.cipher_mode

Der verwendete mcrypt-Verschlüsselungsmodus beim Verschlüsseln des HTTP-Cookies. Siehe [verfügbare Modi](http://php.net/manual/de/mcrypt.ciphers.php).

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

    // Nach der Instanziierung
    $app->config('cookies.cipher_mode', MCRYPT_MODE_CBC);

Datentyp
: integer

Standardwert
: MCRYPT_MODE_CBC

### http.version

Standardmäßig gibt Slim eine HTTP/1.1 Antwort an den Client zurück. Mit dieser Einstellung kannst du die Version des
HTTP-Protokols festlegen (z.B. HTTP/1.0). Dies ist nützlich wenn du PHPFog oder einen nginx-Server verwendest und mit einem
Backend-Proxy kommunizierst, anstatt direkt mit einem HTTP-Client.

    <?php
    // Während der Instanziierung
    $app = new \Slim\Slim(array(
        'http.version' => '1.1'
    ));

    // Nach der Instanziierung
    $app->config('http.version', '1.1');

Datentyp
: string

Standardwert
: "1.1"
