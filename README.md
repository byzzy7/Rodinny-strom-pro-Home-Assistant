# 🌳 Rodinný strom pro Home Assistant

[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-panel-41BDF5?logo=home-assistant&logoColor=white)](https://www.home-assistant.io/)
[![Verze](https://img.shields.io/badge/verze-3.0.0-brightgreen)](https://github.com/)
[![Licence](https://img.shields.io/badge/licence-MIT-blue)](LICENSE)
[![Jazyk](https://img.shields.io/badge/jazyk-čeština-red)](README.md)
[![HTML](https://img.shields.io/badge/technologie-HTML%20%2F%20JS%20%2F%20SVG-orange)](family-tree-v2.html)

> Moderní, barevná genealogická aplikace přímo v Home Assistantu. Žádný server, žádná databáze — jeden HTML soubor, vše lokálně.

---

## ✨ Funkce

| Funkce | Popis |
|--------|-------|
| 🌲 **Interaktivní strom** | Vizualizace rodinných vazeb s pan & zoom |
| 🎨 **Barevné generace** | Každá generace má vlastní barvu (prarodiče → vnuci) |
| 🔍 **Vyhledávání** | Živé vyhledávání podle jména, roku i místa |
| 👤 **Přidání / editace / mazání** | Plný správce osob s formulářem |
| 📷 **Fotografie** | Nahrání fotek přímo do aplikace |
| 📝 **Poznámky** | Životopis, povolání, dokumenty pro každou osobu |
| 📅 **Časová osa** | Timeline všech osob podle roku narození |
| 🌙 **Tmavý režim** | Přepínač světlé / tmavé téma |
| 📂 **Import GEDCOM** | Import z Ancestry, MyHeritage, Gramps, FamilySearch |
| 📤 **Export** | JSON, GEDCOM, CSV, Tisk / PDF |
| 🔗 **Sdílení** | Sdílení celého stromu přes URL (data v hashu) |
| 📱 **Dotykové ovládání** | Funguje na tabletech a mobilech |

---

## 🖼️ Ukázky

### Světlý režim
```
Barevné kartičky, srdíčka ♥ mezi partnery, generační barevné kódování
```

### Tmavý režim
```
Přepínač 🌙 v hlavičce — tmavé pozadí, zachované barvy generací
```

### Časová osa
```
Horizontální pruhy podle roku narození, seřazené chronologicky
```

---

## 🚀 Instalace do Home Assistantu

### Krok 1 — Nahrání souboru

Zkopíruj `family-tree-v2.html` do složky `www` v konfiguraci Home Assistantu:

```
/config/www/family-tree-v2.html
```

> 💡 Pokud složka `www` neexistuje, vytvoř ji.

**Možnosti nahrání:**

| Metoda | Popis |
|--------|-------|
| **File Editor addon** | Nastavení → Doplňky → File Editor → otevři `/config/www/` |
| **Samba share** | `\\IP_ADRESA\config\www\` z Windows průzkumníka |
| **SSH / Terminal** | `cp family-tree-v2.html /config/www/` |
| **Studio Code Server** | VS Code přímo v HA |

### Krok 2 — Ověření dostupnosti

Otevři v prohlížeči:
```
http://IP_ADRESA_HA:8123/local/family-tree-v2.html
```

### Krok 3 — Přidat kartu na dashboard

1. Otevři dashboard → klikni na **tužku** (Upravit)
2. Klikni na **+ Přidat kartu**
3. Vyber typ **Webová stránka** (Webpage / iframe)
4. Zadej URL:

```yaml
url: /local/family-tree-v2.html
```

5. Nastav výšku karty — doporučeno **700 px** nebo více
6. Ulož → Hotovo!

### Volitelně — Celostránkový panel

Pro zobrazení na celou obrazovku bez záhlaví HA:

```yaml
# configuration.yaml nebo Nastavení → Dashboardy
panel_iframe:
  rodina:
    title: "Rodinný strom"
    icon: mdi:family-tree
    url: /local/family-tree-v2.html
```

---

## 📖 Použití

### Navigace v stromu

| Akce | Ovládání |
|------|----------|
| Posun | Tažení myší / prst na dotykové obrazovce |
| Přiblížení | Kolečko myši / pinch gesture |
| Zoom tlačítka | `＋` `－` `⌖` vpravo dole |
| Detail osoby | Klik na kartičku |

### Přidání osoby

1. Klikni na **＋ Přidat** v pravém horním rohu
2. Vyplň jméno, rok narození, pohlaví
3. Volitelně: fotografie, místo, poznámky
4. Vyber rodiče a partnera ze seznamu
5. Ulož

### Import GEDCOM

1. Exportuj GEDCOM soubor z:
   - **Ancestry** → Nastavení → Exportovat strom → GEDCOM
   - **MyHeritage** → Rodokmen → Exportovat → GEDCOM
   - **Gramps** → Rodina → Export → GEDCOM
   - **FamilySearch** → Stáhnout GEDCOM
2. Klikni na **📂 GEDCOM** v hlavičce
3. Vyber soubor `.ged` nebo `.gedcom`

### Export dat

Klikni na **📤 Export** a vyber formát:

| Formát | Obsah |
|--------|-------|
| **JSON** | Kompletní data včetně fotek (base64) |
| **GEDCOM** | Standardní genealogický formát pro import do jiných aplikací |
| **CSV** | Tabulka osob pro Excel / Google Sheets |
| **Tisk** | Vytiskne aktuální pohled stromu |

### Sdílení

1. Klikni na **🔗 Sdílet**
2. Zkopíruj vygenerovaný URL
3. Pošli odkaz — příjemce otevře strom s načtenými daty

> ⚠️ Fotografie se do sdíleného odkazu nezahrnují (URL by byl příliš dlouhý). Sdílí se pouze textová data.

---

## 🗂️ Struktura projektu

```
rodinna-strom-ha/
├── family-tree-v3.html    # Celá aplikace (jeden soubor)
├── README.md              # Tato dokumentace
├── LICENSE                # MIT licence
└── examples/
    └── sample.ged         # Ukázkový GEDCOM soubor
```

---

## 🔧 Technologie

Aplikace je záměrně navržena jako **jeden HTML soubor bez závislostí**:

- **Čisté HTML / CSS / JavaScript** — žádné frameworky
- **SVG** pro vykreslení stromu a časové osy
- **Base64** pro ukládání fotografií přímo v HTML
- **URL hash** pro sdílení dat bez serveru
- **CSS proměnné** pro světlý / tmavý režim

### Kompatibilita

| Prostředí | Podpora |
|-----------|---------|
| Home Assistant (webový panel) | ✅ |
| Chrome / Edge | ✅ |
| Firefox | ✅ |
| Safari | ✅ |
| Mobilní prohlížeče | ✅ |
| Tablet (dotykové ovládání) | ✅ |

---

## 🎨 Barevné kódování generací

| Barva | Generace |
|-------|----------|
| 🔴 Červená | Prarodiče (generace 0) |
| 🟡 Zlatá | Rodiče (generace 1) |
| 🔵 Modrá | Já / sourozenci (generace 2) |
| 🟢 Zelená (teal) | Děti (generace 3) |
| 🟣 Fialová | Vnuci (generace 4) |
| 🟠 Oranžová | Další generace |

---

## 📋 Plánované funkce

- [ ] Ukládání dat do `localStorage` (perzistence mezi session)
- [ ] Podpora více stromů / rodin
- [ ] Napojení na Home Assistant API (entity pro narozeniny)
- [ ] Automatické upozornění na výročí narozenin
- [ ] Rozšířené statistiky (průměrný věk, nejčastější jméno...)
- [ ] Miniatura stromu pro navigaci
- [ ] Filtrování větví stromu

---

## 📝 Changelog

### v3.0.0
- Celé datum narození/úmrtí (den.měsíc.rok místo jen roku)
- Příjmení za svobodna pro ženy (uloženo, zobrazeno v detailu)
- Ukládání dat na HA server přes REST API (`sensor.family_tree`)
- Nastavení HA připojení přes ⚙️ přímo v aplikaci
- Test spojení s HA
- Oprava cache — `no-cache` hlavičky
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



Příspěvky jsou vítány! Postup:

1. Forkni repozitář
2. Vytvoř větev: `git checkout -b feature/nova-funkce`
3. Commitni změny: `git commit -m 'Přidána nová funkce'`
4. Pushni větev: `git push origin feature/nova-funkce`
5. Otevři Pull Request

---

## 🐛 Hlášení chyb

Našel jsi chybu? Otevři [Issue](../../issues) s popisem:
- Co se stalo
- Co jsi očekával
- Verze Home Assistantu
- Prohlížeč

---

## 📄 Licence

Tento projekt je licencován pod licencí **MIT** — viz soubor [LICENSE](LICENSE).

---

## 🙏 Poděkování

- Komunita [Home Assistant](https://www.home-assistant.io/)
- Formát [GEDCOM](https://www.familysearch.org/developers/docs/gedcom/) od FamilySearch
- Inspirace projektem [webtrees](https://webtrees.net/)

---

<p align="center">
  Vytvořeno s ❤️ pro Home Assistant komunitu
</p>
