# Arbify - Gyors Fogadóiroda Link Megnyitó
# Arbify - Quick Bookmaker Link Opener

Egy egyszerű, GitHub Pages-kompatibilis webalkalmazás, amely két fogadóiroda linkjét nyitja meg egyidejűleg.

A simple, GitHub Pages-compatible web application that opens two bookmaker links simultaneously.

## 🚀 Funkciók / Features

- ✅ **Kettős link megnyitás** / Dual link opening
  - Első link új ablakban / First link in new tab
  - Második link jelenlegi ablakban / Second link in current tab
  
- ✅ **PWA támogatás** / PWA Support
  - Automatikus figyelmeztetés mobil felhasználóknak / Automatic warning for mobile users
  - Útmutató böngészőben való megnyitáshoz / Guidance for opening in browser

- ✅ **Modern UI**
  - Sötét téma / Dark theme
  - Animációk és vizuális visszajelzések / Animations and visual feedback
  - Reszponzív design / Responsive design

- ✅ **GitHub Pages kompatibilis**
  - Teljes működés hash-alapú paraméterekkel / Full functionality with hash-based parameters
  - Nincs szerver oldali komponens / No server-side components

## 📖 Használat / Usage

### Link generálás / Link Generation

A rendszer base64url-kódolt JSON objektumot használ a hash fragmentben:

The system uses a base64url-encoded JSON object in the hash fragment:

```
https://arbify.hu/#p=<BASE64URL_ENCODED_JSON>&PWA=true
```

### JSON struktúra / JSON Structure

```json
{
  "bookmaker1": "Első fogadóiroda neve",
  "bookmaker2": "Második fogadóiroda neve",
  "link1": "https://first-bookmaker.com",
  "link2": "https://second-bookmaker.com"
}
```

### Példa link generálás / Example Link Generation

