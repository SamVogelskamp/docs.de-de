---
title: Main-Prozedur in Visual Basic
ms.date: 07/20/2015
f1_keywords:
- vb.Main
helpviewer_keywords:
- Main procedure
- Main method [Visual Basic]
- main function
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
ms.openlocfilehash: 109bf94eb91292cfca700a9e456c8ab53e83d68f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
ms.locfileid: "33652151"
---
# <a name="main-procedure-in-visual-basic"></a>Main-Prozedur in Visual Basic
Alle Visual Basic-Anwendung muss eine Prozedur namens enthalten `Main`. Diese Prozedur dient, wie die Start- und gesamtsteuerung für Ihre Anwendung. Die .NET Framework Aufrufe der `Main` -Prozedur, wenn die Anwendung geladen hat und bereit für die Steuerung an sie übergeben wird. Wenn Sie eine Windows Forms-Anwendung erstellen, müssen Sie schreiben die `Main` Verfahren für Anwendungen, die auf ihre eigenen ausgeführt.  
  
 `Main` enthält den Code, der zuerst ausgeführt wird. In `Main`, Sie bestimmen, welche Form zuerst geladen werden, wenn das Programm gestartet wird, festzustellen, ob eine Kopie der Anwendung bereits auf dem System ausgeführt wird, richten Sie einen Satz von Variablen für die Anwendung oder öffnen Sie eine Datenbank, die die Anwendung erfordert.  
  
## <a name="requirements-for-the-main-procedure"></a>Anforderungen für die Main-Prozedur  
 Eine Datei, die einen eigenen (normalerweise mit der Erweiterung .exe) wird ausgeführt auf darf eine `Main` Prozedur. Eine Bibliothek (z. B. mit der Erweiterung .dll) wird nicht eigenständig ausgeführt und erfordert keine `Main` Prozedur. Die Anforderungen für die verschiedenen Typen von Projekten, die Sie erstellen können, lauten folgendermaßen:  
  
-   Konsolenanwendungen führen Sie auf ihre eigenen, und geben Sie an mindestens eine `Main` Prozedur. sein.  
  
-   Führen Sie auf ihren eigenen Windows Forms-Anwendungen. Visual Basic-Compiler automatisch generiert jedoch eine `Main` Prozedur z. B. eine Anwendung, und Sie müssen nicht schreiben.  
  
-   Klassenbibliotheken erfordern keine `Main` Prozedur. Dazu gehören Windows-Steuerelement-Bibliotheken und Websteuerelementbibliotheken. Webanwendungen werden als Klassenbibliotheken bereitgestellt.  
  
## <a name="declaring-the-main-procedure"></a>Deklarieren Sie die Main-Prozedur  
 Es gibt vier Möglichkeiten zum Deklarieren der `Main` Prozedur. Es kann Argumente annehmen, oder nicht, und sie können einen Wert zurückgeben, oder nicht.  
  
> [!NOTE]
>  Wenn Sie deklarieren `Main` in einer Klasse, verwenden Sie die `Shared` Schlüsselwort. In einem Modul `Main` muss nicht werden `Shared`.  
  
-   Die einfachste Möglichkeit ist das Deklarieren einer `Sub` Prozedur, die keine Argumente übernehmen oder einen Wert zurückgeben.  
  
    ```  
    Module mainModule  
        Sub Main()  
            MsgBox("The Main procedure is starting the application.")  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
-   `Main` kann auch Zurückgeben einer `Integer` -Wert, der das Betriebssystem als Exitcode für das Programm verwendet. Andere Programme können diesen Code mithilfe den Windows-ERRORLEVEL-Wert zu testen. Um einen Exitcode zurückzugeben, müssen Sie deklarieren `Main` als eine `Function` Prozedur anstelle von einer `Sub` Prozedur.  
  
    ```  
    Module mainModule  
        Function Main() As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   `Main` akzeptieren können auch eine `String` Array als Argument. Jede Zeichenfolge im Array enthält einen der Befehlszeilenargumente verwendet, um das Programm aufzurufen. Sie können unterschiedliche Aktionen abhängig von deren Werten ausführen.  
  
    ```  
    Module mainModule  
        Function Main(ByVal cmdArgs() As String) As Integer  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            ' On return, assign appropriate value to returnValue.  
            ' 0 usually means successful completion.  
            MsgBox("The application is terminating with error level " &  
                 CStr(returnValue) & ".")  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
-   Sie können deklarieren, `Main` , überprüfen Sie die Befehlszeilenargumente, jedoch wie folgt einen Exitcode zurückgibt.  
  
    ```  
    Module mainModule  
        Sub Main(ByVal cmdArgs() As String)  
            MsgBox("The Main procedure is starting the application.")  
            Dim returnValue As Integer = 0  
            ' See if there are any arguments.  
            If cmdArgs.Length > 0 Then  
                For argNum As Integer = 0 To UBound(cmdArgs, 1)  
                    ' Insert code to examine cmdArgs(argNum) and take  
                    ' appropriate action based on its value.  
                Next argNum  
            End If  
            ' Insert call to appropriate starting place in your code.  
            MsgBox("The application is terminating.")  
        End Sub  
    End Module  
    ```  
  
## <a name="see-also"></a>Siehe auch  
 <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
 <xref:System.Array.Length%2A>  
 <xref:Microsoft.VisualBasic.Information.UBound%2A>  
 [Struktur eines Visual Basic-Programms](../../../visual-basic/programming-guide/program-structure/structure-of-a-visual-basic-program.md)  
 [/main](../../../visual-basic/reference/command-line-compiler/main.md)  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)  
 [Sub-Anweisung](../../../visual-basic/language-reference/statements/sub-statement.md)  
 [Function-Anweisung](../../../visual-basic/language-reference/statements/function-statement.md)  
 [Integer-Datentyp](../../../visual-basic/language-reference/data-types/integer-data-type.md)  
 [String-Datentyp](../../../visual-basic/language-reference/data-types/string-data-type.md)
