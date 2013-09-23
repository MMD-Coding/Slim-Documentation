---
title: Response Übersicht
status: live
---

Jede Instanz der Slim Applikation besitzt ein Response Objekt. Das Response Objekt ist eine Abstraktion des HTTP
Response der jeweiligen Slim Applikation, die vom HTTP Client zurückgeliefert wird. Obwohl jede Slim Applikation
ein Standard Default Objekt (`Slim\Http\Response`) zur Verfügung stellt, ist die Klasse idempotent. Bei Bedarf kann
die Klasse (in einer Middleware oder an einer anderen Stelle der Slim Applikation) instanziert werden, ohne das Verhalten
der Applikation als Ganzes zu beeinträchtigen. Die aktuelle Referenz auf das Response Objekt erhält man folgendermaßen:

    <?php
    $app = new \Slim\Slim();
    $app->response;

Ein HTTP Response enthält drei primäre Eigenschaften:

* Status
* Header
* Body

Das Response Objekt stellt Helper Methoden (nachfolgend beschrieben) bereit, die die Interaktion mit den Eigenschaften des
HTTP Response ermöglichen. Das Standard Response Objekt liefert einen **200 OK** HTTP Response mit dem Content-Type **text/html**.