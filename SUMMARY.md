# Összefoglaló / Summary

## Mi ez a projekt? / What is this project?

Az Arbify egy GitHub Pages-kompatibilis egyoldalas webalkalmazás, amely két fogadóiroda linkjét nyitja meg egyidejűleg egyetlen kattintással.

Arbify is a GitHub Pages-compatible single-page web application that opens two bookmaker links simultaneously with a single click.

## Új dokumentáció / New Documentation

Ez a PR négy új dokumentációs fájlt ad hozzá a projekthez:

This PR adds four new documentation files to the project:

### 1. README.md
**Célközönség / Target Audience:** Általános felhasználók és fejlesztők / General users and developers

**Tartalom / Content:**
- Projekt áttekintés / Project overview
- Főbb funkciók / Main features  
- Használati útmutató / Usage guide
- Technikai részletek / Technical details
- Böngésző támogatás / Browser support
- PWA funkciók / PWA features

**Használd amikor / Use when:** 
- Először találkozol a projekttel / First time seeing the project
- Gyors áttekintést szeretnél / Want a quick overview
- Telepítési útmutatót keresel / Looking for setup instructions

### 2. LINK_GENERATION_GUIDE.md
**Célközönség / Target Audience:** Fejlesztők / Developers

**Tartalom / Content:**
- Részletes technikai specifikáció / Detailed technical specification
- Lépésről-lépésre kódolási útmutató / Step-by-step encoding guide
- JavaScript és Python példák / JavaScript and Python examples
- PWA paraméter magyarázat / PWA parameter explanation
- Teljes működő példák / Complete working examples
- Hibaelhárítás / Troubleshooting

**Használd amikor / Use when:**
- Link generáló kódot írsz / Writing link generation code
- Részletes technikai információra van szükséged / Need detailed technical information
- Problémát kell megoldanod / Need to solve a problem

### 3. AI_PROMPT.md  
**Célközönség / Target Audience:** AI asszisztensek (Lovable AI, ChatGPT, stb.) / AI assistants

**Tartalom / Content:**
- Gyors prompt sablonok / Quick prompt templates
- Magyar és angol verziók / Hungarian and English versions
- Kompakt kód példák / Compact code examples
- Fontos szabályok / Important rules
- Gyakori hibák / Common mistakes

**Használd amikor / Use when:**
- AI-t kérsz link generálásra / Asking AI to generate links
- Gyors referenciát szeretnél / Want a quick reference
- Prompt sablonra van szükséged / Need a prompt template

### 4. QUICK_REFERENCE.md
**Célközönség / Target Audience:** Tapasztalt fejlesztők / Experienced developers

