---
title: HTTP Caching Übersicht
status: live
---

Eine Slim Applikation bietet integrierte Unterstützung für HTTP Caching. Hierfür stehen die Helper Methoden
`etag()`, `lastModified()` und `expires()` zur Verfügung. Empfohlen wird die Benutzung von `etag()` oder
`lastModified()` in Verbindung mit `expires()` pro Route. `etag()` und `lastModified()` sollten nie gemeinsam
in derselben Routen Callback Funktion verwendet werden.

Die Methoden `etag()` und `lastModified()` sollten in einer Routen Callback Funktion vor dem restlichen Code
ausgeführt werden. Slim ist es so möglich, den GET Request vor der Ausführung des restlichen Codes zu überprüfen.

Sowohl `etag()` als auch `lastModified()` weisen den HTTP Client an, den Response der Ressource in einem clientseitigen
Cache abzulegen. Die `expires()` Methode vermittelt dem HTTP Client, wann der clientseitige Cache der Ressource abläuft.
