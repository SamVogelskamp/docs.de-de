---
title: Asynchrone nachrichtenbasierte Kommunikation
description: .NET-Microservicesarchitektur für .NET-Containeranwendungen | Asynchrone nachrichtenbasierte Kommunikation
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: 865966a70f18c9023e4c733d82ea90aba9478753
ms.sourcegitcommit: 9bd8f213b50f0e1a73e03bd1e840c917fbd6d20a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/27/2018
ms.locfileid: "50135374"
---
# <a name="asynchronous-message-based-communication"></a>Asynchrone nachrichtenbasierte Kommunikation

Asynchrone nachrichtenbasierte und ereignisgesteuerte Kommunikation ist von entscheidender Bedeutung, wenn Änderungen an mehrere Microservices und ihre zugehörigen Domänenmodelle weitergegeben werden. Wie bereits in einem anderen Artikel über Microservices und begrenzte Kontexte erwähnt wurde, können Modelle (Benutzer, Kunde, Produkt, Konto usw.) unterschiedliche Auswirkungen auf verschiedene Microservices oder begrenzte Kontexte haben. Wenn also Änderungen auftreten, muss ihre Umsetzung in den unterschiedlichen Modellen abgestimmt werden. Eine Lösung für dieses Problem besteht in letztlicher Konsistenz und ereignisgesteuerter Kommunikation, die auf asynchronem Messaging beruht.

Bei der Verwendung von Messaging kommunizieren Prozesse durch den asynchronen Nachrichtenaustausch. Ein Client sendet über eine Nachricht einen Befehl oder eine Anforderung an einen Dienst. Wenn der Dienst antworten muss, sendet er eine andere Nachricht zurück an den Client. Da es sich um nachrichtenbasierte Kommunikation handelt, nimmt der Client an, dass die Antwort nicht sofort empfangen wird und dass möglicherweise überhaupt keine Antwort zurückgegeben wird.

Eine Nachricht setzt sich aus einem Header (Metadaten zur Identifizierung und Sicherheit) und dem Nachrichtentext zusammen. Nachrichten werden in der Regel über asynchrone Protokolle wie AMQP gesendet.

Die bevorzugte Infrastruktur für diese Art der Kommunikation ist in der Microservicescommunity ein schlanker Nachrichtenbroker, der sich von großen Brokern und Orchestratoren unterscheidet, die in einer SOA-Architektur verwendet werden. In einem schlanken Nachrichtenbroker hat die Infrastruktur nur die Aufgabe, als Nachrichtenbroker zu agieren, der auf einfachen Implementierungen wie RabbitMQ oder einem skalierbaren Servicebus in der Cloud wie Azure Service Bus basiert. In diesem Szenario werden wichtige Entscheidungen nach wie vor in den Endpunkten, die Nachrichten erzeugen und nutzen, und damit in den Microservices getroffen.

Sie sollten außerdem versuchen, für die Kommunikation zwischen internen Diensten nur asynchrones Messaging und für Nachrichten von Clientanwendungen an Front-End-Dienste (API-Gateways und zusätzlich die erste Ebene von Microservices) ausschließlich die synchrone Kommunikation (z.B. über HTTP) zu verwenden.

Unterschieden wird bei asynchronem Messaging zwischen nachrichtenbasierter Kommunikation mit einem Empfänger und nachrichtenbasierte Kommunikation mit mehreren Empfängern. In den folgenden Abschnitten erfahren Sie mehr über diese beiden Ansätze.

## <a name="single-receiver-message-based-communication"></a>Nachrichtenbasierte Kommunikation mit einem Empfänger 

Bei der asynchronen nachrichtenbasierten Kommunikation mit einem Empfänger wird eine Punkt-zu-Verbindung hergestellt, bei der genau ein Consumer, der den Kanal liest, die Nachricht erhält. Dabei wird die Nachricht nur einmal verarbeitet. Es gibt jedoch Situationen, in denen dies anders ist. In einem Cloudsystem, das automatisch versucht, Fehler zu beheben, könnte dieselbe Nachricht z.B. mehrere Male gesendet werden. Aufgrund von Netzwerkfehlern oder anderen Fehlern muss der Client in der Lage sein, Nachrichten erneut zu senden. Der Server muss außerdem einen idempotenten Vorgang implementieren, um eine bestimmte Nachricht nur einmal verarbeiten zu müssen.

