---
title: Angeben einer Endpunktadresse
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- endpoints [WCF], addressing
ms.assetid: ac24f5ad-9558-4298-b168-c473c68e819b
ms.openlocfilehash: 718a0c086181546ba7b7fb3b31fce0732dd99382
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43517115"
---
# <a name="specifying-an-endpoint-address"></a>Angeben einer Endpunktadresse
Die gesamte Kommunikation mit einem Windows Communication Foundation (WCF)-Dienst erfolgt über dessen Endpunkte. Jeder <xref:System.ServiceModel.Description.ServiceEndpoint> enthält eine <xref:System.ServiceModel.Description.ServiceEndpoint.Address%2A>, eine <xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A> und einen <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A>. Der Vertrag gibt an, welche Vorgänge verfügbar sind. Die Bindung gibt an, wie eine Kommunikation mit dem Dienst stattfindet, und die Adresse gibt an, wo sich der Dienst befindet. Jeder Endpunkt muss eine eindeutige Adresse haben. Die Endpunktadresse wird durch die <xref:System.ServiceModel.EndpointAddress>-Klasse dargestellt, die einen Uniform Resource Identifier (URI) enthält, der die Adresse des Diensts darstellt, eine <xref:System.ServiceModel.EndpointAddress.Identity%2A>, die die Sicherheitsidentität des Diensts darstellt, und eine Auflistung der optionalen <xref:System.ServiceModel.EndpointAddress.Headers%2A>. Die optionalen Header stellen zusätzliche, ausführlichere Adressinformationen bereit, um den Endpunkt zu identifizieren oder mit ihm zu interagieren. Die Header können beispielsweise angeben, wie eine eingehende Nachricht zu bearbeiten ist, wohin der Endpunkt eine Antwortnachricht senden sollte, oder welche Instanz eines Diensts für die Bearbeitung einer eingehenden Nachricht verwendet werden soll, wenn mehrere Instanzen verfügbar sind.  
  
## <a name="definition-of-an-endpoint-address"></a>Definition einer Endpunktadresse  
 In WCF ein <xref:System.ServiceModel.EndpointAddress> Modelliert einen Endpunktverweis (EPR), wie in der WS-Adressierungsstandard definiert.  
  
 Der Adress-URI besteht für die meisten Transporte aus vier Teilen. Z. B. diesen URI `http://www.fabrikam.com:322/mathservice.svc/secureEndpoint` besteht aus folgenden vier Teilen:  
  
-   Schema: http:  
  
-   Computer: `www.fabrikam.com`  
  
-   (Optional) Port: 322  
  
-   Pfad: /mathservice.svc/secureEndpoint  
  
 Bestandteil des EPR-Modells ist, dass jeder Endpunktverweis einige Verweisparameter enthalten kann, die weitere identifizierende Informationen liefern. In WCF diese Endpunktverweise als Instanzen der <xref:System.ServiceModel.Channels.AddressHeader> Klasse.  
  
 Die Endpunktadresse für einen Dienst kann entweder verbindlich mithilfe von Code oder deklarativ durch die Konfiguration angegeben werden. Die Definition von Endpunkten im Code ist normalerweise nicht geeignet, da die Bindungen und Adressen für einen bereitgestellten Dienst sich in der Regel von denen unterscheiden, die während der Entwicklung des Diensts verwendet werden. Im Allgemeinen ist es praktischer, Dienstendpunkte nicht mit Code, sondern mit Konfiguration zu definieren. Werden die Bindung und die Adressinformationen nicht in den Code integriert, ist eine Änderung ohne Neukompilierung und erneute Bereitstellung der Anwendung möglich. Wenn im Code oder in der Konfiguration keine Endpunkte angegeben sind, fügt die Runtime einen Standardendpunkt für alle Basisadressen in jedem Vertrag hinzu, der vom Dienst implementiert wird.  
  
 Es gibt zwei Möglichkeiten, Endpunktadressen für einen Dienst in WCF anzugeben. Sie können eine absolute Adresse für jeden dem Dienst zugeordneten Endpunkt angeben, oder Sie können eine Basisadresse für den <xref:System.ServiceModel.ServiceHost> eines Diensts bereitstellen und dann eine relativ zu dieser Basisadresse definierte Adresse für jeden dem Dienst zugeordneten Endpunkt angeben. Sie können mit jedem dieser Verfahren entweder im Code oder in der Konfiguration die Endpunktadressen für einen Dienst angeben. Wenn Sie keine relative Adresse angeben, verwendet der Dienst die Basisadresse. Sie können für einen Dienst auch mehrere Adressen angeben, jedoch ist für jeden Dienst nur eine Basisadresse für jeden Transport zulässig. Wenn Sie mehrere Endpunkte haben, von denen jeder mit einer anderen Bindung konfiguriert ist, müssen deren Adressen eindeutig sein. Endpunkte, die die gleiche Bindung, aber verschiedene Verträge verwenden, können die gleiche Adresse verwenden.  
  
 Wenn Sie in IIS hosten, verwalten Sie die <xref:System.ServiceModel.ServiceHost>-Instanz nicht selbst. Für einen in IIS gehosteten Dienst ist die Basisadresse immer die in der SVC-Datei angegebene Adresse. Daher müssen Sie relative Endpunktadressen für IIS-gehostete Dienstendpunkte verwenden. Die Angabe einer voll qualifizierten Endpunktadresse kann zu Fehlern bei der Bereitstellung des Diensts führen. Weitere Informationen finden Sie unter [Bereitstellen eines IIS-gehosteten WCF-Diensts](../../../docs/framework/wcf/feature-details/deploying-an-internet-information-services-hosted-wcf-service.md).  
  
