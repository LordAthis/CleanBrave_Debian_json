# CleanBrave_Debian_json
Neonity által windows alá elkészített regisztry értékek linuxos átirata json beállítási fájlba

------------------------------------------------------
A FÁJL SZERKESZTÉS ÉS ELLENŐRZÉS ALATT!!! MÉG HIBÁKAT TARTALMAZHAT, KÖRÜLTEKINTŐEN ÉS KIZÁRÓLAG SAJÁT FELELŐSSÉGEDRE HASZNÁLD!
------------------------------------------------------



Így valósíthatod meg a beállításokat Debianon:


1. A szabály könyvtár létrehozása
A Brave Linux alatt az /etc/brave/policies/managed/ mappából olvassa be a konfigurációkat. Hozd létre ezt a mappát rendszergazdaként: 
bash
sudo mkdir -p /etc/brave/policies/managed/
Körültekintően használja a kódot.


2. A konfigurációs fájl elkészítése
Hozz létre egy új fájlt (pl. cleanbrave.json a fent jelzett mappában:

Például parancssorból
bash:
sudo nano /etc/brave/policies/managed/cleanbrave.json


3. A beállítások beillesztése
A Neonity-féle "CleanBrave" logikájának megfelelően az alábbi tartalmat illeszd a fájlba (ezek a leggyakoribb letiltandó elemek):
json
{
  "BraveRewardsDisabled": true,
  "BraveWalletDisabled": true,
  "BraveVPNDisabled": true,
  "IPFSDisabled": true,
  "TorDisabled": true
}

Mentés: Ctrl+O, majd Enter, kilépés: Ctrl+X.


4. Ellenőrzés
Indítsd újra a böngészőt, majd írd be a címsorba: brave://policy. Itt látnod kell a listában az általad megadott értékeket "OK" státusszal. 
Fontos megjegyzések:
Telepítési mód: Ha a Brave-et nem natív csomagként (deb), hanem Flatpak segítségével telepítetted, előfordulhat, hogy további jogosultságokat kell adnod a böngészőnek
az /etc/brave/ mappa olvasásához a Flatseal alkalmazással vagy parancssorból.
Alternatív hely: Néhány disztribúciónál (vagy régebbi verzióknál) a böngésző az /etc/chromium/policies/managed/ útvonalat is figyeli. 
 

-----------------------------------

Második változat:

-----------------------------------

Alkalmazás lépésről lépésre Debian alatt

1. Mappa létrehozása:
Nyiss egy terminált, és futtasd:
sudo mkdir -p /etc/brave/policies/managed/

2. A fájl szerkesztése:
Hozd létre a konfigurációt:
sudo nano /etc/brave/policies/managed/cleanbrave.json

3. Beillesztés:
Másold be a fenti JSON kódot, majd mentsd el (Ctrl+O, majd Enter) és lépj ki (Ctrl+X).

4. Érvényesítés:
Indítsd újra a Brave-et. A címsorba gépeld be: brave://policy.



Mire figyelj?
Default Browser: Ez a beállítás (DefaultBrowserSettingEnabled: false) letiltja, hogy a Brave folyamatosan kérdezgesse, legyen-e ő az alapértelmezett.
Password Manager: A PasswordManagerEnabled: false miatt a Brave nem fogja felajánlani a jelszavak mentését. Ha ezt mégis szeretnéd használni, írd át true-ra a fájlban.
Manifest V2: Az utolsó sor (ExtensionManifestV2Availability: 2) azért felel, hogy a régi típusú bővítmények (pl. uBlock Origin régebbi verziói) tovább működjenek, amíg a Google végleg le nem tiltja őket.


-------------------------------------------------

Ahhoz, hogy a Brave be tudja olvasni a beállításokat, a fájlnak a rendszer (root) tulajdonában kell lennie, és mindenki számára olvashatónak kell maradnia.
Futtasd le az alábbi parancsot a terminálban:
bash
ls -l /etc/brave/policies/managed/cleanbrave.json


Mit kell látnod a válaszban?

Valami ilyesmit:
-rw-r--r-- 1 root root ... cleanbrave.json


Ha nem így néz ki, javítsd ki ezekkel a parancsokkal:
Tulajdonjog beállítása: (hogy a rendszer felügyelje a fájlt)
sudo chown root:root /etc/brave/policies/managed/cleanbrave.json
Jogosultságok beállítása: (hogy bárki olvashassa, de csak a root módosíthassa)
sudo chmod 644 /etc/brave/policies/managed/cleanbrave.json


Utolsó simítás: Validálás
A JSON formátum nagyon kényes a vesszőkre és zárójelekre. Futtasd le ezt a parancsot, hogy ellenőrizd, nem maradt-e benne hiba:
bash
python3 -m json.tool /etc/brave/policies/managed/cleanbrave.json > /dev/null && echo "A fájl szerkezete OK!" || echo "Hiba van a JSON fájlban!"

Ha a válasz "A fájl szerkezete OK!", akkor már csak egy újraindítás kell a böngészőnek.


EGYENLŐRE ELLENŐRZÉS NÉLKÜL NEONITY LEÍRÁS MÁSOLATA:


# CleanBrave
Debloat Brave using Windows Registry

## 🔒 Disabled Features

The following Brave features are explicitly disabled:

| Feature                         | Registry Key                       | Status    |
|---------------------------------|------------------------------------|-----------|
| Brave Rewards                   | `BraveRewardsDisabled`            | Disabled  |
| Brave Wallet                    | `BraveWalletDisabled`             | Disabled  |
| Brave VPN                       | `BraveVPNDisabled`                | Disabled  |
| Brave AI Chat                   | `BraveAIChatEnabled`              | Disabled  |
| Google Drive Integration        | `DriveDisabled`                   | Disabled  |
| Password Manager                | `PasswordManagerEnabled`          | Disabled  |
| Password Sharing                | `PasswordSharingEnabled`          | Disabled  |
| Password Leak Detection         | `PasswordLeakDetectionEnabled`    | Disabled  |
| Quick Answers                   | `QuickAnswersEnabled`             | Disabled  |
| Parcel Tracking                 | `ParcelTrackingEnabled`           | Disabled  |
| Shopping List                   | `ShoppingListEnabled`             | Disabled  |
| Guest Mode                      | `BrowserGuestModeEnabled`         | Disabled  |
| Browser Sign-in                 | `BrowserSignin`                   | Disabled  |
| Built-in DNS Client             | `BuiltInDnsClientEnabled`         | Disabled  |
| Set as Default Browser          | `DefaultBrowserSettingEnabled`    | Disabled  |
| Background Mode                 | `BackgroundModeEnabled`           | Disabled  |
| Autofill Credit Cards           | `AutofillCreditCardEnabled`       | Disabled  |

---

## 🔍 Telemetry & Reporting

All telemetry, reporting, and device data sharing settings are disabled:

| Functionality                      | Registry Key                           | Status    |
|------------------------------------|----------------------------------------|-----------|
| Cloud Reporting                    | `CloudReportingEnabled`               | Disabled  |
| Safe Browsing Extended Reporting   | `SafeBrowsingExtendedReportingEnabled`| Disabled  |
| Safe Browsing Surveys              | `SafeBrowsingSurveysEnabled`          | Disabled  |
| Deep Scanning                      | `SafeBrowsingDeepScanningEnabled`     | Disabled  |
| Metrics & Heartbeats               | `DeviceMetricsReportingEnabled`, `HeartbeatEnabled`, `DeviceActivityHeartbeatEnabled`, `LogUploadEnabled` | Disabled |
| Device Activity & Inventory        | `ReportAppInventory`, `ReportDeviceActivityTimes`, `ReportDeviceAppInfo`, `ReportDeviceSystemInfo`, `ReportDeviceUsers` | Disabled |
| Website Telemetry                  | `ReportWebsiteTelemetry`              | Disabled  |
| General Metrics Reporting          | `MetricsReportingEnabled`             | Disabled  |

---

## ⚙️ Default Permissions (Prompt or Block)

These default settings control how Brave handles specific browser API permissions:

| API / Setting              | Registry Key                     | Value | Description        |
|----------------------------|----------------------------------|--------|--------------------|
| Geolocation                | `DefaultGeolocationSetting`     | `2`    | Ask on use         |
| Notifications              | `DefaultNotificationsSetting`   | `2`    | Ask on use         |
| Local Fonts                | `DefaultLocalFontsSetting`      | `2`    | Ask on use         |
| Sensors                    | `DefaultSensorsSetting`         | `2`    | Ask on use         |
| Serial Port Access         | `DefaultSerialGuardSetting`     | `2`    | Ask on use         |

---

## 🧩 Extensions

| Setting                        | Registry Key                         | Value | Description                                  |
|--------------------------------|--------------------------------------|--------|----------------------------------------------|
| Extension Manifest V2 Support | `ExtensionManifestV2Availability`    | `2`    | Allow legacy Manifest V2 extensions          |

---

## ✅ Notes

- All `dword:00000000` = Disabled
- All `dword:00000001` = Enabled
- All `dword:00000002` = Prompt (Ask) for permission
- Empty strings like `""` indicate no reporting endpoint configured

This configuration is intended to maximize user privacy and minimize online tracking or feature creep in Brave browser.





