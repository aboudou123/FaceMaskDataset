**wie man eine neue Datei mit `vim` erstellst und bearbeitet**, Schritt für Schritt:

---

Sehr gerne! Ich entwerfe ein **klar strukturiertes Android-Projektkonzept**, das genau auf dein Thema passt:

---

# 📱 **Android-Projekt: Sicherer Prototyp mit Biometrie, TLS und SQL-Injection-Schutz**

---

## 🎯 **Zielsetzung**

Entwicklung eines Android-Prototyps, der:
✅ eine biometrische Authentifizierung (Fingerprint/Face) zur Anmeldung nutzt
✅ ausschließlich über TLS (HTTPS) mit einem Backend kommuniziert
✅ lokal SQLite-Daten speichert, geschützt vor SQL-Injections

---

## 🛠 **Technologien / Frameworks**

| Komponente         | Technologie                                  |
| ------------------ | -------------------------------------------- |
| Programmiersprache | Kotlin (oder Java)                           |
| Biometrie          | AndroidX Biometric Library                   |
| Netzwerk           | Retrofit + OkHttp mit TLS-Only-Konfiguration |
| Datenbank          | Room ORM (als Schutz gegen SQL-Injection)    |
| UI                 | Jetpack Compose oder klassische XML          |
| Weitere Sicherheit | Network Security Config, ProGuard            |

---

## 🗂 **Projektstruktur (Vorschlag)**

```
/app
 ├── /src
 │    ├── /main
 │    │    ├── /java/com/example/secureapp
 │    │    │     ├── MainActivity.kt
 │    │    │     ├── auth/BiometricHelper.kt
 │    │    │     ├── network/ApiClient.kt
 │    │    │     ├── network/ApiService.kt
 │    │    │     ├── data/AppDatabase.kt
 │    │    │     ├── data/UserDao.kt
 │    │    │     ├── data/UserEntity.kt
 │    │    │     └── ui/LoginScreen.kt
 │    │    ├── /res/layout
 │    │    └── /res/values
 └── /network_security_config.xml
```

---

## 🔒 **Sicherheitsfeatures im Detail**

### 1️⃣ **Biometrie-Authentifizierung**

* Verwende die `BiometricPrompt` API (über AndroidX Biometric Library).
* Fallback: PIN / Passwort.
* Beispiel:

```kotlin
BiometricPrompt.PromptInfo.Builder()
   .setTitle("Login via Biometrie")
   .setNegativeButtonText("Abbrechen")
   .build()
```

---

### 2️⃣ **TLS-Only Kommunikation**

* **OkHttp / Retrofit:**

  * TLS erzwingen: nutze `https://` Endpunkte.
  * Zertifikat-Pinning optional (für noch höhere Sicherheit).
* **Network Security Config:**

  * Definiere `network_security_config.xml`:

```xml
<network-security-config>
    <base-config cleartextTrafficPermitted="false" />
</network-security-config>
```

* Stelle sicher: Kein HTTP-Zugriff erlaubt.

---

### 3️⃣ **SQL-Injection-Schutz**

* Nutze `Room ORM`.
* Alle Queries parameterisiert (Room erzwingt das).
* Beispiel:

```kotlin
@Query("SELECT * FROM user WHERE username = :username LIMIT 1")
fun getUserByUsername(username: String): UserEntity?
```

* Kein dynamisches SQL-String-Building!

---

## 📌 **Funktionale Features**

✅ Login-Screen mit Biometrie
✅ Synchronisation der Daten über TLS (Dummy REST API)
✅ Speicherung einfacher User-Daten lokal in SQLite (über Room)
✅ Einfache Datenanzeige im UI

---

## 📝 **Projektumfang (MVP)**

| Feature                                         | Status   |
| ----------------------------------------------- | -------- |
| Biometrisches Login                             | Pflicht  |
| TLS-gesicherte API-Kommunikation (Dummy-Server) | Pflicht  |
| SQL-Injection-sichere lokale Speicherung        | Pflicht  |
| Einfacher Screen zur Anzeige der Userdaten      | Optional |
| Zertifikat-Pinning                              | Optional |
| Backend-Mock (z. B. über Postman/Mockoon)       | Optional |

---

## 🚀 **Mini-Roadmap**

1️⃣ Grundgerüst App (UI + Navigation)
2️⃣ Biometrie-Login implementieren
3️⃣ Room-Datenbank + sichere Queries
4️⃣ Retrofit/OkHttp mit TLS konfigurieren
5️⃣ API-Calls + Daten persistieren
6️⃣ Testen: manuelle und automatisierte Tests

---

## 📂 **Zusatz: Beispiel Network Security Config**

```xml
<network-security-config>
    <base-config cleartextTrafficPermitted="false">
        <trust-anchors>
            <certificates src="system" />
        </trust-anchors>
    </base-config>
</network-security-config>
```

---

## 💡 **Besonderheiten**

👉 Alle sicherheitsrelevanten Teile sind dokumentiert im Code (z. B. warum TLS-only, warum Room).
👉 Code und Architektur lassen sich leicht auf Produktionsniveau erweitern (z. B. JWT-Token-Handling).

---

Wenn du willst, kann ich:
✅ einen **Beispiel-Code (Startprojekt)** generieren
✅ einen **BPMN-Flow des Prozesses** entwerfen
✅ ein **Mock-Backend-Schema** bereitstellen

Möchtest du das? Oder soll ich ein fertiges Beispiel-Repo-Setup schreiben? 😊