```javascript
// 1. Adat objektum / Data object
const data = {
  bookmaker1: "Tippmix",
  bookmaker2: "BetSafe",
  link1: "https://tippmix.hu/fogadas",
  link2: "https://betsafe.com/bet"
};

// 2. Base64url kódolás / Base64url encoding
const base64url = btoa(JSON.stringify(data))
  .replace(/\+/g, '-')
  .replace(/\//g, '_')
  .replace(/=+$/, '');

// 3. Végső link / Final link
const finalLink = `https://arbify.hu/#p=${base64url}&PWA=true`;
```

## 📚 Dokumentáció / Documentation

A projekt két dokumentációs fájlt tartalmaz:

The project includes two documentation files:

1. **[LINK_GENERATION_GUIDE.md](LINK_GENERATION_GUIDE.md)** - Részletes útmutató / Detailed guide
   - Teljes technikai dokumentáció / Complete technical documentation
   - Kódpéldák többnyelvű / Code examples in multiple languages
   - Hibaelhárítás / Troubleshooting

2. **[AI_PROMPT.md](AI_PROMPT.md)** - AI promptok / AI prompts
   - Gyors prompt sablonok / Quick prompt templates
   - Lovable AI és más AI asszisztensekhez / For Lovable AI and other AI assistants
   - Kész kódsnippetek / Ready-to-use code snippets

## 🎯 Mikor használd a PWA paramétert / When to Use PWA Parameter

Csak akkor használd a `PWA=true` paramétert, ha:

Only use the `PWA=true` parameter if:

- ✅ A link mobil PWA alkalmazásból nyílik meg
- ✅ The link opens from a mobile PWA application
- ✅ Be akarod ágyazni mobil alkalmazásba
- ✅ You want to embed it in a mobile application

Ne használd ha:

Don't use if:

- ❌ Desktop böngészőből nyitod meg
- ❌ Opening from desktop browser
- ❌ Nem vagy biztos a környezetben
- ❌ You're not sure about the environment

## 🛠️ Technikai részletek / Technical Details

### Fájlstruktúra / File Structure

```
arbify/
├── index.html           # Fő alkalmazás fájl / Main application file
├── README.md           # Ez a fájl / This file
├── LINK_GENERATION_GUIDE.md  # Részletes útmutató / Detailed guide
└── AI_PROMPT.md        # AI prompt sablonok / AI prompt templates
```

### Követelmények / Requirements

- Modern böngésző / Modern browser
  - JavaScript támogatás / JavaScript support
  - ES6+ kompatibilitás / ES6+ compatibility
- URL Fragment (hash) támogatás / URL Fragment (hash) support

### Korlátozások / Limitations

- Csak http:// és https:// protokollok / Only http:// and https:// protocols
- Mindkét link kötelező / Both links are required
- Egyszer kattintható (átirányítás után) / Single-click (after redirect)

## 🔒 Biztonság / Security

- Nincs szerver oldali adattárolás / No server-side data storage
- Csak HTTPS protokoll támogatott / Only HTTPS protocol supported
- Linkek validálása a kliensen / Link validation on client
- noopener és noreferrer flag használata / Using noopener and noreferrer flags

## 🌐 Böngésző támogatás / Browser Support

- ✅ Chrome/Edge (legújabb 2 verzió / latest 2 versions)
- ✅ Firefox (legújabb 2 verzió / latest 2 versions)
- ✅ Safari (legújabb 2 verzió / latest 2 versions)
- ✅ Mobile Safari (iOS 14+)
- ✅ Chrome Mobile (Android 10+)

## 📱 PWA funkciók / PWA Features

### Banner megjelenítés / Banner Display

Ha `PWA=true` paraméter jelen van, a banner:

When `PWA=true` parameter is present, the banner:

- Automatikusan megjelenik / Automatically appears
- Útmutatást ad platform-specifikusan / Provides platform-specific guidance
- Bezárható az X gombbal / Closable with X button

### Platform-specifikus útmutatók / Platform-specific Guidance

**iOS:**
- "Megnyitás Safariban" opció használata
- Using "Open in Safari" option

**Android:**
- "Megnyitás Chrome-ban" menüpont
- Using "Open in Chrome" menu option

## 🎨 UI Elemek / UI Elements

### Vizuális visszajelzések / Visual Feedback

- Animált nyíl ikon / Animated arrow icon
- Pulse animáció a banneren / Pulse animation on banner
- Hover effektek / Hover effects
- Letiltott állapot jelzése / Disabled state indication

### Színséma / Color Scheme

- Sötét téma alapértelmezés / Dark theme by default
- Emerald zöld akcióra / Emerald green for actions
- Amber sárga figyelmeztetésekre / Amber yellow for warnings

## 🤝 Hozzájárulás / Contributing

Ez egy egyszerű, statikus projekt. Ha fejlesztési ötleted van:

This is a simple, static project. If you have improvement ideas:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 Licenc / License

Ez a projekt nyílt forráskódú.

This project is open source.

## 💡 Tippek / Tips

### Domain konfiguráció / Domain Configuration

A dokumentációban és példákban az `arbify.hu` domain név szerepel. Ha a domain megváltozik, frissíteni kell:
- README.md példákat
- test.html fájlban a baseUrl változót
- AI_PROMPT.md és QUICK_REFERENCE.md példákat
- LINK_GENERATION_GUIDE.md dokumentációt

The documentation and examples use the `arbify.hu` domain name. If the domain changes, update:
- README.md examples
- test.html baseUrl variable
- AI_PROMPT.md and QUICK_REFERENCE.md examples
- LINK_GENERATION_GUIDE.md documentation

### Link tesztelés / Link Testing

Tesztelés előtt ellenőrizd:

Before testing, check:

1. Mindkét URL érvényes és elérhető / Both URLs are valid and reachable
2. Base64url kódolás helyes (-, _ karakterek) / Base64url encoding is correct (-, _ characters)
3. JSON struktúra helyes / JSON structure is correct

### Gyakori hibák / Common Mistakes

❌ **Hibás:** `https://arbify.hu/#p=eyJ...=&PWA=true` (= karakter a végén)
✅ **Helyes:** `https://arbify.hu/#p=eyJ...Q&PWA=true` (nincs = karakter)

❌ **Hibás:** `{"link1": "/path"}` (relatív URL)
✅ **Helyes:** `{"link1": "https://example.com/path"}` (teljes URL)

## 🔗 Hasznos linkek / Useful Links

- [Base64 Encoder/Decoder](https://www.base64encode.org/)
- [JSON Validator](https://jsonlint.com/)
- [URL Encoder](https://www.urlencoder.org/)

## 📞 Támogatás / Support

Ha kérdésed van vagy problémába ütközöl:

If you have questions or run into issues:

1. Olvasd el a [LINK_GENERATION_GUIDE.md](LINK_GENERATION_GUIDE.md) fájlt
2. Nézd meg az [AI_PROMPT.md](AI_PROMPT.md) példákat
3. Nyiss egy issue-t a GitHub repository-ban

---

**Készítette / Made with** ❤️ **az akadálymentesség jegyében / for accessibility**
