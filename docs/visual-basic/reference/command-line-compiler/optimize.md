---
title: -Optimierung
ms.date: 07/20/2015
helpviewer_keywords:
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization [Visual Basic], enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
ms.openlocfilehash: 2f066835c5f864538f281d4c58772e0e60c132f2
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33649944"
---
# <a name="-optimize"></a>-Optimierung
Aktiviert oder deaktiviert compileroptimierungen.  
  
## <a name="syntax"></a>Syntax  
  
```  
-optimize[ + | - ]  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Definition|  
|---|---|  
|`+` &#124; `-`|Dies ist optional. Die `-optimize-` -Option deaktiviert compileroptimierungen. Die `-optimize+` Option Optimierungen aktiviert. Optimierungen sind standardmäßig deaktiviert.|  
  
## <a name="remarks"></a>Hinweise  
 Durch Compileroptimierungen wird Ihre Ausgabedatei kleiner, schneller und effizienter. Jedoch, da Optimierungen führen zu neuanordnungen von Code in die Ausgabedatei `-optimize+` können das Debuggen erschwert.  
  
 Alle Module mit generiert `-target:module` für eine Assembly, die die gleiche verwenden muss `-optimize` Einstellungen wie die Assembly. Weitere Informationen finden Sie unter [-Ziel (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md).  
  
 Sie können Kombinieren der `-optimize` und `-debug` Optionen.  
  
|Zum Festlegen von - Optimierung in der integrierten Entwicklungsumgebung von Visual Studio|  
|---|  
|1.  Ein Projekt auswählen in **Projektmappen-Explorer**. Klicken Sie im Menü **Projekt** auf **Eigenschaften**.<br />     <br />2.  Klicken Sie auf die Registerkarte **Kompilieren**.<br />3.  Klicken Sie auf die Schaltfläche **Erweitert** .<br />4.  Ändern der **Optimierungen aktivieren** Kontrollkästchen.|  
  
## <a name="example"></a>Beispiel  
 Der folgende code kompiliert `T2.vb` und compileroptimierungen aktiviert.  
  
```console
vbc t2.vb -optimize  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)  
 [-Debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)  
 [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)  
 [-Ziel (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