## <a name="defining-endpoint-addresses-in-configuration"></a>Definieren von Endpunktadressen in der Konfiguration  
 Verwenden Sie zum Definieren eines Endpunkts in einer Konfigurationsdatei das [ \<Endpunkt >](https://msdn.microsoft.com/library/13aa23b7-2f08-4add-8dbf-a99f8127c017) Element.  
  
 [!code-xml[S_UEHelloWorld#5](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp2.config#5)]  
  
 Wenn die <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> (d. h., wenn die hostanwendung versucht, den Dienst starten)-Methode aufgerufen wird, sucht das System nach einer [ \<Service >](../../../docs/framework/configure-apps/file-schema/wcf/service.md) Element mit einem Namensattribut, der angibt, "UE. Samples.HelloService". Wenn die [ \<Service >](../../../docs/framework/configure-apps/file-schema/wcf/service.md) Element gefunden wird, wird das System die angegebene Klasse geladen und erstellt Endpunkte mithilfe der in der Konfigurationsdatei bereitgestellten Endpunktdefinitionen. Dieser Mechanismus erlaubt Ihnen, mit nur zwei Zeilen Code einen Dienst zu laden und zu starten, ohne dass die Bindungs- und Adressierungsinformationen im Code enthalten sein müssen. Der Vorteil dieses Ansatzes zeigt sich darin, dass diese Änderungen ohne Neukompilierung oder erneute Bereitstellung der Anwendung durchgeführt werden können.  
  
 Die optionalen Header werden in deklariert eine [ \<Header >](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md). Folgendes ist ein Beispiel für die Elemente verwendet, um die Endpunkte für einen Dienst in einer Konfigurationsdatei angeben, die zwischen zwei Headern unterscheidet: "Gold"-Clients von `http://tempuri1.org/` und "Standard"-Clients von `http://tempuri2.org/`. Der Client, der diesen Dienst aufruft, müssen die entsprechenden [ \<Header >](../../../docs/framework/configure-apps/file-schema/wcf/headers-element.md) in der Konfigurationsdatei.  
  
 [!code-xml[S_UEHelloWorld#1](../../../samples/snippets/common/VS_Snippets_CFX/s_uehelloworld/common/serviceapp.config#1)]  
  
 Header können auch durch einzelne Nachrichten statt (wie vorher gezeigt) durch alle Nachrichten an einem Endpunkt festgelegt werden. Dies geschieht, indem mithilfe von <xref:System.ServiceModel.OperationContextScope> ein neuer Kontext in einer Clientanwendung erstellt wird, um der ausgehenden Nachricht einen benutzerdefinierten Header hinzuzufügen. Dies wird im folgenden Beispiel gezeigt.  
  
 [!code-csharp[OperationContextScope#4](../../../samples/snippets/csharp/VS_Snippets_CFX/operationcontextscope/cs/client.cs#4)]
 [!code-vb[OperationContextScope#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/operationcontextscope/vb/client.vb#4)]  
  
## <a name="endpoint-address-in-metadata"></a>Endpunktadresse in Metadaten  
 Eine Endpunktadresse wird in WSDL (Web Services Description Language) als ein WS-Addressierungs-`EndpointReference` (EPR)-Element innerhalb des `wsdl:port`-Elements des entsprechenden Endpunkts dargestellt. Der EPR enthält die Endpunktadresse sowie eventuelle Adresseigenschaften. Beachten Sie, dass der EPR in `wsdl:port` `soap:Address` ersetzt, wie im folgenden Beispiel gezeigt.  
  
  
  
## <a name="defining-endpoint-addresses-in-code"></a>Definieren von Endpunktadressen in Code  
 Eine Endpunktadresse kann mit der <xref:System.ServiceModel.EndpointAddress>-Klasse im Code erstellt werden. Der für die Endpunktadresse angegebene URI kann ein voll qualifizierter Pfad oder ein zur Basisadresse des Diensts relativer Pfad sein. Das folgende Codebeispiel zeigt, wie eine Instanz der <xref:System.ServiceModel.EndpointAddress>-Klasse erstellt und der <xref:System.ServiceModel.ServiceHost>-Instanz, die den Dienst hostet, hinzugefügt wird.  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie eine vollständige Endpunktadresse im Code angegeben wird.  
  
 [!code-csharp[S_UEHelloWorld#2](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#2)]  
  
 Das folgende Codebeispiel zeigt, wie der Basisadresse des Diensthosts eine relative Adresse ("MyService") hinzugefügt wird.  
  
 [!code-csharp[S_UEHelloWorld#3](../../../samples/snippets/csharp/VS_Snippets_CFX/s_uehelloworld/cs/snippet.cs#3)]  
  
> [!NOTE]
>  Eigenschaften von <xref:System.ServiceModel.Description.ServiceDescription> in der Dienstanwendung dürfen nicht im Anschluss an die <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A>-Methode auf <xref:System.ServiceModel.ServiceHostBase> geändert werden. Einige Member, wie die <xref:System.ServiceModel.ServiceHostBase.Credentials%2A>-Eigenschaft und die `AddServiceEndpoint`-Methoden auf <xref:System.ServiceModel.ServiceHostBase> und <xref:System.ServiceModel.ServiceHost>, lösen eine Ausnahme aus, wenn eine Änderung nach diesem Punkt stattfindet. Andere Member können geändert werden, wobei das Ergebnis jedoch nicht definiert ist.  
>   
>  Ähnlich verhält es sich mit den <xref:System.ServiceModel.Description.ServiceEndpoint>-Werten, die auf dem Client nach dem Aufruf von <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> auf <xref:System.ServiceModel.ChannelFactory> nicht geändert werden dürfen. Die <xref:System.ServiceModel.ChannelFactory.Credentials%2A>-Eigenschaft löst eine Ausnahme aus, wenn sie nach diesem Punkt geändert wird. Die anderen Clientbeschreibungswerte können ohne Fehler geändert werden, aber das Ergebnis ist nicht definiert.  
>   
>  Sowohl für den Dienst als auch den Client wird empfohlen, die Beschreibung vor dem Aufruf von <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> zu ändern.  
  
## <a name="using-default-endpoints"></a>Verwenden von Standardendpunkten  
 Wenn im Code oder in der Konfiguration keine Endpunkte angegeben sind, stellt die Runtime Standardendpunkte bereit, indem ein Standardendpunkt für alle Basisadressen in jedem Dienstvertrag, der vom Dienst implementiert wird, hinzugefügt wird. Die Basisadresse kann im Code oder in der Konfiguration angegeben werden, und die Standardendpunkte werden hinzugefügt, wenn <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> auf dem <xref:System.ServiceModel.ServiceHost> aufgerufen wird.  
  
 Wenn Endpunkte explizit bereitgestellt werden, können die Standardpunkte dennoch hinzugefügt werden, indem <xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints%2A> auf dem <xref:System.ServiceModel.ServiceHost> aufgerufen wird, bevor <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> aufgerufen wird. Weitere Informationen über Standardendpunkte, Bindungen und Verhalten finden Sie unter [Simplified Configuration (Vereinfachte Konfiguration)](../../../docs/framework/wcf/simplified-configuration.md) und [Simplified Configuration for WCF Services (Vereinfachte Konfiguration für WCF-Dienste)](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.ServiceModel.EndpointAddress>  
 [Dienstidentität und Authentifizierung](../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)  
 [Übersicht über die Endpunkterstellung](../../../docs/framework/wcf/endpoint-creation-overview.md)  
 [Hosting](../../../docs/framework/wcf/feature-details/hosting.md)
