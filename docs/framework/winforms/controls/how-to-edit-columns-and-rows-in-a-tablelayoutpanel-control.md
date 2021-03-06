---
title: 'Gewusst wie: Bearbeiten von Zeilen und Spalten in einem TableLayoutPanel-Steuerelement'
ms.date: 03/30/2017
f1_keywords:
- net.ComponentModel.StyleCollectionEditor
helpviewer_keywords:
- columns [Windows Forms], editing
- TableLayoutPanel control [Windows Forms], editing
- rows [Windows Forms], editing
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
ms.openlocfilehash: 820d2f98290650bfaf377bd2d4b863dfb2e6e704
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43500783"
---
# <a name="how-to-edit-columns-and-rows-in-a-tablelayoutpanel-control"></a>Gewusst wie: Bearbeiten von Zeilen und Spalten in einem TableLayoutPanel-Steuerelement
Können Sie den auflistungs-Editor, der die <xref:System.Windows.Forms.TableLayoutPanel> Steuerelement mit der Bezeichnung der **Spalten- und Zeilenstile** Dialogfeld, um die Zeilen und Spalten der Steuerelemente zu bearbeiten.  
  
> [!NOTE]
>  Wenn Sie ein Steuerelement, die mehrere Zeilen oder Spalten umfassen soll, legen die `RowSpan` und `ColumnSpan` Eigenschaften des Steuerelements. Weitere Informationen finden Sie unter [Walkthrough: Arranging Controls on Windows Forms Using a TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md).  
>   
>  Wenn Sie ein Steuerelement in einer Zelle ausrichten möchten oder wenn Sie ein Steuerelement in einer Zelle ausdehnen möchten, Verwenden des Steuerelements <xref:System.Windows.Forms.Control.Anchor%2A> Eigenschaft. Weitere Informationen finden Sie unter [Walkthrough: Arranging Controls on Windows Forms Using a TableLayoutPanel](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md).  
>   
>  Je nach den aktiven Einstellungen oder der Version unterscheiden sich die Dialogfelder und Menübefehle auf Ihrem Bildschirm möglicherweise von den in der Hilfe beschriebenen. Klicken Sie im Menü **Extras** auf **Einstellungen importieren und exportieren** , um die Einstellungen zu ändern. Weitere Informationen finden Sie unter [Personalisieren von Visual Studio-IDE](/visualstudio/ide/personalizing-the-visual-studio-ide).  
  
### <a name="to-edit-rows-and-columns"></a>Bearbeiten von Zeilen und Spalten  
  
1.  Ziehen Sie eine <xref:System.Windows.Forms.TableLayoutPanel> -Steuerelement aus der **Toolbox** auf das Formular.  
  
2.  Klicken Sie auf die <xref:System.Windows.Forms.TableLayoutPanel> des Steuerelements Smarttag-Glyphe (![Smarttag-Glyphe](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.gif "VS_WinFormSmtTagGlyph")), und wählen Sie **Zeilen und Spalten bearbeiten** zum Öffnen der  **Spalten- und Zeilenstile** Dialogfeld. Sie können auch der rechten Maustaste auf die <xref:System.Windows.Forms.TableLayoutPanel> steuern, und wählen Sie **Zeilen und Spalten bearbeiten** aus dem Kontextmenü.  
  
3.  Wählen Sie zum Hinzufügen oder Entfernen von Spalten, **Spalten** aus der **Elementtyp** im Dropdown Listenfeld.  
  
4.  Wählen Sie zum Hinzufügen oder Entfernen von Zeilen, **Zeilen** aus der **Elementtyp** im Dropdown Listenfeld.  
  
5.  Klicken Sie auf die **hinzufügen** Schaltfläche, um das Ende einer Zeile oder Spalte hinzufügen der **Member** Liste.  
  
6.  Klicken Sie auf die **einfügen** , um eine Zeile oder Spalte, bevor Sie das aktuell ausgewählte Element in der Liste hinzuzufügen.  
  
7.  Wenn Sie eine Zeile oder Spalte hinzufügen, wählen Sie die **Größentyp** für die neue Zeile oder Spalte. Weitere Informationen finden Sie unter <xref:System.Windows.Forms.SizeType>.  
  
8.  Um eine Zeile oder Spalte zu entfernen, klicken Sie auf die **entfernen** Schaltfläche, um das aktuell ausgewählte Element im Löschen der **Member** Liste.  
  
## <a name="see-also"></a>Siehe auch  
 <xref:System.Windows.Forms.SizeType>  
 [TableLayoutPanel-Steuerelement](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)
