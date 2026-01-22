# Arbify - Quick Link Opener

Egyszerű webalkalmazás azonnali átirányításhoz no-referrer politikával.

## Funkciók

### 1. Instant Redirect (Azonnali átirányítás)

Egyetlen URL paraméterrel egyszerű, azonnali átirányítást hajthatsz végre no-referrer fejléccel.

**Használat:**

```
# Hash alapú paraméter
https://example.com/#g=https://target-site.com

# Query alapú paraméter  
https://example.com/?g=https://target-site.com
```

**Példák:**

```
# Átirányítás Google-ra
https://arbify-bet.hu/#g=https://www.google.com

# Átirányítás GitHub-ra
https://arbify-bet.hu/?g=https://github.com

# URL-kódolt paraméter
https://arbify-bet.hu/#g=https%3A%2F%2Fexample.com%2Fpath%3Fquery%3Dvalue
```

**Jellemzők:**
- ✅ Azonnali átirányítás UI megjelenítése nélkül
- ✅ No-referrer politika (adatvédelem)
- ✅ Hash (#g=) és query (?g=) paraméter támogatás
- ✅ Automatikus URL dekódolás
- ✅ Biztonsági URL validáció

### 2. Dual Link Mode (Dupla link mód)

A normál működés során két link egyidejű megnyitását támogatja.

**Használat:**

```
# Base64 kódolt JSON paraméter
https://example.com/#p=<BASE64URL_JSON>
```

A JSON formátum:
```json
{
  "bookmaker1": "Fogadóiroda 1 neve",
  "link1": "https://first-link.com",
  "bookmaker2": "Fogadóiroda 2 neve", 
  "link2": "https://second-link.com"
}
```

## Biztonsági funkciók

- 🔒 **Protokoll validáció**: Csak `http://` és `https://` protokollok engedélyezettek
- 🔒 **No-referrer politika**: Megakadályozza a referrer információ kiszivárgását
- 🔒 **URL validáció**: Védelmet nyújt érvénytelen és veszélyes átirányítások ellen
- 🔒 **Blokkolt protokollok**: JavaScript, data, ftp és más veszélyes protokollok automatikusan blokkolva

## Technikai részletek

### Instant Redirect működése

1. Az oldal betöltődik
2. A JavaScript azonnal ellenőrzi a `g` paramétert (hash vagy query)
3. Ha megtalálható és érvényes:
   - Beállítja a `no-referrer` meta tag-et
   - Validálja az URL-t (csak http/https)
   - Azonnali átirányítás `window.location.replace()` használatával
4. Ha nincs `g` paraméter, megjeleníti a normál UI-t

### Implementáció

```javascript
// Meta tag a fejlécben
<meta name="referrer" content="no-referrer" />

// JavaScript logika
const gParam = hashParts.get("g") || queryParts.get("g");
if (gParam) {
  const redirectUrl = normalizeUrl(safeDecode(gParam));
  if (redirectUrl) {
    window.location.replace(redirectUrl);
    return;
  }
}
```

## GitHub Pages Deployment

Az alkalmazás automatikusan települ GitHub Pages-re amikor változtatásokat pusholsz a `main` branch-be.

## Licenc

Ez egy nyílt forráskódú projekt.
