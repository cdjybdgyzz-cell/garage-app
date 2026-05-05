# Garage App → iOS App (TestFlight) Anleitung

## Voraussetzungen
- Mac mit macOS
- Xcode (aus dem App Store installieren)
- Apple Developer Account ($99/Jahr) - https://developer.apple.com
- GitHub Repo bereits erstellt

---

## Schritt 1: Xcode Projekt erstellen

1. **Xcode öffnen** → "Create New Project"
2. Wähle **iOS** → **App** → Weiter
3. Eingaben:
   - **Product Name:** `Garage`
   - **Team:** Dein Apple Developer Account auswählen
   - **Organization Identifier:** `com.deinname.garage` (z.B. `com.secundaria.garage`)
   - **Interface:** Storyboard
   - **Language:** Swift
4. Speichern unter einem Ordner (z.B. `~/Documents/Garage-iOS`)

---

## Schritt 2: WebView einrichten

### 2.1 WKWebView importieren
Öffne `ViewController.swift` und ersetze den Inhalt:

```swift
import UIKit
import WebKit

class ViewController: UIViewController, WKNavigationDelegate {
    
    var webView: WKWebView!
    
    override func loadView() {
        webView = WKWebView()
        webView.navigationDelegate = self
        view = webView
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        // GitHub Pages URL (wird in Schritt 4 aktiviert)
        let url = URL(string: "https://cdjybdgyzz-cell.github.io/garage-app/")!
        webView.load(URLRequest(url: url))
        webView.allowsBackForwardNavigationGestures = true
    }
    
    // Offline-Fallback: Lade lokale Dateien
    override func viewDidAppear(_ animated: Bool) {
        if let localURL = Bundle.main.url(forResource: "index", withExtension: "html") {
            webView.loadFileURL(localURL, allowingReadAccessTo: localURL.deletingLastPathComponent())
        }
    }
}
```

### 2.2 Lokale Dateien hinzufügen (Optional - für Offline-Nutzung)
1. Ziehe `index.html` in dein Xcode Projekt (unter "Garage" Ordner)
2. Aktiviere **"Copy items if needed"**
3. Aktiviere **"Add to target: Garage"**

---

## Schritt 3: App konfigurieren

### 3.1 Info.plist anpassen
Öffne `Info.plist` und füge hinzu:

| Key | Value |
|-----|-------|
| `Bundle display name` | Garage |
| `App Transport Security Settings` → `Allow Arbitrary Loads` | YES (für lokale HTML-Dateien) |

### 3.2 App-Icons hinzufügen
1. Öffne `Assets.xcassets` → `AppIcon`
2. Ziehe Icon-Bilder für alle Grössen hinein (1024x1024 für App Store)
3. Generator: https://appicon.co (lädt alle Grössen automatisch)

### 3.3 Bundle Identifier prüfen
- Targets → Garage → **Bundle Identifier:** `com.deinname.garage`
- **Version:** 1.0
- **Build:** 1

---

## Schritt 4: GitHub Pages aktivieren (für Online-Version)

1. Gehe zu: https://github.com/cdjybdgyzz-cell/garage-app/settings/pages
2. **Source:** `Deploy from a branch`
3. **Branch:** `main` / `/root`
4. Klicke **Save**
5. Warte ca. 2-5 Minuten
6. Deine App ist dann unter `https://cdjybdgyzz-cell.github.io/garage-app/` erreichbar

---

## Schritt 5: App in den App Store hochladen

### 5.1 Signierung einrichten
1. Xcode → **Settings** (Cmd+,) → **Accounts**
2. **+** → **Apple ID** → Login mit Developer Account
3. Targets → Garage → **Signing & Capabilities**
   - **Team:** Dein Account
   - **Bundle Identifier:** (muss unique sein)
   - **Automatically manage signing:** ✅

### 5.2 Archive erstellen
1. **Gerät auswählen:** `Any iOS Device (arm64)`
2. Menü: **Product** → **Archive**
3. Warte bis der Prozess fertig ist (kann 5-10 Min dauern)

### 5.3 Upload to App Store
1. Im **Organizer** Fenster: **Distribute App**
2. Wähle: **App Store Connect**
3. **Upload** → Weiter
4. **Automatically manage signing** → Weiter
5. **Upload** (dauert einige Minuten)

---

## Schritt 6: TestFlight einrichten

1. Gehe zu: https://appstoreconnect.apple.com
2. **My Apps** → **Garage**
3. **TestFlight** Tab
4. App wird nach Upload geprüft (dauert 1-24 Stunden)
5. Sobald "Ready to Submit" erscheint:
   - Klicke **"Internal Testing"**
   - **+ Testers** → E-Mail-Adressen hinzufügen
   - **Start Testing**

### Tester erhalten E-Mail:
- Öffnen den Link auf iOS-Gerät
- Installieren **TestFlight App** (aus App Store)
- Installieren **Garage** via TestFlight

---

## Wichtige Hinweise

### App Store Richtlinien
- Web-Apps nur mit WKWebView können abgelehnt werden ("Minimum Functionality")
- Lösung: Native Features hinzufügen (Push Notifications, File Upload, etc.)

### Kosten
- Apple Developer: **$99/Jahr** (zwingend für TestFlight)
- GitHub Pages: **Kostenlos**

### Offline-Nutzung
Wenn du `index.html` in Xcode einbindest, funktioniert die App auch offline (localStorage funktioniert in WKWebView).

---

## Schnell-Checkliste

- [ ] Xcode installiert
- [ ] Apple Developer Account aktiv ($99)
- [ ] Xcode Projekt erstellt
- [ ] WKWebView Code eingefügt
- [ ] App Icons hinzugefügt
- [ ] Signierung eingerichtet
- [ ] Archive erstellt
- [ ] Upload erfolgreich
- [ ] App Store Connect: App angelegt
- [ ] TestFlight: Tester hinzugefügt

---

## Troubleshooting

**"No signing certificate found"**
→ Xcode → Settings → Accounts → Download Manual Profiles

**"Bundle identifier not available"**
→ Ändere Bundle ID (z.B. `com.deinname.garage2`)

**App wird abgelehnt**
→ Füge native Features hinzu (z.B. Camera Access, Push Notifications)
