---
title: 'Gewusst wie: Datennavigation mithilfe des BindingNavigator-Steuerelements in Windows Forms'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- BindingNavigator control [Windows Forms], navigating data
- data [Windows Forms], navigating
- data navigation
- examples [Windows Forms], BindingNavigator control
ms.assetid: 0e5d4f34-bc9b-47cf-9b8d-93acbb1f1dbb
ms.openlocfilehash: 14f845e33b38da39b900b32c07297a350326350d
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43519612"
---
# <a name="how-to-navigate-data-with-the-windows-forms-bindingnavigator-control"></a>Gewusst wie: Datennavigation mithilfe des BindingNavigator-Steuerelements in Windows Forms
Die Einführung des <xref:System.Windows.Forms.BindingNavigator>-Steuerelements in Windows Forms ermöglicht es Entwicklern, Endbenutzern eine einfache Benutzeroberfläche für die Datennavigation und -bearbeitung auf den Formularen bereitzustellen, die sie erstellen.  
  
 Das <xref:System.Windows.Forms.BindingNavigator>-Steuerelement ist ein <xref:System.Windows.Forms.ToolStrip>-Steuerelement mit Schaltflächen, die für die Navigation zum ersten, letzten, nächsten und vorherigen Datensatz in einem Dataset vorkonfiguriert sind, sowie mit Schaltflächen zum Hinzufügen und Löschen von Datensätzen. Schaltflächen lassen sich ganz einfach zu dem <xref:System.Windows.Forms.BindingNavigator>-Steuerelement hinzufügen, da es ein <xref:System.Windows.Forms.ToolStrip>-Steuerelement ist.  Siehe auch [Vorgehensweise: Hinzufügen der Schaltflächen für das Laden, Speichern und Abbrechen zum BindingNavigator-Steuerelement in Windows Forms](https://msdn.microsoft.com/library/safa4957\(v=vs.110\)).  
  
 Für jede Schaltfläche im <xref:System.Windows.Forms.BindingNavigator>-Steuerelement gibt es einen entsprechenden Member der <xref:System.Windows.Forms.BindingSource>-Komponente, die dieselbe Funktionalität programmgesteuert bereitstellt. Beispielsweise entspricht die <xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A>-Schaltfläche der <xref:System.Windows.Forms.BindingSource.MoveFirst%2A>-Methode der <xref:System.Windows.Forms.BindingSource>-Komponente, die <xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A>-Schaltfläche der <xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A>-Methode usw. Demzufolge ist das Aktivieren des <xref:System.Windows.Forms.BindingNavigator>-Steuerelements für die Navigation zwischen Datensätzen ebenso einfach wie das Festlegen seiner <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A>-Eigenschaft auf die entsprechende <xref:System.Windows.Forms.BindingSource>-Komponente auf dem Formular.  
  
### <a name="to-set-up-the-bindingnavigator-control"></a>So richten Sie das BindingNavigator-Steuerelement ein  
  
1.  Fügen Sie eine <xref:System.Windows.Forms.BindingSource>-Komponente namens `bindingSource1` und zwei <xref:System.Windows.Forms.TextBox>-Steuerelemente namens `textBox1` und `textBox2` hinzu.  
  
2.  Binden Sie `bindingSource1` an Daten und die TextBox-Steuerelemente an `bindingSource1`. Fügen Sie zu diesem Zweck den folgenden Code in Ihr Formular ein, und rufen Sie `LoadData` aus dem Konstruktor des Formulars oder der <xref:System.Windows.Forms.Form.Load>-Ereignisbehandlungsmethode heraus auf.  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#2)]  
  
3.  Fügen Sie Ihrem Formular ein <xref:System.Windows.Forms.BindingNavigator>-Steuerelement namens `bindingNavigator1` hinzu.  
  
4.  Legen Sie die <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A>-Eigenschaft für `bindingNavigator1` auf `bindingSource1` fest. Dies ist mit dem Designer oder im Code möglich.  
  
     [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#3)]  
  
## <a name="example"></a>Beispiel  
 Das folgende Codebeispiel ist das vollständige Beispiel für die zuvor aufgeführten Schritte.  
  
 [!code-csharp[System.Windows.Forms.BindingNavigatorNavigate#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingNavigatorNavigate#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingNavigatorNavigate/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
 Für dieses Beispiel benötigen Sie Folgendes:  
  
-   Verweise auf die Assemblys "System", "System.Data", "System.Drawing", "System.Windows.Forms" und "System.Xml".  
  
 Informationen zum Erstellen dieses Beispiels über die Befehlszeile für Visual Basic oder Visual c# finden Sie unter [erstellen über die Befehlszeile](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md) oder [Befehlszeile mit csc.exe](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md). Sie können auch in diesem Beispiel in Visual Studio erstellen, indem Sie den Code in ein neues Projekt einfügen.  Siehe auch: [Vorgehensweise Kompilieren und Ausführen eines vollständigen Windows Forms-Codebeispiels mit Visual Studio](https://msdn.microsoft.com/library/Bb129228\(v=vs.110\)).  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.BindingNavigator>  
 [BindingNavigator-Steuerelement](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)  
 [ToolStrip-Steuerelement](../../../../docs/framework/winforms/controls/toolstrip-control-windows-forms.md)
