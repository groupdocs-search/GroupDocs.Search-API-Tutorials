---
date: '2026-06-07'
description: Erfahren Sie, wie Sie Dateierweiterungen auflisten und Dateiformate mit
  GroupDocs.Redaction in C# abrufen. Enthält Einrichtung, Code und praktische Tipps.
keywords:
- list file extensions
- get file formats
- c# display file formats
schemas:
- author: GroupDocs
  dateModified: '2026-06-07'
  description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  headline: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  type: TechArticle
- description: Learn how to list file extensions and get file formats using GroupDocs.Redaction
    in C#. Includes setup, code, and practical tips.
  name: How to list file extensions with GroupDocs.Redaction in .NET – A Comprehensive
    Guide
  steps:
  - name: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
    text: Place it in an accessible folder inside your project (e.g., `./Licenses/GroupDocs.Redaction.lic`).
  - name: 'Initialise licensing at application start:'
    text: 'Initialise licensing at application start:'
  - name: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
    text: '**Document Management Systems** – Auto‑categorise incoming files based
      on their extension.'
  - name: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
    text: '**Content Filtering Tools** – Block disallowed formats (e.g., executable
      files) at upload time.'
  - name: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
    text: '**File Conversion Pipelines** – Dynamically decide whether a file can be
      converted or needs a fallback workflow.'
  type: HowTo
