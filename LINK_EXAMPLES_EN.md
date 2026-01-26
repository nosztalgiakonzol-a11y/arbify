# Link Examples - Arbify

This file contains real, working examples of Arbify links.

---

## EXAMPLE 1: Dual Link (Open Simultaneously button)

### Input:
```json
{
  "bookmaker1": "Bet365",
  "link1": "https://www.bet365.com",
  "bookmaker2": "Unibet",
  "link2": "https://www.unibet.com"
}
```

### Encoding steps:

**1. JSON string:**
```
{"bookmaker1":"Bet365","link1":"https://www.bet365.com","bookmaker2":"Unibet","link2":"https://www.unibet.com"}
```

**2. Base64 encoding:**
```
eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

**3. Base64URL (replace + and /, remove = padding):**
```
eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

### Final links:

**Basic version:**
```
https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

**With PWA flag (for mobile PWA view):**
```
https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9&PWA=true
```

---

## EXAMPLE 2: Instant Redirect - Simple URL

### Input:
```
Target URL: https://www.bet365.com/sport/football
```

### Three methods:

**A) Simple version (if no special characters):**
```
https://arbify-bet.hu/#g=https://www.bet365.com/sport/football
```

**B) URL-encoded version:**

After URL encoding:
```
https%3A%2F%2Fwww.bet365.com%2Fsport%2Ffootball
```

Final link:
```
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fsport%2Ffootball
```

**C) Base64URL-encoded version (NEW, recommended):**

After Base64URL encoding:
```
aHR0cHM6Ly93d3cuYmV0MzY1LmNvbS9zcG9ydC9mb290YmFsbA
```

Final link:
```
https://arbify-bet.hu/#g=aHR0cHM6Ly93d3cuYmV0MzY1LmNvbS9zcG9ydC9mb290YmFsbA
```

---

## EXAMPLE 3: Instant Redirect - Complex URL with parameters

### Input:
```
Target URL: https://www.unibet.com/betting/sports/event/12345?market=1x2&odds=2.5
```

### Two recommended methods for complex URLs:

**A) URL-encoded version:**
```
https%3A%2F%2Fwww.unibet.com%2Fbetting%2Fsports%2Fevent%2F12345%3Fmarket%3D1x2%26odds%3D2.5
```

Final link:
```
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.unibet.com%2Fbetting%2Fsports%2Fevent%2F12345%3Fmarket%3D1x2%26odds%3D2.5
```

**B) Base64URL-encoded version (NEW, recommended):**
```
aHR0cHM6Ly93d3cudW5pYmV0LmNvbS9iZXR0aW5nL3Nwb3J0cy9ldmVudC8xMjM0NT9tYXJrZXQ9MXgyJm9kZHM9Mi41
```

Final link:
```
https://arbify-bet.hu/#g=aHR0cHM6Ly93d3cudW5pYmV0LmNvbS9iZXR0aW5nL3Nwb3J0cy9ldmVudC8xMjM0NT9tYXJrZXQ9MXgyJm9kZHM9Mi41
```

---

## EXAMPLE 4: Multiple bookmaker examples

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

## EXAMPLE 5: Calculator betting button

If you want to direct users to a specific event in the calculator:

### Event-specific link:
```
Target: https://www.bet365.com/matches/12345/bet?selection=home_win

URL-encoded:
https%3A%2F%2Fwww.bet365.com%2Fmatches%2F12345%2Fbet%3Fselection%3Dhome_win

Final link:
https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fmatches%2F12345%2Fbet%3Fselection%3Dhome_win
```

---

## Summary table

| Type | Parameter | Example link |
|------|-----------|--------------|
| **Dual link** | `#p=BASE64URL` | `https://arbify-bet.hu/#p=eyJib29rbWFr...` |
| **Dual link PWA** | `#p=BASE64URL&PWA=true` | `https://arbify-bet.hu/#p=eyJib29rbWFr...&PWA=true` |
| **Instant redirect simple** | `#g=URL` | `https://arbify-bet.hu/#g=https://bet365.com` |
| **Instant redirect URL-encoded** | `#g=ENCODED_URL` | `https://arbify-bet.hu/#g=https%3A%2F%2Fbet365.com` |
| **Instant redirect Base64URL** | `#g=BASE64URL` | `https://arbify-bet.hu/#g=aHR0cHM6Ly93d3cuYmV0MzY1LmNvbQ` |

---

## Quick testing

These links work immediately, you can try them:

1. **Bet365 instant redirect (simple):**
   ```
   https://arbify-bet.hu/#g=https://www.bet365.com
   ```

2. **Bet365 instant redirect (Base64URL, NEW):**
   ```
   https://arbify-bet.hu/#g=aHR0cHM6Ly93d3cuYmV0MzY1LmNvbQ
   ```

3. **Dual link (Bet365 + Unibet):**
   ```
   https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
   ```

4. **Complex URL (Base64URL, NEW):**
   ```
   https://arbify-bet.hu/#g=aHR0cHM6Ly93d3cudW5pYmV0LmNvbS9iZXR0aW5nL3Nwb3J0cy9ldmVudC8xMjM0NT9tYXJrZXQ9MXgyJm9kZHM9Mi41
   ```

---

## JavaScript code example

```javascript
// Generate dual link
function generateDualLink(bookmaker1, link1, bookmaker2, link2, isPWA = false) {
  const data = { bookmaker1, link1, bookmaker2, link2 };
  const json = JSON.stringify(data);
  const base64 = btoa(json).replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');
  return `https://arbify-bet.hu/#p=${base64}${isPWA ? '&PWA=true' : ''}`;
}

// Generate instant redirect - URL-encoded
function generateInstantRedirect(targetUrl) {
  const encoded = encodeURIComponent(targetUrl);
  return `https://arbify-bet.hu/#g=${encoded}`;
}

// Generate instant redirect - Base64URL-encoded (NEW, recommended)
function generateInstantRedirectBase64(targetUrl) {
  const base64 = btoa(targetUrl).replace(/\+/g, '-').replace(/\//g, '_').replace(/=/g, '');
  return `https://arbify-bet.hu/#g=${base64}`;
}

// Usage:
const dualLink = generateDualLink("Bet365", "https://www.bet365.com", "Unibet", "https://www.unibet.com");
const redirectLink = generateInstantRedirect("https://www.bet365.com/sport/football");
const redirectLinkBase64 = generateInstantRedirectBase64("https://www.bet365.com/sport/football");

console.log(dualLink);
console.log(redirectLink);
console.log(redirectLinkBase64);
```
