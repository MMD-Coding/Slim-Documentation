---
title: Response Cookies
status: live
---

Die Slim application stellt Helper Methoden bereit, um Cookies mit dem HTTP Response mitzusenden.

### Cookie setzen

Das folgende Beispiel demonstriert, wie mit Hilfe der `setCookie()` Methode ein HTTP Cookie erzeugt werden kann,
das dann mit dem HTTP Response mitgesendet wird.

    <?php
    $app->setCookie('foo', 'bar', '2 days');

Das Beispiel erzeugt ein HTTP Cookie mit dem Namen "foo" und dem Inhalt "bar", das in zwei Tagen ab sofort abläuft.
Es können außerdem zusätzliche Cookie Eigenschaften (z.B. Pfad, Domain, Secure, httponly) bereitgestellt werden.
Die `setCookie()` Methode von Slim benutzt dieselbe Signatur wie die native `setCookie()` Funktion von PHP.

    <?php
    $app->setCookie(
        $name,
        $value,
        $expiresAt,
        $path,
        $domain,
        $secure,
        $httponly
    );

### Ein verschlüsseltes Cookie setzen

Um den Response eines Cookies zu verschlüsseln, muss die Slim Eigenschaft `cookies.encrypt` auf `true` gesetzt werden.
Ist dieser Wert `true`, wird Slim den Response des Cookies automatisch vor Auslieferung an den Client verschlüsseln.

Folgende Einstellungen für die Verschlüsselung von Cookies stehen zur Verfügung:

    <?php
    $app = new \Slim\Slim(array(
        'cookies.encrypt' => true,
        'cookies.secret_key' => 'my_secret_key',
        'cookies.cipher' => MCRYPT_RIJNDAEL_256,
        'cookies.cipher_mode' => MCRYPT_MODE_CBC
    ));

### Cookie löschen

Ein Cookie kann mit Hilfe der `deleteCookie()` Methode gelöscht werden. Das Cookie wird so vor dem nächsten HTTP Request
beim Client gelöscht. Die Methode akzeptiert dieselbe Signatur wie die `setCookie()` Instanzmethode, allerdings *ohne* das `$expires`
Argument. Lediglich das erste Argument ist benötigt.

    <?php
    $app->deleteCookie('foo');

Muss zusätzlich der Pfad und die Domain angegeben werden:

    <?php
    $app->deleteCookie('foo', '/', 'foo.com');

Außerdem können die secure und httponly Eigenschaften übergeben werden:	

    <?php
    $app->deleteCookie('foo', '/', 'foo.com', true, true);
