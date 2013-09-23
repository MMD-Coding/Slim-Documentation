---
title: Response Status
status: live
---

Der an den Client zurückgelieferte HTTP Response besitzt einen Status Code, der den Typ des Responses
charakterisiert (zum Bespiel 200 OK, 400 Bad Request oder 500 Server Error). Über das Response Objekt der Slim
Application kann der HTTP Status Code manuell gesetzt werden:

    <?php
    $app->response->setStatus(400);

Ist es gewünscht, einen **anderen** Status als 200 OK zurückzuliefern, muss dieser lediglich auf dem Objekt gesetzt werden.
Der aktuelle Status des Response Objektes kann über die folgende Methode ausgelesen werden:

    <?php
    $status = $app->response->getStatus();
	