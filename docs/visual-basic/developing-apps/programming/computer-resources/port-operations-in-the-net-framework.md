---
title: Operationen für serielle Anschlüsse in .NET Framework mit Visual Basic
ms.date: 07/20/2015
helpviewer_keywords:
- ports, Visual Basic
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
ms.openlocfilehash: 66b3729081540e8dede42556c58e44cd55b62666
ms.sourcegitcommit: 412bbc2e43c3b6ca25b358cdf394be97336f0c24
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2018
ms.locfileid: "42925710"
---
# <a name="port-operations-in-the-net-framework-with-visual-basic"></a>Operationen für serielle Anschlüsse in .NET Framework mit Visual Basic
Sie können auf die seriellen Anschlüsse Ihres Computers über die [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]-Klassen im Namespace <xref:System.IO.Ports?displayProperty=nameWithType> zugreifen. Die wichtigste Klasse, <xref:System.IO.Ports.SerialPort>, bietet ein Framework für synchrone und ereignisgesteuerte E/A-Vorgänge, Zugriff auf Pin- und Unterbrechungszustände sowie Zugriff auf die Treibereigenschaften für den seriellen Anschluss. Sie kann von einem <xref:System.IO.Stream>-Objekt umschlossen werden, auf das durch die Eigenschaft <xref:System.IO.Ports.SerialPort.BaseStream> zugegriffen werden kann. Durch die Umschließung von <xref:System.IO.Ports.SerialPort> in einem <xref:System.IO.Stream>-Objekt kann auf den seriellen Anschluss von Klassen zugegriffen werden, die Streams verwenden. Der Namespace enthält Enumerationen, die die Steuerung von seriellen Anschlüssen vereinfacht.  
  
 Die einfachste Möglichkeit zum Erstellen eines <xref:System.IO.Ports.SerialPort>-Objekts besteht darin, die Methode <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> zu verwenden.  
  
> [!NOTE]
>  Sie können [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)]-Klassen nicht verwenden, um direkt auf andere Porttypen wie Parallelanschlüsse, USB-Anschlüsse usw. zuzugreifen.  
  
## <a name="enumerations"></a>Enumerationen  
 Diese Tabelle enthält und beschreibt die wichtigsten Enumerationen für den Zugriff auf einen seriellen Anschluss:  
  
|Enumeration|Beschreibung |  
|---|---|   
|<xref:System.IO.Ports.Handshake>|Gibt das Steuerungsprotokoll an, das beim Herstellen einer Kommunikation eines seriellen Anschlusses für ein <xref:System.IO.Ports.SerialPort>-Objekt verwendet wird.|  
|<xref:System.IO.Ports.Parity>|Gibt das Paritätsbit für ein <xref:System.IO.Ports.SerialPort>-Objekt an.|  
|<xref:System.IO.Ports.SerialData>|Gibt den Zeichentyp an, der an einem seriellen Anschluss des <xref:System.IO.Ports.SerialPort>-Objekts empfangen wurde.|  
|<xref:System.IO.Ports.SerialError>|Gibt die Fehler für das <xref:System.IO.Ports.SerialPort>-Objekt an.|  
|<xref:System.IO.Ports.SerialPinChange>|Gibt die Art der Änderungen für das <xref:System.IO.Ports.SerialPort>-Objekt an.|  
|<xref:System.IO.Ports.StopBits>|Gibt die Anzahl von Stoppbits an, die das <xref:System.IO.Ports.SerialPort>-Objekt verwendet.|  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.VisualBasic.Devices.Ports>  
 [Zugreifen auf die Anschlüsse des Computers](../../../../visual-basic/developing-apps/programming/computer-resources/accessing-the-computer-s-ports.md)