Wie in Abbildung 4-18 dargestellt wird, eigent sich die nachrichtenbasierte Kommunikation mit einem Empfänger besonders gut für das Senden asynchroner Befehle von einem Microservice zu einem anderen.

Nachdem Sie die nachrichtenbasierte Kommunikation mithilfe von Befehlen oder Ereignissen gestartet haben, sollten Sie sie nicht zusammen mit der synchronen HTTP-Kommunikation verwenden.

![](./media/image18.PNG)

**Abbildung 4-18.** Ein einzelner Microservice empfängt eine asynchrone Nachricht

Beachten Sie, dass Befehle, die von Clientanwendungen ausgehen, als synchrone HTTP-Befehle implementiert werden können. Nachrichtenbasierte Befehle empfehlen sich, wenn Sie auf höhere Skalierbarkeit angewiesen sind oder bereits über einen nachrichtenbasierten Geschäftsprozess verfügen.

## <a name="multiple-receivers-message-based-communication"></a>Nachrichtenbasierte Kommunikation mit mehreren Empfängern 

Wenn Sie einen flexibleren Ansatz benötigen, können Sie auch einen Veröffentlichen/Abonnieren-Vorgang verwenden, damit die Nachrichten des Senders zusätzlichen Abonnentenmicroservices oder externen Anwendungen zur Verfügung gestellt werden. Es empfiehlt sich daher, dem [Offen/Geschlossen-Prinzip](https://en.wikipedia.org/wiki/Open/closed_principle) im sendenden Dienst zu folgen. Auf diese Weise können später zusätzliche Abonnenten hinzugefügt werden, ohne dass der sendende Dienst geändert wird.

Wenn Sie die Veröffentlichen/Abonnieren-Kommunikation verwenden, können Sie z.B. eine Ereignisbusschnittstelle nutzen, um Ereignisse für Abonnenten zu veröffentlichen.

## <a name="asynchronous-event-driven-communication"></a>Asynchrone ereignisgesteuerte Kommunikation

Bei Verwendung der asynchronen ereignisgesteuerten Kommunikation veröffentlicht ein Microservice ein Integrationsereignis, wenn eine Änderung in der zugehörigen Domäne eintritt und ein anderer Microservice darüber informiert werden muss (beispielsweise im Fall einer Preisänderung in einem Microservice für einen Produktkatalog). Zusätzliche Microservices abonnieren die Ereignisse, damit sie sie asynchron empfangen können. In diesem Fall aktualisieren die Empfänger möglicherweise ihre eigenen Domänenentitäten, was dazu führen kann, dass weitere Integrationsereignisse veröffentlicht werden. Dieses System des Veröffentlichens/Abonnierens erfolgt in der Regel über die Implementierung eines Ereignisbusses. Der Ereignisbus kann als Abstraktion oder Schnittstelle entworfen werden und verfügt über eine API, die für das Abonnieren oder Abbestellen und für das Veröffentlichen von Ereignissen benötigt wird. Des Weiteren kann der Ereignisbus über mindestens eine Implementierung verfügen, die auf einem Nachrichtenbroker für die prozessübergreifende Kommunikation basiert. Beispiele hierfür sind Nachrichtenwarteschlangen oder Service Busse, die die asynchrone Kommunikation und ein Veröffentlichen/Abonnieren-Modell unterstützen.

Wenn ein System letztliche Konsistenz verwendet, die durch Integrationsereignisse gesteuert wird, sollte dieser Ansatz dem Endbenutzer verdeutlicht werden. Das System sollten keinen Ansatz verwenden, der Integrationsereignisse imitiert (wie etwa im Fall von SignalR oder beim Abruf von Clientsystemen). Sowohl der Endbenutzer als auch der Geschäftsinhaber müssen die letztliche Konsistenz im System akzeptieren und erkennen, dass dieser Ansatz in Unternehmen häufig kein Problem darstellt, solange er explizit dargelegt wird.

Wie bereits unter [Challenges and solutions for distributed data management (Herausforderungen und Lösungen für die verteilte Datenverwaltung)](#challenges-and-solutions-for-distributed-data-management) beschrieben wurde, können Sie Integrationsereignisse dazu nutzen, microserviceübergreifende Geschäftsaufgaben zu implementieren. Dadurch kommt es zu letztlicher Konsistenz zwischen diesen Diensten. Eine letztlich konsistente Transaktion besteht aus einer Reihe von verteilten Aktionen. Bei jeder Aktion aktualisiert der zugehörige Microservice eine Domänenentität und veröffentlicht ein weiteres Integrationsereignis, das die nächste Aktion innerhalb derselben End-to-End-Geschäftsaufgabe auslöst.

Zu beachten ist, dass Sie möglicherweise mit mehreren Microservices kommunizieren müssen, die für dasselbe Ereignis abonniert sind. Dazu können Sie das Veröffentlichen/Abonnieren-Messaging verwenden, das auf ereignisgesteuerter Kommunikation basiert, wie in Abbildung 4-19 gezeigt wird. Dieser Veröffentlichen/Abonnieren-Ansatz kann nicht nur für die Microservicearchitektur genutzt werden. Vergleichbar ist die Funktionsweise dieses Ansatzes damit, wie [begrenzte Kontexte](https://martinfowler.com/bliki/BoundedContext.html) in DDD kommunizieren sollten oder wie Änderungen von der Schreibdatenbank zur Lesedatenbank im Architekturmuster [CQRS (Command and Query Responsibility Segregation; Zuständigkeitstrennung für Befehle und Abfragen)](https://martinfowler.com/bliki/CQRS.html) weitergegeben werden. Das Ziel ist letztliche Konsistenz zwischen mehreren Datenquellen im verteilten System.

![](./media/image19.png)

**Abbildung 4-19.** Asynchrone ereignisgesteuerte Nachrichtenkommunikation

Die Implementierung bestimmt darüber, welches Protokoll für die ereignisgesteuerte Nachrichtenkommunikation verwendet wird. [AMQP](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol) kann dazu beitragen, eine zuverlässige Kommunikation unter Verwendung von Warteschlangen zu gewährleisten.

Bei der Nutzung eines Ereignisbusses empfiehlt sich eine Abstraktionsebene (beispielsweise eine Ereignisbusschnittstelle), die auf einer zugehörigen Implementierung in Klassen mit Code basiert, der die API eines Nachrichtenbrokers wie [RabbitMQ](https://www.rabbitmq.com/) oder eines Service Busses wie [Azure Service Bus mit Themen](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions) verwendet. Alternativ können Sie auch Service Busse auf höherer Ebene wie NServiceBus, MassTransit oder Brighter verwenden, um den Ereignisbus und das Veröffentlichen/Abonnieren-System umzusetzen.

## <a name="a-note-about-messaging-technologies-for-production-systems"></a>Hinweis zu Messagingtechnologien für Produktionssysteme

Die Messagingtechnologien zur Implementierung eines abstrakten Ereignisbusses werden auf unterschiedlichen Ebenen eingesetzt. Produkte wie RabbitMQ (ein Nachrichtenbroker) und Azure Service Bus sind auf einer niedrigeren Ebene anzusiedeln als andere Produkte wie NServiceBus, MassTransit oder Brighter, die zusätzlich zu RabbitMQ und Azure Service Bus verwendet werden können. Die Auswahl des geeigneten Produkts hängt davon ab, welchen Funktionsumfang auf der Anwendungsebene und welche Standardskalierbarkeit Sie für die Anwendung benötigen. Für die Implementierung eines Proof-of-Concept-Ereignisbusses für eine Entwicklungsumgebung (s. eShopOnContainers-Beispiel) ist eine einfache Implementierung zusätzlich zu einer im Docker-Container ausgeführten RabbitMQ-Installation möglicherweise ausreichend.

Für unternehmenskritische Systeme und Produktionssysteme, für die eine sehr hohe Skalierbarkeit erforderlich ist, sollten Sie jedoch Azure Service Bus testen und verwenden. Für auf höherer Ebene angesiedelte Abstraktionen und Features, die die Entwicklung von verteilten Anwendungen vereinfachen, empfehlen sich andere kommerzielle Busse und Open Source-Service Busse wie NServiceBus, MassTransit und Brighter. Selbstverständlichen können Sie auch eigene Dienstbusfeatures erstellen, die auf Technologien wie RabbitMQ und Docker für niedrigere Ebenen basieren. Sie sollten jedoch beachten, dass Eigenentwicklungen für eine individuelle Unternehmensanwendung möglicherweise zu kostspielig sind.

## <a name="resiliently-publishing-to-the-event-bus"></a>Resilientes Veröffentlichen im Ereignisbus

Eine Herausforderung beim Implementieren einer ereignisgesteuerten Architektur für mehrere Microservices besteht darin, den Zustand durch einen unteilbaren Vorgang im ursprünglichen Microservice zu aktualisieren, während das zugehörige Integrationsereignis auf der Grundlage von Transaktionen resilient im Ereignisbus veröffentlicht wird. Die folgende Liste, die allerdings nicht zwangsläufig vollständig ist, enthält mehrere Ansätze zur Lösung dieses Problems:

-   Verwenden einer Transaktionswarteschlange wie MSMQ, die auf DTC basiert (dieser Ansatz ist allerdings bereits älter und wird nicht mehr empfohlen).

-   Verwenden von [Transaktionsprotokollmining](https://www.scoop.it/t/sql-server-transaction-log-mining).

-   Verwenden des [Musters „Ereignissourcing“](https://msdn.microsoft.com/library/dn589792.aspx).

-   Verwenden des [Musters „Postausgang“](http://gistlabs.com/2014/05/the-outbox/). Hierbei bildet eine Transaktionsdatenbanktabelle als Nachrichtenwarteschlange die Basis für eine Ereigniserstellerkomponente, die das Ereignis erstellt und veröffentlicht.

Bei der Verwendung der asynchronen Kommunikation sollten darüber hinaus die Idempotenz und die Deduplizierung von Nachrichten berücksichtigt werden. Diese Themen werden an anderer Stelle in diesem Leitfaden unter [Implementieren ereignisbasierter Kommunikation zwischen Microservices (Integrationsereignissen)](#implementing_event_based_comms_microserv) behandelt.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

-   **Event Driven Messaging (Ereignisgesteuertes Messaging)**
    [*http://soapatterns.org/design\_patterns/event\_driven\_messaging*](http://soapatterns.org/design_patterns/event_driven_messaging)

-   **Publish/Subscribe Channel (Veröffentlichungs-/Abonnementkanal)**
    [*https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html*](https://www.enterpriseintegrationpatterns.com/patterns/messaging/PublishSubscribeChannel.html)

-   **Udi Dahan. Clarified CQRS (Erläuterung zu CQRS)**
    [*http://udidahan.com/2009/12/09/clarified-cqrs/*](http://udidahan.com/2009/12/09/clarified-cqrs/)

-   **Command and Query Responsibility Segregation (CQRS) (Zuständigkeitstrennung für Befehle und Abfragen (CQRS))**
    [*https://docs.microsoft.com/azure/architecture/patterns/cqrs*](https://docs.microsoft.com/azure/architecture/patterns/cqrs)

-   **Communicating Between Bounded Contexts (Kommunizieren zwischen gebundenen Kontexten)**
    [*https://msdn.microsoft.com/library/jj591572.aspx*](https://msdn.microsoft.com/library/jj591572.aspx)

-   **Eventual consistency (Letztliche Konsistenz)**
    [*https://en.wikipedia.org/wiki/Eventual\_consistency*](https://en.wikipedia.org/wiki/Eventual_consistency)

-   **Jimmy Bogard. Refactoring Towards Resilience: Evaluating Coupling (Refactoring für die Dienstbeständigkeit: Eine Beurteilung der Kopplung)**
    [*https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/*](https://jimmybogard.com/refactoring-towards-resilience-evaluating-coupling/)


>[!div class="step-by-step"]
[Zurück](communication-in-microservice-architecture.md)
[Weiter](maintain-microservice-apis.md)
