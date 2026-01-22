# Prompt Lovable AI számára - Arbify Link Generálás
# Prompt for Lovable AI - Arbify Link Generation

## Magyar verzió

```
Kérlek generálj egy arbify.hu linket a következő specifikáció alapján:

BEMENET:
- Fogadóiroda 1 neve: [IDE ÍRD A NEVET]
- Fogadóiroda 2 neve: [IDE ÍRD A NEVET]
- Link 1 (első URL): [IDE ÍRD A TELJES URL-T]
- Link 2 (második URL): [IDE ÍRD A TELJES URL-T]
- PWA környezet: [IGEN/NEM - írj "IGEN"-t ha mobil PWA appból nyílik meg]

FELADAT:
1. Hozz létre egy JSON objektumot:
   {
     "bookmaker1": "első fogadóiroda neve",
     "bookmaker2": "második fogadóiroda neve", 
     "link1": "első teljes URL https://...",
     "link2": "második teljes URL https://..."
   }

2. Konvertáld ezt base64url formátumba:
   - JSON → base64 kódolás
   - Cseréld: + karaktert - -re
   - Cseréld: / karaktert _ -ra  
   - Távolítsd el: záró = jeleket

3. Építs fel egy linket:
   Alap: https://arbify.hu/#p=<BASE64URL>
   Ha PWA=IGEN: https://arbify.hu/#p=<BASE64URL>&PWA=true

PÉLDA:
Bemenet:
- Fogadóiroda 1: Tippmix
- Fogadóiroda 2: BetSafe
- Link 1: https://tippmix.hu/fogadas
- Link 2: https://betsafe.com/bet
- PWA: IGEN

Eredmény:
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUvZm9nYWRhcyIsImxpbmsyIjoiaHR0cHM6Ly9iZXRzYWZlLmNvbS9iZXQifQ&PWA=true

Kérlek generáld le a linket a fenti bemenet alapján.
```

## English Version

```
Please generate an arbify.hu link based on the following specification:

INPUT:
- Bookmaker 1 name: [ENTER NAME HERE]
- Bookmaker 2 name: [ENTER NAME HERE]
- Link 1 (first URL): [ENTER FULL URL HERE]
- Link 2 (second URL): [ENTER FULL URL HERE]
- PWA environment: [YES/NO - write "YES" if opening from mobile PWA app]

TASK:
1. Create a JSON object:
   {
     "bookmaker1": "first bookmaker name",
     "bookmaker2": "second bookmaker name",
     "link1": "first full URL https://...",
     "link2": "second full URL https://..."
   }

2. Convert this to base64url format:
   - JSON → base64 encoding
   - Replace: + character with -
   - Replace: / character with _
   - Remove: trailing = signs

3. Build a link:
   Basic: https://arbify.hu/#p=<BASE64URL>
   If PWA=YES: https://arbify.hu/#p=<BASE64URL>&PWA=true

EXAMPLE:
Input:
- Bookmaker 1: Tippmix
- Bookmaker 2: BetSafe
- Link 1: https://tippmix.hu/fogadas
- Link 2: https://betsafe.com/bet
- PWA: YES

Result:
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUvZm9nYWRhcyIsImxpbmsyIjoiaHR0cHM6Ly9iZXRzYWZlLmNvbS9iZXQifQ&PWA=true

Please generate the link based on the input above.
```

## Gyors referencia / Quick Reference

### Kódolási kód / Encoding Code

**JavaScript:**
```javascript
const data = {
  bookmaker1: "Név1", bookmaker2: "Név2",
  link1: "https://...", link2: "https://..."
};
const b64url = btoa(JSON.stringify(data))
  .replace(/\+/g, '-').replace(/\//g, '_').replace(/=+$/, '');
const link = `https://arbify.hu/#p=${b64url}` + (isPWA ? '&PWA=true' : '');
```

**Python:**
```python
import json, base64
data = {"bookmaker1": "Név1", "bookmaker2": "Név2",
        "link1": "https://...", "link2": "https://..."}
b64url = base64.b64encode(json.dumps(data).encode()).decode()
b64url = b64url.replace('+', '-').replace('/', '_').rstrip('=')
link = f"https://arbify.hu/#p={b64url}" + ("&PWA=true" if is_pwa else "")
```

## Fontos szabályok / Important Rules

✅ **MINDIG** használj teljes URL-t (https://...)
✅ **ALWAYS** use full URLs (https://...)

✅ **MINDKÉT** link kötelező
✅ **BOTH** links are required

✅ **PWA=true** CSAK mobil PWA környezetben
✅ **PWA=true** ONLY in mobile PWA environment

✅ Base64url NEM egyenlő base64 (-, _ karakterek!)
✅ Base64url is NOT the same as base64 (-, _ characters!)

❌ NE használj részleges URL-t (/path/to/page)
❌ DO NOT use partial URLs (/path/to/page)

❌ NE hagyd el egyik linket sem
❌ DO NOT omit any link
