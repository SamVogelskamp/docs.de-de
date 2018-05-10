### <a name="sslstream-supports-tls-alerts"></a>SslStream unterstützt TLS-Warnungen

|   |   |
|---|---|
|Details|Nach einem fehlgeschlagenen TLS-Handshake wird eine <xref:System.IO.IOException?displayProperty=name> mit einer inneren <xref:System.ComponentModel.Win32Exception?displayProperty=name> von dem ersten E/A-Lese-/Schreibvorgang ausgelöst. Der <xref:System.ComponentModel.Win32Exception.NativeErrorCode?displayProperty=name>-Code für die <xref:System.ComponentModel.Win32Exception?displayProperty=name> kann mithilfe dieser [Kanaldokumentation](https://msdn.microsoft.com/library/windows/desktop/dd721886%28v=vs.85%29.aspx) der TLS-Warnung des Remoteanbieters zugeordnet werden. Weitere Informationen finden Sie unter [RFC 2246: Abschnitt 7.2.2, Fehlerwarnungen](https://tools.ietf.org/html/rfc2246#section-7.2.2). <br/>Das Verhalten in .NET Framework 4.6.2 und früheren Versionen besteht darin, dass für den Transportkanal (in der Regel eine TCP-Verbindung) ein Timeout während des Schreib- oder Lesevorgangs auftritt, wenn beim Handshake bei der anderen Partei ein Fehler aufgetreten ist und die Verbindung unmittelbar danach zurückgewiesen wurde.|
|Vorschlag|Anwendungen, die Netzwerk-E/A-APIs aufrufen (z.B. <xref:System.IO.Stream.Read(System.Byte[],System.Int32,System.Int32)>/<xref:System.IO.Stream.Write(System.Byte[],System.Int32,System.Int32)>) sollten <xref:System.IO.IOException> oder <xref:System.TimeoutException?displayProperty=name> verarbeiten.<br/>Die TLS-Warnfunktion ist ab .NET Framework 4.7 standardmäßig aktiviert. Für Anwendungen für Versionen von .NET Framework von 4.0 bis 4.6.2, die auf einem System mit .NET Framework 4.7 oder höher ausgeführt werden, ist diese Funktion deaktiviert, um die Kompatibilität zu erhalten. <br/>Die folgende Konfigurations-API ist zum Aktivieren oder Deaktivieren des Features für .NET Framework 4.6- oder höhere Anwendungen, die unter .NET Framework 4.7 oder höher ausgeführt werden, verfügbar.<ul><li>Programmgesteuert:</li></ul>Die folgenden Methoden müssen unmittelbar nach dem Anwendungsstart aufgerufen werden, da ServicePointManager nur einmal initialisiert wird:<pre><code class="lang-csharp">AppContext.SetSwitch(&quot;TestSwitch.LocalAppContext.DisableCaching&quot;, true);&#13;&#10;AppContext.SetSwitch(&quot;Switch.System.Net.DontEnableTlsAlerts&quot;, true); // Set to &#39;false&#39; to enable the feature in .NET Framework 4.6 - 4.6.2.&#13;&#10;</code></pre><ul><li>AppConfig:</li></ul><pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Net.DontEnableTlsAlerts=true&quot;/&gt;&#13;&#10;&lt;!-- Set to &#39;false&#39; to enable the feature in .NET Framework 4.6 - 4.6.2. --&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre><ul><li>Registrierungsschlüssel (globaler Wert für einen Computer):</li></ul>Legen Sie den Wert auf <code>false</code> fest, um das Feature in .NET Framework 4.6 bis 4.6.2 zu aktivieren.<pre><code>Key = HKLM\SOFTWARE\[Wow6432Node\]Microsoft\.NETFramework\AppContext\Switch.System.Net.DontEnableTlsAlerts&#13;&#10;Type = String&#13;&#10;Value = &quot;true&quot;&#13;&#10;</code></pre>|
|Bereich|Microsoft Edge|
|Version|4.7|
|Typ|Neuzuweisung|
|Betroffene APIs|<ul><li><xref:System.Net.Security.SslStream?displayProperty=nameWithType></li><li><xref:System.Net.WebRequest?displayProperty=nameWithType></li><li><xref:System.Net.HttpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.FtpWebRequest?displayProperty=nameWithType></li><li><xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType></li><li><xref:System.Net.Http?displayProperty=nameWithType></li></ul>|
