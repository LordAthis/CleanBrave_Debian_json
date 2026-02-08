# CleanBrave_Debian_json
Neonity által windows alá elkészített regisztry értékek linuxos átirata json beállítási fájlba

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
 