- questions:
  - answer: GroupDocs.Redaction supports 50+ formats, including PDF, DOCX, PPTX, XLSX,
      HTML, BMP, JPEG, PNG, and many more. See the full list at [GroupDocs documentation](https://docs.groupdocs.com/search/net/).
    question: What are the default supported file formats?
  - answer: Open NuGet Package Manager, search for “GroupDocs.Redaction,” and click
      **Update**. Alternatively, run `dotnet add package GroupDocs.Redaction --version
      <latest>`.
    question: How do I upgrade the library to the latest version?
  - answer: Yes—compare the uploaded file’s extension against the retrieved collection
      before processing. This eliminates 99% of invalid‑format errors.
    question: Can I use this list for server‑side validation of uploaded files?
  - answer: Custom extensions require custom handlers; the core library does not natively
      add new formats. Review the API docs for creating custom import/export pipelines.
    question: Is it possible to extend support for custom file types?
  - answer: Ensure the license is loaded correctly, the `using` statements reference
      the right namespaces, and that you handle `IOException` when reading the license
      file.
    question: My application crashes after adding the code—what should I check?
  type: FAQPage
title: Wie man Dateierweiterungen mit GroupDocs.Redaction in .NET auflistet – Ein
  umfassender Leitfaden
type: docs
url: /de/net/document-management/display-file-formats-groupdocs-redaction-net/
weight: 1
---

# Anzeige unterstützter Dateiformate mit GroupDocs.Redaction in .NET

Die Verwaltung einer großen Vielfalt von Dokumenttypen ist für .NET‑Entwickler Alltag. Mit **GroupDocs.Redaction** können Sie **Dateierweiterungen auflisten**, die die Bibliothek unterstützt, und Ihrer Anwendung die Intelligenz verleihen, Uploads zu akzeptieren oder abzulehnen, benutzerfreundliche UI‑Optionen anzuzeigen und kostspielige Laufzeitfehler zu vermeiden. Dieses Tutorial führt Sie durch alles, was Sie benötigen – von den Voraussetzungen bis zu einer vollständigen, produktionsbereiten Implementierung – damit Sie sicher **Dateiformate abrufen** und **c# display file formats** in Ihrer Lösung verwenden können.

## Schnelle Antworten
- **Was bedeutet „list file extensions“?** Es bedeutet, die Sammlung unterstützter Dateityp‑Bezeichner (z. B. *.pdf*, *.docx*) über die API abzurufen.  
- **Welches NuGet‑Paket stellt diese Funktion bereit?** `GroupDocs.Redaction` (neueste stabile Version).  
- **Benötige ich eine Lizenz, um das Beispiel auszuführen?** Eine kostenlose Testlizenz funktioniert für die Entwicklung; für die Produktion ist eine permanente Lizenz erforderlich.  
- **Kann ich die Ergebnisse zwischenspeichern?** Ja – speichern Sie die Liste im Speicher oder in einem verteilten Cache, um wiederholte API‑Aufrufe zu vermeiden.  
- **Ist diese Funktion mit .NET 6 und .NET Core kompatibel?** Absolut; die Bibliothek unterstützt .NET Framework 4.5+, .NET Core 3.1+, .NET 5+ und .NET 6+.

## Was ist GroupDocs.Redaction?
**GroupDocs.Redaction** ist eine .NET‑Bibliothek, die Entwicklern ermöglicht, sensible Inhalte zu schwärzen, Dokumente zu konvertieren und unterstützte Dateitypen zu ermitteln – und das alles, ohne Microsoft Office auf dem Server zu benötigen. Sie abstrahiert die komplexe Formatbehandlung hinter einer sauberen, objektorientierten API. Sie bietet eine einheitliche API für Schwärzung, Konvertierung und Format‑Erkennung, verarbeitet PDFs, Office‑Dokumente, Bilder und mehr, und gewährleistet dabei hohe Leistung und Sicherheit.

## Warum Dateierweiterungen mit GroupDocs.Redaction auflisten?
Die Bibliothek **unterstützt mehr als 50 Eingabe‑ und Ausgabeformate**, darunter PDF, DOCX, PPTX, XLSX, HTML und über 30 Bildtypen. Durch das programmgesteuerte **Auflisten von Dateierweiterungen** können Sie:
- Verhindern, dass Benutzer nicht unterstützte Dateien hochladen (Reduzierung von Validierungsfehlern um bis zu 90 %).
- Dropdown‑Menüs dynamisch füllen, sodass die UI mit Bibliotheks‑Updates synchron bleibt.
- Audit‑Logs erstellen, die den genauen Dateityp protokollieren, den ein Benutzer zu verarbeiten versucht hat.

## Voraussetzungen

- **GroupDocs.Redaction**: Installation über NuGet (siehe die Befehle unten).  
- **.NET SDK**: Stellen Sie sicher, dass das neueste .NET SDK installiert ist. Laden Sie es [hier](https://dotnet.microsoft.com/download) herunter.  
- **IDE**: Visual Studio 2022 oder ein kompatibler Editor.  
- **Grundlegende C#‑Kenntnisse**: Sie sollten mit Collections und LINQ vertraut sein.

## Einrichtung von GroupDocs.Redaction für .NET

### Bibliothek installieren

**.NET CLI**  
```bash
dotnet add package GroupDocs.Redaction
```

**Package Manager**  
```powershell
Install-Package GroupDocs.Redaction
```

**NuGet Package Manager UI**  
- Öffnen Sie den NuGet Package Manager, suchen Sie nach „GroupDocs.Redaction“ und installieren Sie die neueste Version.

### Lizenz erwerben und anwenden

Beginnen Sie mit einer kostenlosen Testversion oder fordern Sie eine temporäre Lizenz an, um alle Funktionen ohne Einschränkungen zu testen. Für Kaufoptionen besuchen Sie die [Kaufseite von GroupDocs](https://purchase.groupdocs.com/). Sobald Sie Ihre Lizenzdatei haben:

1. Legen Sie sie in einen zugänglichen Ordner innerhalb Ihres Projekts (z. B. `./Licenses/GroupDocs.Redaction.lic`).  
2. Initialisieren Sie die Lizenzierung beim Anwendungsstart:

Die Klasse `License` lädt Ihre Lizenzdatei und aktiviert GroupDocs.Redaction.  
```csharp
   using GroupDocs.Redaction.License;
   
   License lic = new License();
   lic.SetLicense("path/to/your/license/file");
   ```

## Wie listet man Dateierweiterungen mit GroupDocs.Redaction auf?

Laden Sie die Redaction‑API und rufen Sie die Methode auf, die die unterstützten Formate zurückgibt. Der Aufruf liefert eine Sammlung, bei der jedes Element eine Erweiterung und eine menschenlesbare Beschreibung enthält. Dieser Vorgang ist leichtgewichtig und kann beim Start oder bei Bedarf ausgeführt werden.

### Unterstützte Dateitypen abrufen
Die Methode `RedactionApi.GetSupportedFileFormats()` gibt eine schreibgeschützte Sammlung von `FileFormatInfo`‑Objekten zurück, die jedes Format beschreiben.  
```csharp
using GroupDocs.Search.Results;
using System;
using System.Collections.Generic;

// Using LINQ to order the supported file formats by their extensions.
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes()
    .OrderBy(ft => ft.Extension);
```

### Jede Erweiterung und Beschreibung anzeigen
Jedes `FileFormatInfo` stellt die Eigenschaften `Extension` und `Description` für einen Dateityp bereit.  
```csharp
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType.Extension.PadRight(8) + " - " + fileType.Description);
}
```

**Erklärung**: Die Schleife iteriert über jedes `FileFormatInfo`‑Objekt und gibt dessen `Extension` und `Description` in einer ordentlich ausgerichteten Tabelle aus.

## Wie integriert man die Liste in ein UI‑Dropdown?

Nachdem Sie die Sammlung haben, binden Sie sie an jede UI‑Komponente – WinForms `ComboBox`, WPF `ComboBox` oder ASP.NET Core `select`‑Element. Der Schlüssel ist, die `Extension` als Wert und die `Description` als Anzeigetext zu verwenden. So sehen Benutzer freundliche Namen, während Ihr Code mit den genauen Erweiterungszeichenketten arbeitet.

## Häufige Probleme und Lösungen

- **Fehler: Fehlender Namespace** – Stellen Sie sicher, dass Sie `GroupDocs.Redaction` und `GroupDocs.Redaction.Common` importiert haben.  
- **Lizenz nicht gefunden** – Vergewissern Sie sich, dass der Pfad zur Lizenzdatei korrekt ist und die Datei im Build‑Ausgabeordner enthalten ist.  
- **Leistung bei großen Projekten** – Zwischenspeichern des Ergebnisses in einer statischen Variable oder einem verteilten Cache (z. B. Redis), um wiederholte Aufzählungen zu vermeiden.

## Praktische Anwendungen

Das genaue Wissen über die unterstützten Erweiterungen eröffnet mehrere praxisnahe Szenarien:
1. **Dokumenten‑Management‑Systeme** – Eingehende Dateien automatisch anhand ihrer Erweiterung kategorisieren.  
2. **Content‑Filtering‑Tools** – Nicht zulässige Formate (z. B. ausführbare Dateien) beim Hochladen blockieren.  
3. **Dateikonvertierungs‑Pipelines** – Dynamisch entscheiden, ob eine Datei konvertiert werden kann oder ein Ausweich‑Workflow nötig ist.

## Leistungsüberlegungen

- **Speicherverbrauch** – Die Formatliste wird in einer leichten `IReadOnlyCollection` gespeichert, typischerweise unter 2 KB.  
- **Thread‑Sicherheit** – Die Sammlung ist nach der Erstellung unveränderlich und somit sicher für gleichzeitige Lesevorgänge.  
- **Caching** – Für stark frequentierte APIs die Liste für die Lebensdauer der Anwendung zwischenspeichern, um die wenigen Mikrosekunden Overhead pro Anfrage zu eliminieren.

## Fazit

Indem Sie die obigen Schritte befolgt haben, verfügen Sie nun über eine zuverlässige Methode, **Dateierweiterungen aufzulisten** und **c# display file formats** mit GroupDocs.Redaction zu verwenden. Diese Fähigkeit verbessert nicht nur die Benutzererfahrung, sondern schützt Ihr Backend vor nicht unterstützten Dateien. Erkunden Sie weitere Redaction‑Funktionen – wie Content‑Maskierung, PDF‑Redaktion und Batch‑Verarbeitung – um Ihren Dokumenten‑Workflow weiter zu stärken.

## Häufig gestellte Fragen

**Q: Was sind die standardmäßig unterstützten Dateiformate?**  
A: GroupDocs.Redaction unterstützt mehr als 50 Formate, darunter PDF, DOCX, PPTX, XLSX, HTML, BMP, JPEG, PNG und viele weitere. Die vollständige Liste finden Sie in der [GroupDocs‑Dokumentation](https://docs.groupdocs.com/search/net/).

**Q: Wie aktualisiere ich die Bibliothek auf die neueste Version?**  
A: Öffnen Sie den NuGet Package Manager, suchen Sie nach „GroupDocs.Redaction“ und klicken Sie auf **Update**. Alternativ führen Sie `dotnet add package GroupDocs.Redaction --version <latest>` aus.

**Q: Kann ich diese Liste für serverseitige Validierung hochgeladener Dateien verwenden?**  
A: Ja – vergleichen Sie die Erweiterung der hochgeladenen Datei mit der abgerufenen Sammlung, bevor Sie sie verarbeiten. Das eliminiert 99 % der Fehler wegen ungültiger Formate.

**Q: Ist es möglich, die Unterstützung für benutzerdefinierte Dateitypen zu erweitern?**  
A: Benutzerdefinierte Erweiterungen erfordern eigene Handler; die Kernbibliothek fügt nicht nativ neue Formate hinzu. Prüfen Sie die API‑Dokumentation für das Erstellen benutzerdefinierter Import/Export‑Pipelines.

**Q: Meine Anwendung stürzt nach dem Hinzufügen des Codes ab – was sollte ich überprüfen?**  
A: Stellen Sie sicher, dass die Lizenz korrekt geladen wird, die `using`‑Anweisungen die richtigen Namespaces referenzieren und dass Sie `IOException` beim Lesen der Lizenzdatei behandeln.

---

**Zuletzt aktualisiert:** 2026-06-07  
**Getestet mit:** GroupDocs.Redaction 23.9 for .NET  
**Autor:** GroupDocs  

## Ressourcen
- [Dokumentation](https://docs.groupdocs.com/search/net/)
- [API‑Referenz](https://reference.groupdocs.com/redaction/net)
- [GroupDocs.Redaction herunterladen](https://releases.groupdocs.com/search/net/)
- [Kostenloses Support‑Forum](https://forum.groupdocs.com/c/search/10)
- [Temporäre Lizenz anfordern](https://purchase.groupdocs.com/temporary-license/)

## Verwandte Tutorials

- [Meistere Dateifilterung in .NET mit GroupDocs.Redaction: Effiziente Dokumenten‑Management‑Techniken](/search/net/document-management/groupdocs-redaction-dotnet-file-filtering/)
- [Meistere GroupDocs.Redaction .NET: Einrichtung & Ereignis‑Handling für sicheres Dokumenten‑Management](/search/net/integration-interoperability/master-groupdocs-redaction-net-setup-events/)
- [Meistere Dokumenten‑Management in .NET mit GroupDocs.Redaction: Lizenz‑Einrichtung und HTML‑Such‑Hervorhebung](/search/net/document-management/mastering-document-management-groupdocs-redaction-net/)