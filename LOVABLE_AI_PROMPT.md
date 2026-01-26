# Lovable AI - Link Generation Útmutató

## Áttekintés

Ez az útmutató elmagyarázza, hogyan generálj linkeket az Arbify alkalmazáshoz. Két fő típusú link létezik:

1. **Dupla link mód** - "Megnyitás egyszerre" gomb számára
2. **Instant redirect** - Fogadóirodák gombjaihoz és kalkulátoron belüli fogadás gombhoz

---

## 1. Dupla Link Mód - "Megnyitás egyszerre" Gomb

### Mikor használd:
Amikor a felhasználó két fogadóirodát szeretne egyszerre megnyitni.

### Link formátum:
```
https://arbify-bet.hu/#p=<BASE64URL_JSON>&PWA=true
```

### Lépések a link generálásához:

#### 1. lépés: Hozd létre a JSON objektumot
```javascript
const data = {
  "bookmaker1": "Fogadóiroda 1 neve",    // Első fogadóiroda neve
  "link1": "https://fogadoiroda1.hu",    // Első link
  "bookmaker2": "Fogadóiroda 2 neve",    // Második fogadóiroda neve
  "link2": "https://fogadoiroda2.hu"     // Második link
};
```

#### 2. lépés: Kódold Base64URL formátumba
```javascript
// JSON stringgé alakítás
const jsonString = JSON.stringify(data);

// Base64 kódolás
const base64 = btoa(jsonString);

// Base64URL konverzió (+ és / karakterek cseréje, padding eltávolítása)
const base64url = base64
  .replace(/\+/g, '-')
  .replace(/\//g, '_')
  .replace(/=/g, '');
```

#### 3. lépés: Építsd fel a linket
```javascript
// Alap link
let link = `https://arbify-bet.hu/#p=${base64url}`;

// Ha telefonról nézi PWA nézetben, add hozzá a PWA=true paramétert
if (isPWAView && isMobileDevice) {
  link += '&PWA=true';
}
```

### PWA detektálás (opcionális):
```javascript
// Ellenőrizd, hogy PWA módban fut-e
const isPWAView = window.matchMedia('(display-mode: standalone)').matches || 
                  window.navigator.standalone === true;

// Ellenőrizd, hogy mobil eszközön fut-e
const isMobileDevice = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
```

### Teljes példa:
```javascript
function generateDualLinkUrl(bookmaker1, link1, bookmaker2, link2) {
  // 1. JSON objektum létrehozása
  const data = {
    bookmaker1: bookmaker1,
    link1: link1,
    bookmaker2: bookmaker2,
    link2: link2
  };
  
  // 2. Base64URL kódolás
  const jsonString = JSON.stringify(data);
  const base64 = btoa(jsonString);
  const base64url = base64
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=/g, '');
  
  // 3. Link építése
  let url = `https://arbify-bet.hu/#p=${base64url}`;
  
  // PWA detektálás
  const isPWAView = window.matchMedia('(display-mode: standalone)').matches || 
                    window.navigator.standalone === true;
  const isMobileDevice = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
  
  if (isPWAView && isMobileDevice) {
    url += '&PWA=true';
  }
  
  return url;
}

// Használat:
const url = generateDualLinkUrl(
  "Bet365",
  "https://www.bet365.com",
  "Unibet",
  "https://www.unibet.com"
);
// Eredmény: https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

---

## 2. Instant Redirect - Fogadóiroda Gombok és Kalkulátor

### Mikor használd:
- Fogadóiroda gombokhoz (egyetlen fogadóiroda gyors megnyitása)
- Kalkulátoron belüli "Fogadás" gombhoz
- Bármely helyhez, ahol azonnali átirányítás szükséges egy URL-re

### Link formátum:
```
https://arbify-bet.hu/#g=<TARGET_URL>
```
vagy
```
https://arbify-bet.hu/?g=<TARGET_URL>
```

### Lépések a link generálásához:

#### 1. lépés: URL enkódolás (ha szükséges)
```javascript
const targetUrl = "https://fogadoiroda.hu/esemeny?id=12345";

// URL enkódolás (opcionális, de ajánlott különleges karakterek esetén)
const encodedUrl = encodeURIComponent(targetUrl);
```

#### 2. lépés: Link építése
```javascript
// Hash alapú (ajánlott GitHub Pages-hez)
const link = `https://arbify-bet.hu/#g=${encodedUrl}`;

// vagy Query alapú
const link = `https://arbify-bet.hu/?g=${encodedUrl}`;
```

### Egyszerű példa (URL enkódolás nélkül):
```javascript
function generateInstantRedirectUrl(targetUrl) {
  // Egyszerű verzió: ha az URL nem tartalmaz különleges karaktereket
  return `https://arbify-bet.hu/#g=${targetUrl}`;
}

// Használat:
const url = generateInstantRedirectUrl("https://www.bet365.com");
// Eredmény: https://arbify-bet.hu/#g=https://www.bet365.com
```

### Biztonságos példa (URL enkódolással):
```javascript
function generateInstantRedirectUrl(targetUrl) {
  // Biztonságos verzió: URL enkódolással
  const encoded = encodeURIComponent(targetUrl);
  return `https://arbify-bet.hu/#g=${encoded}`;
}

// Használat komplex URL-lel:
const url = generateInstantRedirectUrl("https://www.bet365.com/sport/inplay?affid=12345");
// Eredmény: https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fsport%2Finplay%3Faffid%3D12345
```

### Kalkulátor gombok példa:
```javascript
// Kalkulátorban, amikor a felhasználó kattint a "Fogadás" gombra
function createBetButton(bookmakerName, betUrl) {
  const button = document.createElement('button');
  button.textContent = `Fogadás ${bookmakerName}`;
  
  // Instant redirect link generálása
  const redirectUrl = `https://arbify-bet.hu/#g=${encodeURIComponent(betUrl)}`;
  
  button.onclick = function() {
    window.open(redirectUrl, '_blank');
  };
  
  return button;
}

// Használat:
const betButton = createBetButton(
  "Bet365",
  "https://www.bet365.com/match/12345/bet"
);
```

---

## Összefoglalás

### Dupla link ("Megnyitás egyszerre"):
```javascript
const url = `https://arbify-bet.hu/#p=${base64urlJSON}&PWA=true`;
```

### Instant redirect (fogadóiroda gombok, kalkulátor):
```javascript
const url = `https://arbify-bet.hu/#g=${encodeURIComponent(targetUrl)}`;
```

### Kulcs különbségek:

| Funkció | Paraméter | Formátum | Használat |
|---------|-----------|----------|-----------|
| Dupla link | `#p=` | Base64URL JSON | Két link egyszerre |
| Instant redirect | `#g=` | URL (enkódolt) | Egy link azonnali átirányítás |
| PWA flag | `&PWA=true` | Boolean | Mobilon PWA nézetben |

---

## Biztonsági megjegyzések

- Az Arbify **csak HTTP és HTTPS** protokollokat engedélyez
- Blokkolja: `javascript:`, `data:`, `file:`, `ftp:` stb.
- Automatikus URL validáció történik szerver oldalon
- No-referrer politika minden átirányításnál
