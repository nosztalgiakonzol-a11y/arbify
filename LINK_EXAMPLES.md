# Link Példák - Arbify

Ez a fájl valódi, működő példákat tartalmaz az Arbify linkjeire.

---

## PÉLDA 1: Dupla Link (Megnyitás egyszerre gomb)

### Bemenet:
```json
{
  "bookmaker1": "Bet365",
  "link1": "https://www.bet365.com",
  "bookmaker2": "Unibet",
  "link2": "https://www.unibet.com"
}
```

### Kódolási lépések:

**1. JSON string:**
```
{"bookmaker1":"Bet365","link1":"https://www.bet365.com","bookmaker2":"Unibet","link2":"https://www.unibet.com"}
```

**2. Base64 kódolás:**
```
eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

**3. Base64URL (+ és / cserélve, = padding eltávolítva):**
```
eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

### Végső linkek:

**Alap verzió:**
```
https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

**PWA flag-gel (telefonon PWA nézetben):**
```
https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9&PWA=true
```

---

## PÉLDA 2: Instant Redirect - Egyszerű URL

### Bemenet:
```
Cél URL: https://www.bet365.com/sport/football
```

### Két módszer:

**A) Egyszerű verzió (ha nincs különleges karakter):**
```
https://arbify-bet.hu/#g=https://www.bet365.com/sport/football
```

**B) URL-kódolt verzió (ajánlott):**

URL-kódolás után:
```
https%3A%2F%2Fwww.bet365.com%2Fsport%2Ffootball
```

Végső link:
```
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fsport%2Ffootball
```

---

## PÉLDA 3: Instant Redirect - Komplex URL paraméterekkel

### Bemenet:
```
Cél URL: https://www.unibet.com/betting/sports/event/12345?market=1x2&odds=2.5
```

### URL-kódolás (kötelező, mert vannak ? és & karakterek):

**URL-kódolt verzió:**
```
https%3A%2F%2Fwww.unibet.com%2Fbetting%2Fsports%2Fevent%2F12345%3Fmarket%3D1x2%26odds%3D2.5
```

**Végső link:**
```
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.unibet.com%2Fbetting%2Fsports%2Fevent%2F12345%3Fmarket%3D1x2%26odds%3D2.5
```

---

## PÉLDA 4: Több fogadóiroda példa

### Bet365:
```
https://arbify-bet.hu/#g=https://www.bet365.com
```

### Unibet:
```
https://arbify-bet.hu/#g=https://www.unibet.com
```

### 888sport:
```
https://arbify-bet.hu/#g=https://www.888sport.com
```

### Tipsport:
```
https://arbify-bet.hu/#g=https://www.tipsport.hu
```

---

## PÉLDA 5: Kalkulátor fogadás gomb

Ha a kalkulátorban egy konkrét eseményre akarod irányítani a felhasználót:

### Esemény specifikus link:
```
Cél: https://www.bet365.com/matches/12345/bet?selection=home_win

URL-kódolva:
https%3A%2F%2Fwww.bet365.com%2Fmatches%2F12345%2Fbet%3Fselection%3Dhome_win

Végső link:
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fmatches%2F12345%2Fbet%3Fselection%3Dhome_win
```

---

## Összefoglaló táblázat

| Típus | Paraméter | Példa link |
|-------|-----------|------------|
| **Dupla link** | `#p=BASE64URL` | `https://arbify-bet.hu/#p=eyJib29rbWFr...` |
| **Dupla link PWA** | `#p=BASE64URL&PWA=true` | `https://arbify-bet.hu/#p=eyJib29rbWFr...&PWA=true` |
| **Instant redirect egyszerű** | `#g=URL` | `https://arbify-bet.hu/#g=https://bet365.com` |
| **Instant redirect kódolt** | `#g=ENCODED_URL` | `https://arbify-bet.hu/#g=https%3A%2F%2Fbet365.com` |

---

## Gyors tesztelés

Ezek a linkek azonnal működnek, kipróbálhatod őket:

1. **Bet365 instant redirect:**
   ```
   https://arbify-bet.hu/#g=https://www.bet365.com
   ```

2. **Dupla link (Bet365 + Unibet):**
   ```
   https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
   ```

3. **Komplex URL példa:**
   ```
   https://arbify-bet.hu/#g=https%3A%2F%2Fwww.unibet.com%2Fbetting%2Fsports%2Fevent%2F12345%3Fmarket%3D1x2%26odds%3D2.5
   ```

---

## JavaScript kód példa

```javascript
// Dupla link generálás
function generateDualLink(bookmaker1, link1, bookmaker2, link2, isPWA = false) {
  const data = { bookmaker1, link1, bookmaker2, link2 };
  const json = JSON.stringify(data);
  const base64 = btoa(json).replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');
  return `https://arbify-bet.hu/#p=${base64}${isPWA ? '&PWA=true' : ''}`;
}

// Instant redirect generálás
function generateInstantRedirect(targetUrl) {
  const encoded = encodeURIComponent(targetUrl);
  return `https://arbify-bet.hu/#g=${encoded}`;
}

// Használat:
const dualLink = generateDualLink("Bet365", "https://www.bet365.com", "Unibet", "https://www.unibet.com");
const redirectLink = generateInstantRedirect("https://www.bet365.com/sport/football");

console.log(dualLink);
console.log(redirectLink);
```
