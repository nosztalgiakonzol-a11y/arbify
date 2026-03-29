# Arbify Link Generation Guide

## A rendszer áttekintése / System Overview

Az arbify.hu egy gyors megnyitó szolgáltatás, amely két fogadóiroda linkjét egyidejűleg nyitja meg:
- Az első link új ablakban nyílik
- A második link az aktuális ablakban nyílik meg

The arbify.hu is a quick launch service that opens two bookmaker links simultaneously:
- First link opens in a new tab
- Second link opens in the current tab

## Link formátum / Link Format

### Alapvető struktúra / Basic Structure

```
https://arbify.hu/#p=<BASE64URL_ENCODED_JSON>
```

vagy PWA támogatással / or with PWA support:

```
https://arbify.hu/#p=<BASE64URL_ENCODED_JSON>&PWA=true
```

## JSON struktúra / JSON Structure

A `p` paraméter egy base64url kódolású JSON objektum, amely a következő mezőket tartalmazza:

The `p` parameter is a base64url-encoded JSON object containing the following fields:

```json
{
  "bookmaker1": "Fogadóiroda neve 1",
  "bookmaker2": "Fogadóiroda neve 2",
  "link1": "https://teljes-url-1.com",
  "link2": "https://teljes-url-2.com"
}
```

### Mezők / Fields:

