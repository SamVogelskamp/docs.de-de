---
title: dotnet nuget delete-Befehl – .NET Core-CLI
description: Der dotnet-nuget-delete-Befehl löscht ein Paket vom Server oder hebt dessen Auflistung auf.
author: karann-msft
ms.author: mairaw
ms.date: 06/01/2018
ms.openlocfilehash: f4aa027a465c4adea1de13853063d03e8e295411
ms.sourcegitcommit: c93fd5139f9efcf6db514e3474301738a6d1d649
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/27/2018
ms.locfileid: "50180878"
---
# <a name="dotnet-nuget-delete"></a>dotnet nuget delete

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>name

`dotnet nuget delete` – Löscht ein Paket vom Server oder hebt dessen Auflistung auf.

## <a name="synopsis"></a>Übersicht

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--no-service-endpoint]
    [--non-interactive] [-s|--source]
dotnet nuget delete [-h|--help]
```
# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--non-interactive]
    [-s|--source]
dotnet nuget delete [-h|--help]
```
# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)
```
dotnet nuget delete [<PACKAGE_NAME> <PACKAGE_VERSION>] [--force-english-output] [-k|--api-key] [--non-interactive]
    [-s|--source]
dotnet nuget delete [-h|--help]
```
---

## <a name="description"></a>Beschreibung 

Der `dotnet nuget delete`-Befehl löscht ein Paket vom Server oder hebt dessen Auflistung auf. Für [nuget.org](https://www.nuget.org/) wird die Auflistung des Pakets aufgehoben.

## <a name="arguments"></a>Argumente

`PACKAGE_NAME`

Name/ID des zu löschenden Pakets.

`PACKAGE_VERSION`

Version des zu löschenden Pakets.

## <a name="options"></a>Optionen

# <a name="net-core-21tabnetcore21"></a>[.NET Core 2.1](#tab/netcore21)

`--force-english-output`

 Erzwingt die Ausführung der Anwendung mithilfe einer invarianten Kultur, die auf Englisch basiert.

`-h|--help`

Druckt eine kurze Hilfe für den Befehl.

`-k|--api-key <API_KEY>`

Der API-Schlüssel für den Server.

`--no-service-endpoint` fügt „api/v2/package“ nicht der Quell-URL an.fügen

`--non-interactive`

Fordert nicht zu Eingaben oder Bestätigungen des Benutzers auf.

`-s|--source <SOURCE>`

Gibt die Server-URL an. Unterstützte URLs für „nuget.org“ sind u.a. `https://www.nuget.org`, `https://www.nuget.org/api/v3` und `https://www.nuget.org/api/v2/package`. Ersetzen Sie für private Feeds den Hostnamen (z.B. `%hostname%/api/v3`).

# <a name="net-core-20tabnetcore20"></a>[.NET Core 2.0](#tab/netcore20)

`--force-english-output`

 Erzwingt die Ausführung der Anwendung mithilfe einer invarianten Kultur, die auf Englisch basiert.

`-h|--help`

Druckt eine kurze Hilfe für den Befehl.

`-k|--api-key <API_KEY>`

Der API-Schlüssel für den Server.

`--non-interactive`

Fordert nicht zu Eingaben oder Bestätigungen des Benutzers auf.

`-s|--source <SOURCE>`

Gibt die Server-URL an. Unterstützte URLs für „nuget.org“ sind u.a. `https://www.nuget.org`, `https://www.nuget.org/api/v3` und `https://www.nuget.org/api/v2/package`. Ersetzen Sie für private Feeds den Hostnamen (z.B. `%hostname%/api/v3`).

# <a name="net-core-1xtabnetcore1x"></a>[.NET Core 1.x](#tab/netcore1x)

`--force-english-output`

 Erzwingt die Ausführung der Anwendung mithilfe einer invarianten Kultur, die auf Englisch basiert.

`-h|--help`

Druckt eine kurze Hilfe für den Befehl.

`-k|--api-key <API_KEY>`

Der API-Schlüssel für den Server.

`--non-interactive`

Fordert nicht zu Eingaben oder Bestätigungen des Benutzers auf.

`-s|--source <SOURCE>`

Gibt die Server-URL an. Unterstützte URLs für „nuget.org“ sind u.a. `https://www.nuget.org`, `https://www.nuget.org/api/v3` und `https://www.nuget.org/api/v2/package`. Ersetzen Sie für private Feeds den Hostnamen (z.B. `%hostname%/api/v3`).

---

## <a name="examples"></a>Beispiele

Löscht Version 1.0 des Pakets `Microsoft.AspNetCore.Mvc`:

`dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0`

Löscht Version 1.0 des Pakets `Microsoft.AspNetCore.Mvc`, wobei der Benutzer nicht zur Eingabe von Anmeldeinformationen oder zu anderen Eingaben aufgefordert wird:

`dotnet nuget delete Microsoft.AspNetCore.Mvc 1.0 --non-interactive`
