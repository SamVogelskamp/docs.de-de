---
title: 'Vorgehensweise: Angeben einer Clientbindung in einer Konfiguration'
ms.date: 03/30/2017
ms.assetid: 4a7c79aa-50ee-4991-891e-adc0599323a7
ms.openlocfilehash: e2ea5a4b1c2ca9b661be5d4c653a3b5668bd26f5
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33499059"
---
# <a name="how-to-specify-a-client-binding-in-configuration"></a>Vorgehensweise: Angeben einer Clientbindung in einer Konfiguration
In diesem Beispiel wird eine Client-Konsolenanwendung erstellt, um einen Rechnerdienst zu nutzen, und die Bindung dieses Clients wird deklarativ in der Konfiguration angegeben. Der Client greift auf den `CalculatorService` zu, der die `ICalculator`-Schnittstelle implementiert, und sowohl der Dienst als auch der Client verwenden die Klasse <xref:System.ServiceModel.BasicHttpBinding>.  
  
 In der umrissenen Prozedur wird davon ausgegangen, dass der Rechnerdienst ausgeführt wird. Informationen zum Erstellen des Diensts finden Sie unter [wie: Angeben einer Dienstbindung in einer Konfiguration](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md). Darüber hinaus verwendet der [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) , dass Windows Communication Foundation (WCF) bereitstellt, um die Clientkomponenten automatisch zu generieren. Das Tool generiert den Clientcode und die Konfiguration zum Zugreifen auf den Dienst.  
  
 Der Client wird in zwei Schritten erstellt. Svcutil.exe generiert den `ClientCalculator`, der die `ICalculator`-Schnittstelle implementiert. Diese Clientanwendung wird dann durch das Erstellen einer Instanz von `ClientCalculator` erstellt.  
  
 Normalerweise ist es die bewährte Methode, die Bindung anzugeben und die Informationen deklarativ in der Konfiguration anzusprechen anstatt imperativ im Code. Die Definition von Endpunkten im Code ist normalerweise nicht geeignet, da die Bindungen und Adressen für einen bereitgestellten Dienst sich in der Regel von denen unterscheiden, die während der Entwicklung des Diensts verwendet werden. Allgemeiner gesagt ist es durch die Trennung von Bindungs- und Adressierungsinformationen vom Code möglich, diese zu ändern, ohne die Anwendung neu kompilieren oder erneut bereitstellen zu müssen.  
  
 Sie können alle der folgenden Konfigurationsschritte ausführen, mit der [Dienstkonfigurations-Editor-Tool (SvcConfigEditor.exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  
  
 Eine Kopie der Quelle dieses Beispiels, finden Sie unter der [Standardbindung](../../../docs/framework/wcf/samples/basicbinding.md) Beispiel.  
  
### <a name="specifying-a-client-binding-in-configuration"></a>Eine Clientbindung in einer Konfiguration angeben  
  
1.  Verwenden Sie Svcutil.exe in der Befehlszeile, um Code von Dienstmetadaten zu generieren.  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Der generierte Client enthält die `ICalculator`-Schnittstelle, die den Dienstvertrag definiert, dem die Clientimplementierung entsprechen muss.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#1)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#1)]  
  
3.  Der generierte Client enthält außerdem die Implementierung vom `ClientCalculator`.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#2)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#2)]  
  
4.  Svcutil.exe generiert auch die Konfiguration für den Client, der die <xref:System.ServiceModel.BasicHttpBinding>-Klasse verwendet. Wenn Sie Visual Studio verwenden möchten, nennen Sie diese Datei "App.config". Beachten Sie, dass die Adresse und die Bindungsinformationen in der Implementierung des Diensts nirgendwo angegeben werden. Es muss auch kein Code geschrieben werden, um Informationen aus der Konfigurationsdatei abzurufen.  
  
     [!code-xml[C_HowTo_ConfigureClientBinding#100](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/common/client.exe.config#100)]   
            
5.  Erstellen Sie eine Instanz des `ClientCalculator` in einer Anwendung, und rufen Sie dann die Dienstvorgänge auf.  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/client.cs#3)]  
  
6.  Kompilieren Sie den Code, und führen Sie den Client aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von Bindungen, um Dienste und Clients zu konfigurieren](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)