- **bookmaker1**: Az első fogadóiroda neve (opcionális, de ajánlott)
- **bookmaker2**: A második fogadóiroda neve (opcionális, de ajánlott)
- **link1**: Az első link teljes URL-je (kötelező, http:// vagy https://)
- **link2**: A második link teljes URL-je (kötelező, http:// vagy https://)

## Base64URL kódolás / Base64URL Encoding

### Kódolási lépések / Encoding Steps:

1. Hozd létre a JSON objektumot
2. Konvertáld JSON stringgé
3. Kódold base64-be
4. Helyettesítsd a karaktereket:
   - `+` → `-`
   - `/` → `_`
   - Távolítsd el a záró `=` karaktereket

### Példa / Example:

```javascript
// 1. JSON objektum
const data = {
  "bookmaker1": "Tippmix",
  "bookmaker2": "BetSafe",
  "link1": "https://tippmix.hu/fogadas",
  "link2": "https://betsafe.com/bet"
};

// 2. JSON string
const jsonString = JSON.stringify(data);

// 3. Base64 kódolás
const base64 = btoa(jsonString);

// 4. Base64URL konverzió
const base64url = base64
  .replace(/\+/g, '-')
  .replace(/\//g, '_')
  .replace(/=+$/, '');

// 5. Végső link
const finalLink = `https://arbify.hu/#p=${base64url}`;
console.log(finalLink);
```

### Python példa / Python Example:

```python
import json
import base64

# 1. JSON objektum
data = {
    "bookmaker1": "Tippmix",
    "bookmaker2": "BetSafe",
    "link1": "https://tippmix.hu/fogadas",
    "link2": "https://betsafe.com/bet"
}

# 2. JSON string és kódolás
json_string = json.dumps(data)
base64_bytes = base64.b64encode(json_string.encode('utf-8'))
base64_string = base64_bytes.decode('utf-8')

# 3. Base64URL konverzió
base64url = base64_string.replace('+', '-').replace('/', '_').rstrip('=')

# 4. Végső link
final_link = f"https://arbify.hu/#p={base64url}"
print(final_link)
```

## PWA paraméter / PWA Parameter

### Mikor használd / When to Use:

Ha a linket PWA (Progressive Web App) alkalmazásból fogják megnyitni, add hozzá a `PWA=true` paramétert:

If the link will be opened from a PWA (Progressive Web App), add the `PWA=true` parameter:

```
https://arbify.hu/#p=<BASE64URL>&PWA=true
```

### Mit csinál / What it Does:

- Megjelenít egy figyelmeztető bannert mobil felhasználóknak
- Útmutatást ad iOS és Android felhasználóknak, hogyan nyissák meg a linket böngészőben
- iOS: "Megnyitás Safariban" opció
- Android: "Megnyitás Chrome-ban" opció

It will:
- Display a warning banner for mobile users
- Provide guidance for iOS and Android users on how to open the link in a browser
- iOS: "Open in Safari" option
- Android: "Open in Chrome" option

## Prompt Lovable AI számára / Prompt for Lovable AI

### Magyar verzió:

```
Generálj egy arbify.hu/#p= linket a következő adatokkal:

Fogadóiroda 1: [NÉV]
Fogadóiroda 2: [NÉV]
Link 1: [TELJES URL]
Link 2: [TELJES URL]

A link formátuma:
1. Hozz létre egy JSON objektumot ezekkel a mezőkkel: bookmaker1, bookmaker2, link1, link2
2. Kódold base64url formátumba (base64, de + → -, / → _, = eltávolítva)
3. Add hozzá a hash fragmenthez: https://arbify.hu/#p=<BASE64URL>
4. Ha PWA alkalmazásból nyílik meg, add hozzá: &PWA=true

Példa végeredmény:
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUvZm9nYWRhcyIsImxpbmsyIjoiaHR0cHM6Ly9iZXRzYWZlLmNvbS9iZXQifQ&PWA=true
```

### English version:

```
Generate an arbify.hu/#p= link with the following data:

Bookmaker 1: [NAME]
Bookmaker 2: [NAME]
Link 1: [FULL URL]
Link 2: [FULL URL]

Link format:
1. Create a JSON object with these fields: bookmaker1, bookmaker2, link1, link2
2. Encode it in base64url format (base64, but + → -, / → _, = removed)
3. Add to hash fragment: https://arbify.hu/#p=<BASE64URL>
4. If opening from PWA app, add: &PWA=true

Example result:
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUvZm9nYWRhcyIsImxpbmsyIjoiaHR0cHM6Ly9iZXRzYWZlLmNvbS9iZXQifQ&PWA=true
```

## Teljes példa / Complete Example

### Bemenet / Input:
- Fogadóiroda 1: "Szerencsejáték"
- Fogadóiroda 2: "Tipsport"
- Link 1: "https://szerencsejatek.hu/sportfogadas"
- Link 2: "https://tipsport.hu/sport"

### Generált JSON:
```json
{
  "bookmaker1": "Szerencsejáték",
  "bookmaker2": "Tipsport",
  "link1": "https://szerencsejatek.hu/sportfogadas",
  "link2": "https://tipsport.hu/sport"
}
```

### Base64URL kódolás után:
```
eyJib29rbWFrZXIxIjoiU3plcmVuY3NlasOha3RlayIsImJvb2ttYWtlcjIiOiJUaXBzcG9ydCIsImxpbmsxIjoiaHR0cHM6Ly9zemVyZW5jc2VqYXRlay5odS9zcG9ydGZvZ2FkYXMiLCJsaW5rMiI6Imh0dHBzOi8vdGlwc3BvcnQuaHUvc3BvcnQifQ
```

### Végső link (alap / basic):
```
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiU3plcmVuY3NlasOha3RlayIsImJvb2ttYWtlcjIiOiJUaXBzcG9ydCIsImxpbmsxIjoiaHR0cHM6Ly9zemVyZW5jc2VqYXRlay5odS9zcG9ydGZvZ2FkYXMiLCJsaW5rMiI6Imh0dHBzOi8vdGlwc3BvcnQuaHUvc3BvcnQifQ
```

### Végső link (PWA támogatással / with PWA support):
```
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiU3plcmVuY3NlasOha3RlayIsImJvb2ttYWtlcjIiOiJUaXBzcG9ydCIsImxpbmsxIjoiaHR0cHM6Ly9zemVyZW5jc2VqYXRlay5odS9zcG9ydGZvZ2FkYXMiLCJsaW5rMiI6Imh0dHBzOi8vdGlwc3BvcnQuaHUvc3BvcnQifQ&PWA=true
```

## Fontos megjegyzések / Important Notes

1. **Mindkét link kötelező** / Both links are required
   - Ha bármelyik hiányzik, a gomb letiltva marad
   - If either is missing, the button stays disabled

2. **URL validáció** / URL Validation
   - Csak http:// vagy https:// protokollal kezdődő URL-ek engedélyezettek
   - Only URLs starting with http:// or https:// are allowed

3. **Bookmaker nevek opcionálisak** / Bookmaker names are optional
   - Ha megadod, megjelennek az oldalon
   - If provided, they will be displayed on the page

4. **PWA flag használata** / PWA flag usage
   - Csak akkor add hozzá, ha biztosan PWA környezetből nyílik meg
   - Only add if you're certain it will open from a PWA environment
   - Felesleges használata zavaró lehet desktop böngészőben
   - Unnecessary use can be confusing in desktop browsers

## Hibaelhárítás / Troubleshooting

### A gomb inaktív marad / Button stays disabled:
- Ellenőrizd, hogy mindkét link érvényes URL-e
- Ellenőrizd a base64url kódolást
- Check that both links are valid URLs
- Check the base64url encoding

### A banner nem jelenik meg / Banner doesn't appear:
- Ellenőrizd, hogy a PWA=true paraméter szerepel-e a hash fragmentben
- Check that the PWA=true parameter is in the hash fragment

### Dekódolási hiba / Decoding error:
- Győződj meg róla, hogy a JSON érvényes
- Ellenőrizd a base64url konverziót (-, _ karakterek, nincs =)
- Make sure the JSON is valid
- Check the base64url conversion (-, _ characters, no =)

## Online eszközök / Online Tools

Teszteléshez használhatsz online base64 kódolókat, de ne felejtsd el a base64url konverziót:
- `+` → `-`
- `/` → `_`
- Távolítsd el a záró `=` jeleket

For testing, you can use online base64 encoders, but don't forget the base64url conversion:
- `+` → `-`
- `/` → `_`
- Remove trailing `=` signs
