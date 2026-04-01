# 🌳 Rodinný strom pro Home Assistant

[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-panel-41BDF5?logo=home-assistant&logoColor=white)](https://www.home-assistant.io/)
[![Verze](https://img.shields.io/badge/verze-3.2.0-brightgreen)](https://github.com/)
[![Licence](https://img.shields.io/badge/licence-MIT-blue)](LICENSE)
[![Jazyk](https://img.shields.io/badge/jazyk-čeština-red)](README.md)
[![HTML](https://img.shields.io/badge/technologie-HTML%20%2F%20JS%20%2F%20SVG-orange)](family-tree-v3.html)

> Moderní genealogická aplikace přímo v Home Assistantu. Jeden HTML soubor, žádné frameworky — data se ukládají na HA server nebo do localStorage.

---

## ✨ Funkce

| Funkce | Popis |
|--------|-------|
| 🌲 **Interaktivní strom** | SVG strom s pan & zoom, karty umístěné pod rodiče |
| 🎨 **Barevné rodinné větve** | Každá větev má vlastní barvu, spojovací čáry s glow efektem |
| 🔍 **Vyhledávání** | Živé vyhledávání podle jména, roku i místa |
| 👤 **Správa osob** | Přidání, editace, mazání s formulářem |
| 📷 **Fotografie** | Nahrání fotek přímo do aplikace (base64) |
| 📝 **Poznámky** | Životopis, povolání, dokumenty pro každou osobu |
| 👨‍👩‍👧 **Sourozenci** | Přiřazení sourozence i bez společných rodičů |
| 🎂 **Narozeniny** | Indikátor dnes / brzy na kartičce i v detailu |
| 📅 **Časová osa** | Timeline všech osob podle roku narození |
| 📊 **Statistiky** | Počty osob, generací, rodin, jmen, příjmení, pohlaví |
| 🌙 **Tmavý režim** | Přepínač světlé / tmavé téma, uloženo v localStorage |
| 📂 **Import GEDCOM** | Import z Ancestry, MyHeritage, Gramps, FamilySearch |
| 📤 **Export** | JSON, GEDCOM, CSV, Tisk / PDF |
| 🔗 **Sdílení** | Sdílení celého stromu přes URL (data v Base64 hashu) |
| 💾 **Home Assistant sync** | Ukládání dat jako `sensor.family_tree` přes REST API |
| 📱 **Mobilní podpora** | Dotykové ovládání, pinch zoom, hamburger menu |

---

## 🚀 Instalace do Home Assistantu

### Krok 1 — Nahrání souboru

Zkopíruj `family-tree-v3.html` do složky `www` v konfiguraci Home Assistantu:

```
/config/www/family-tree-v3.html
```

> Pokud složka `www` neexistuje, vytvoř ji.

**Možnosti nahrání:**

| Metoda | Popis |
|--------|-------|
| **File Editor addon** | Nastavení → Doplňky → File Editor → otevři `/config/www/` |
| **Samba share** | `\\IP_ADRESA\config\www\` z Windows průzkumníka |
| **SSH / Terminal** | `cp family-tree-v3.html /config/www/` |
| **Studio Code Server** | VS Code přímo v HA |

### Krok 2 — Ověření dostupnosti

Otevři v prohlížeči:
```
http://IP_ADRESA_HA:8123/local/family-tree-v3.html
```

### Krok 3 — Přidat kartu na dashboard

1. Otevři dashboard → klikni na **tužku** (Upravit)
2. Klikni na **+ Přidat kartu**
3. Vyber typ **Webová stránka** (Webpage / iframe)
4. Zadej URL:

```yaml
url: /local/family-tree-v3.html
```

5. Nastav výšku karty — doporučeno **700 px** nebo více
6. Ulož → Hotovo!

### Volitelně — Celostránkový panel

```yaml
# configuration.yaml
panel_iframe:
  rodina:
    title: "Rodinný strom"
    icon: mdi:family-tree
    url: /local/family-tree-v3.html
```

---

## 💾 Synchronizace s Home Assistantem

Aplikace umí ukládat data přímo na HA server jako entitu `sensor.family_tree`. Data pak přežijí vymazání cache prohlížeče a jsou dostupná ze všech zařízení v síti.

### Nastavení

1. Klikni na **⚙️** v hlavičce
2. Zadej adresu HA (např. `http://homeassistant.local:8123`)
3. Vlož **Long-Lived Access Token** (Profil → Bezpečnost → Tokeny)
4. Klikni **🔌 Test spojení** pro ověření
5. Ulož

Bez HA konfigurace se data ukládají pouze do `localStorage` prohlížeče.

---

## 📖 Použití

### Navigace ve stromu

| Akce | Ovládání |
|------|----------|
| Posun | Tažení myší / prst na dotykové obrazovce |
| Přiblížení | Kolečko myši / pinch gesture |
| Zoom tlačítka | `＋` `－` `⌖` vpravo dole |
| Detail osoby | Klik na kartičku |
| Zavřít detail | `✕` v panelu nebo klik mimo |

### Přidání osoby

1. Klikni na **＋ Přidat** v pravém horním rohu
2. Vyplň jméno, datum narození, pohlaví
3. Volitelně: fotografie, místo, poznámky, příjmení za svobodna
4. Vyber rodiče, sourozence nebo partnera ze seznamu
5. Ulož

### Sourozenectví

Sourozenecký vztah lze nastavit dvěma způsoby:
- **Se společnými rodiči** — stačí vybrat stejné rodiče, sourozenci se detekují automaticky
- **Bez rodičů** (kořenová úroveň) — vyber sourozence v poli „Sourozenec / Sourozenka", propojení se uloží explicitně

### Import GEDCOM

1. Exportuj GEDCOM z Ancestry, MyHeritage, Gramps nebo FamilySearch
2. Klikni na **📂 GEDCOM** v hlavičce
3. Vyber soubor `.ged` nebo `.gedcom`

### Export dat

| Formát | Obsah |
|--------|-------|
| **JSON** | Kompletní data včetně fotek (base64) |
| **GEDCOM** | Standardní formát pro import do jiných aplikací |
| **CSV** | Tabulka osob pro Excel / Google Sheets |
| **Tisk / PDF** | Tisk aktuálního pohledu stromu |

### Sdílení

1. Klikni na **🔗 Sdílet**
2. Zkopíruj vygenerovaný URL
3. Pošli odkaz — příjemce uvidí strom s daty

> Data jsou zakódována přímo v URL (Base64). Fotografie se nesdílejí — URL by byl příliš dlouhý.

---

## 🎨 Barevné kódování

### Rodinné větve
Každá rodinná linie má přiřazenou barvu (červená, modrá, zelená, zlatá…). Barva se promítá do:
- Barevného pruhu na kartičce
- Spojovacích čar (s glow efektem)
- Legendy vlevo dole

### Narozeniny
| Indikátor | Význam |
|-----------|--------|
| 🎂 zlatý rámeček | Dnes má narozeniny |
| 🎁 | Narozeniny do 7 dnů |

---

## 🗂️ Struktura projektu

```
rodinna-strom-ha/
├── family-tree-v3.html    # Celá aplikace (jeden soubor)
├── README.md              # Tato dokumentace
└── LICENSE                # MIT licence
```

---

## 🔧 Technologie

Aplikace je záměrně navržena jako **jeden HTML soubor bez závislostí**:

- **HTML / CSS / JavaScript** — žádné frameworky, žádné npm balíčky
- **SVG** pro vykreslení stromu, spojovacích čar a časové osy
- **CSS proměnné** pro světlý / tmavý režim
- **Base64** pro ukládání fotografií
- **URL hash** pro sdílení dat bez serveru
- **Home Assistant REST API** pro persistentní uložení dat

### Kompatibilita

| Prostředí | Podpora |
|-----------|---------|
| Home Assistant (webový panel / iframe) | ✅ |
| Chrome / Edge | ✅ |
| Firefox | ✅ |
| Safari | ✅ |
| Mobilní prohlížeče | ✅ |
| Tablet (dotykové ovládání, pinch zoom) | ✅ |

---

## 📝 Changelog

### v3.2.0
- Sourozenci bez společných rodičů (explicitní `sibids` propojení)
- Barevné spojovací čáry podle rodinné větve s glow efektem
- Srdíčko partnerů v kroužku, správně centrované
- Nové řazení karet — děti umístěny pod rodiče místo globálního centrování
- Oprava determinismu layoutu (strom se nepřeuspořádává po kliknutí)

### v3.1.0
- Statistiky — počty osob, generací, rodin, jmen, příjmení, pohlaví
- Narozeninové indikátory na kartičkách i v detailu osoby
- Mobilní hamburger menu
- Dotykové ovládání a pinch zoom
- Automatická detekce změny souboru a reload cache

### v3.0.0
- Ukládání dat na HA server přes REST API (`sensor.family_tree`)
- Nastavení HA připojení a test spojení přímo v aplikaci
- Celé datum narození/úmrtí (den.měsíc.rok)
- Příjmení za svobodna pro ženy
- localStorage jako záloha při výpadku HA

### v2.0.0
- Vyhledávání osob
- Editace a mazání osob
- Fotografie / avatary
- Export JSON, GEDCOM, CSV, tisk
- Sdílení přes URL hash
- Poznámky a dokumenty
- Tmavý režim
- Časová osa (Timeline)

### v1.0.0
- Základní interaktivní strom
- Import GEDCOM
- Přidávání osob
- Barevné generace

---

## 🐛 Hlášení chyb

Našel jsi chybu? Otevři [Issue](../../issues) s popisem:
- Co se stalo a co jsi očekával
- Verze Home Assistantu a prohlížeče

---

## 📄 Licence

Tento projekt je licencován pod licencí **MIT** — viz soubor [LICENSE](LICENSE).

---

## 🙏 Poděkování

- Komunita [Home Assistant](https://www.home-assistant.io/)
- Formát [GEDCOM](https://www.familysearch.org/developers/docs/gedcom/) od FamilySearch

---

<p align="center">
  Vytvořeno s ❤️ pro Home Assistant komunitu
</p>
