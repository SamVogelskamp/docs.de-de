---
title: Elementvorgänge (C#)
ms.date: 10/03/2018
ms.assetid: 283206c9-3246-4c48-b01a-d9de409a7231
ms.openlocfilehash: dbae8c0b3d98fe9674fbbeb432c1e42763e81026
ms.sourcegitcommit: 586dbdcaef9767642436b1e4efbe88fb15473d6f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/06/2018
ms.locfileid: "48836776"
---
# <a name="element-operations-c"></a>Elementvorgänge (C#)

Bei Elementvorgängen werden einzelne, spezifische Elemente aus einer Sequenz zurückgegeben.  
  
 Die Methoden des Standardabfrageoperators, die Elementvorgänge ausführen, sind im folgenden Abschnitt aufgeführt.  
  
## <a name="methods"></a>Methoden  
  
|Methodenname|Beschreibung |C#-Abfrageausdruckssyntax|Weitere Informationen|  
|-----------------|-----------------|---------------------------------|----------------------|  
|ElementAt|Gibt das Element an einen angegebenen Index in einer Auflistung zurück.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ElementAt%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAt%2A?displayProperty=nameWithType>|  
|ElementAtOrDefault|Gibt das Element an einen angegebenen Index in einer Auflistung oder einen Standardwert zurück, wenn der Index außerhalb des gültigen Bereichs liegt.|Nicht zutreffend.|<xref:System.Linq.Enumerable.ElementAtOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.ElementAtOrDefault%2A?displayProperty=nameWithType>|  
|First|Gibt das erste Element einer Auflistung oder das erste Element, das eine Bedingung erfüllt, zurück.|Nicht zutreffend.|<xref:System.Linq.Enumerable.First%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.First%2A?displayProperty=nameWithType>|  
|FirstOrDefault|Gibt das erste Element einer Auflistung oder das erste Element, das eine Bedingung erfüllt, zurück. Gibt einen Standardwert zurück, wenn kein solches Element vorhanden ist.|Nicht zutreffend.|<xref:System.Linq.Enumerable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.FirstOrDefault%60%601%28System.Linq.IQueryable%7B%60%600%7D%29?displayProperty=nameWithType>|  
|Letzter|Gibt das letzte Element einer Auflistung oder das letzte Element, das eine Bedingung erfüllt, zurück.|Nicht zutreffend.|<xref:System.Linq.Enumerable.Last%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Last%2A?displayProperty=nameWithType>|  
|LastOrDefault|Gibt das letzte Element einer Auflistung oder das letzte Element, das eine Bedingung erfüllt, zurück. Gibt einen Standardwert zurück, wenn kein solches Element vorhanden ist.|Nicht zutreffend.|<xref:System.Linq.Enumerable.LastOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.LastOrDefault%2A?displayProperty=nameWithType>|  
|Single|Gibt das einzige Element einer Auflistung oder das einzige Element, das eine Bedingung erfüllt, zurück. Löst eine <xref:System.InvalidOperationException> aus, wenn kein oder mehr als ein Element für die Rückgabe vorhanden ist. |Nicht zutreffend.|<xref:System.Linq.Enumerable.Single%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.Single%2A?displayProperty=nameWithType>|  
|SingleOrDefault|Gibt das einzige Element einer Auflistung oder das einzige Element, das eine Bedingung erfüllt, zurück. Gibt einen Standardwert zurück, wenn kein Element zurückgegeben werden kann. Löst eine <xref:System.InvalidOperationException> aus, wenn mehr als ein Element für die Rückgabe vorhanden ist. |Nicht zutreffend.|<xref:System.Linq.Enumerable.SingleOrDefault%2A?displayProperty=nameWithType><br /><br /> <xref:System.Linq.Queryable.SingleOrDefault%2A?displayProperty=nameWithType>|  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Linq>  
- [Standard Query Operators Overview (C#) (Übersicht der Standardabfrageoperatoren (C#))](../../../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)  
- [How to: Query for the Largest File or Files in a Directory Tree (LINQ) (C#) (Vorgehensweise: Abfragen der größten Datei oder der größten Dateien in einer Verzeichnisstruktur (LINQ) (C#))](../../../../csharp/programming-guide/concepts/linq/how-to-query-for-the-largest-file-or-files-in-a-directory-tree-linq.md)