**Tartalom / Content:**
- Minimális kód példák / Minimal code examples
- Multi-nyelv támogatás / Multi-language support (JS, Python, PHP, Ruby, Go, C#, Java)
- CLI eszközök (Bash, PowerShell) / CLI tools
- Gyors keresési táblázat / Quick lookup table
- Ellenőrző lista / Checklist

**Használd amikor / Use when:**
- Gyorsan kell implementálnod / Need to implement quickly
- Másik programozási nyelvet használsz / Using a different programming language
- Referencia kártya kell / Need a reference card

### 5. test.html
**Célközönség / Target Audience:** Mindenki / Everyone

**Tartalom / Content:**
- Interaktív link generátor / Interactive link generator
- Élő tesztelés / Live testing
- Előre elkészített teszt linkek / Pre-made test links
- Vizuális visszajelzés / Visual feedback

**Használd amikor / Use when:**
- Linket szeretnél generálni böngészőben / Want to generate links in browser
- Tesztelni szeretnéd a funkciót / Want to test functionality
- Látni akarod a működést / Want to see it in action

## Link Generálás Folyamata / Link Generation Process

```
1. Adat bemenet / Data input
   ↓
2. JSON objektum létrehozása / Create JSON object
   {
     "bookmaker1": "Name1",
     "bookmaker2": "Name2", 
     "link1": "https://...",
     "link2": "https://..."
   }
   ↓
3. JSON → String / JSON to String
   ↓
4. Base64 kódolás / Base64 encoding
   ↓
5. Base64URL konverzió / Base64URL conversion
   (+ → -, / → _, remove =)
   ↓
6. URL összeállítás / URL assembly
   https://arbify.hu/#p=<BASE64URL>[&PWA=true]
   ↓
7. Link kész! / Link ready!
```

## Használati Példa / Usage Example

### Forgatókönyv / Scenario
Két fogadóiroda linkjét szeretnéd egyszerre megnyitni.

You want to open two bookmaker links at once.

### Lépések / Steps

1. **Adat előkészítés / Prepare data:**
   ```
   Fogadóiroda 1: Tippmix
   Fogadóiroda 2: BetSafe
   Link 1: https://tippmix.hu/fogadas
   Link 2: https://betsafe.com/bet
   ```

2. **Link generálás / Generate link:**
   - Használd a test.html oldalt / Use test.html page
   - VAGY használd a kód példákat / OR use code examples
   - VAGY küld el a AI_PROMPT.md-t egy AI-nak / OR send AI_PROMPT.md to an AI

3. **Eredmény / Result:**
   ```
   https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUvZm9nYWRhcyIsImxpbmsyIjoiaHR0cHM6Ly9iZXRzYWZlLmNvbS9iZXQifQ
   ```

4. **Használat / Usage:**
   - Nyisd meg a linket / Open the link
   - Kattints a gombra / Click the button
   - Link1 új ablakban nyílik / Link1 opens in new tab
   - Link2 jelenlegi ablakban / Link2 in current tab

## PWA Funkció / PWA Feature

### Mikor használd / When to use:
Ha a linket mobil PWA alkalmazásból fogják megnyitni.

If the link will be opened from a mobile PWA application.

### Mit csinál / What it does:
- Megjelenít egy figyelmeztető bannert / Shows a warning banner
- iOS: "Megnyitás Safariban" útmutató / iOS: "Open in Safari" guidance
- Android: "Megnyitás Chrome-ban" útmutató / Android: "Open in Chrome" guidance

### Hogyan használd / How to use:
Adj hozzá `&PWA=true` a link végére:
Add `&PWA=true` to the end of the link:

```
https://arbify.hu/#p=<BASE64URL>&PWA=true
```

## Gyakori Kérdések / FAQ

### Q: Miért hash (#) és nem query (?) paraméter?
### Q: Why hash (#) and not query (?) parameter?

**A:** GitHub Pages kompatibilitás miatt. A hash paraméterek kliens oldalon működnek, szerver oldali konfiguráció nélkül.

**A:** For GitHub Pages compatibility. Hash parameters work client-side without server-side configuration.

### Q: Mi a különbség base64 és base64url között?
### Q: What's the difference between base64 and base64url?

**A:** Base64url URL-barát karakter cserékkel:
- `+` → `-`
- `/` → `_`
- `=` eltávolítva / removed

**A:** Base64url uses URL-safe character replacements.

### Q: Kötelező mindkét bookmaker név?
### Q: Are both bookmaker names required?

**A:** Nem, csak a linkek kötelezőek. A nevek opcionálisak, de javítják a felhasználói élményt.

**A:** No, only links are required. Names are optional but improve user experience.

### Q: Működik mobilon?
### Q: Does it work on mobile?

**A:** Igen! PWA móddal még jobb mobil támogatás van.

**A:** Yes! With PWA mode there's even better mobile support.

### Q: Mennyi link generálható?
### Q: How many links can be generated?

**A:** Korlátlan. Minden link stateless, nincs szerver oldali tárolás.

**A:** Unlimited. All links are stateless, no server-side storage.

## Biztonság / Security

### ✅ Biztonságos / Secure:
- Nincs szerver oldali adattárolás / No server-side data storage
- Csak HTTPS linkek / Only HTTPS links
- Client-side validáció / Client-side validation
- noopener, noreferrer flagek / flags

### ⚠️ Fontos / Important:
- Linkek láthatóak az URL-ben / Links are visible in URL
- Ne ossz meg érzékeny linkeket / Don't share sensitive links
- Csak megbízható forrásból származó linkeket használj / Only use links from trusted sources

## Teljesítmény / Performance

- ⚡ Gyors betöltés / Fast loading (single HTML file)
- 📦 Kis méret / Small size (~13KB index.html)
- 🚀 Nincs függőség / No dependencies
- 💾 Offline működés / Works offline (after first load)

## Jövőbeli Fejlesztések / Future Enhancements

Lehetséges továbbfejlesztések:

Possible enhancements:

- [ ] Könyvjelző funkció / Bookmark feature
- [ ] Link előzmények (localStorage) / Link history (localStorage)
- [ ] Több mint 2 link támogatása / Support for more than 2 links
- [ ] QR kód generálás / QR code generation
- [ ] Link rövidítő integráció / URL shortener integration
- [ ] Testreszabható téma / Customizable theme
- [ ] Statisztikák (kattintások) / Statistics (clicks)

## Közreműködés / Contributing

Ha szeretnél hozzájárulni:

If you want to contribute:

1. Fork a repository-t / Fork the repository
2. Hozz létre egy feature branch-et / Create a feature branch
3. Commitold a változásokat / Commit your changes
4. Nyiss egy pull request-et / Open a pull request

## Licenc / License

Nyílt forráskódú projekt. / Open source project.

---

**Verzió / Version:** 1.0  
**Utolsó frissítés / Last updated:** 2026-01-22  
**Dokumentáció készült / Documentation created by:** GitHub Copilot
