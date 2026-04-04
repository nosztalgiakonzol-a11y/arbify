# Lovable AI - Link Generation Guide

## Overview

This guide explains how to generate links for the Arbify application. There are two main types of links:

1. **Dual Link Mode** - For the "Open Simultaneously" button
2. **Instant Redirect** - For bookmaker buttons and calculator betting buttons

---

## 1. Dual Link Mode - "Open Simultaneously" Button

### When to use:
When the user wants to open two bookmakers simultaneously.

### Link format:
```
https://arbify-bet.hu/#p=<BASE64URL_JSON>&PWA=true
```

### Steps to generate the link:

#### Step 1: Create the JSON object
```javascript
const data = {
  "bookmaker1": "First Bookmaker Name",    // First bookmaker name
  "link1": "https://bookmaker1.com",       // First link
  "bookmaker2": "Second Bookmaker Name",   // Second bookmaker name
  "link2": "https://bookmaker2.com"        // Second link
};
```

#### Step 2: Encode to Base64URL format
```javascript
// Convert to JSON string
const jsonString = JSON.stringify(data);

// Base64 encoding
const base64 = btoa(jsonString);

// Base64URL conversion (replace + and / characters, remove padding)
const base64url = base64
  .replace(/\+/g, '-')
  .replace(/\//g, '_')
  .replace(/=/g, '');
```

#### Step 3: Build the link
```javascript
// Base link
let link = `https://arbify-bet.hu/#p=${base64url}`;

// If viewing from phone in PWA mode, add PWA=true parameter
if (isPWAView && isMobileDevice) {
  link += '&PWA=true';
}
```

### PWA Detection (optional):
```javascript
// Check if running in PWA mode
const isPWAView = window.matchMedia('(display-mode: standalone)').matches || 
                  window.navigator.standalone === true;

// Check if running on mobile device
const isMobileDevice = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
```

### Complete example:
```javascript
function generateDualLinkUrl(bookmaker1, link1, bookmaker2, link2) {
  // 1. Create JSON object
  const data = {
    bookmaker1: bookmaker1,
    link1: link1,
    bookmaker2: bookmaker2,
    link2: link2
  };
  
  // 2. Base64URL encoding
  const jsonString = JSON.stringify(data);
  const base64 = btoa(jsonString);
  const base64url = base64
    .replace(/\+/g, '-')
    .replace(/\//g, '_')
    .replace(/=/g, '');
  
  // 3. Build link
  let url = `https://arbify-bet.hu/#p=${base64url}`;
  
  // PWA detection
  const isPWAView = window.matchMedia('(display-mode: standalone)').matches || 
                    window.navigator.standalone === true;
  const isMobileDevice = /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent);
  
  if (isPWAView && isMobileDevice) {
    url += '&PWA=true';
  }
  
  return url;
}

// Usage:
const url = generateDualLinkUrl(
  "Bet365",
  "https://www.bet365.com",
  "Unibet",
  "https://www.unibet.com"
);
// Result: https://arbify-bet.hu/#p=eyJib29rbWFrZXIxIjoiQmV0MzY1IiwibGluazEiOiJodHRwczovL3d3dy5iZXQzNjUuY29tIiwiYm9va21ha2VyMiI6IlVuaWJldCIsImxpbmsyIjoiaHR0cHM6Ly93d3cudW5pYmV0LmNvbSJ9
```

---

## 2. Instant Redirect - Bookmaker Buttons and Calculator

### When to use:
- For bookmaker buttons (quick opening of a single bookmaker)
- For "Place Bet" button within calculator
- Anywhere instant redirect to a URL is needed

### Link format:
```
https://arbify-bet.hu/#g=<TARGET_URL>
```
or
```
https://arbify-bet.hu/?g=<TARGET_URL>
```

### Steps to generate the link:

#### Step 1: URL encoding (if needed)
```javascript
const targetUrl = "https://bookmaker.com/event?id=12345";

// URL encoding (optional but recommended for special characters)
const encodedUrl = encodeURIComponent(targetUrl);
```

#### Step 2: Build the link
```javascript
// Hash-based (recommended for GitHub Pages)
const link = `https://arbify-bet.hu/#g=${encodedUrl}`;

// or Query-based
const link = `https://arbify-bet.hu/?g=${encodedUrl}`;
```

### Simple example (without URL encoding):
```javascript
function generateInstantRedirectUrl(targetUrl) {
  // Simple version: if URL doesn't contain special characters
  return `https://arbify-bet.hu/#g=${targetUrl}`;
}

// Usage:
const url = generateInstantRedirectUrl("https://www.bet365.com");
// Result: https://arbify-bet.hu/#g=https://www.bet365.com
```

### Safe example (with URL encoding):
```javascript
function generateInstantRedirectUrl(targetUrl) {
  // Safe version: with URL encoding
  const encoded = encodeURIComponent(targetUrl);
  return `https://arbify-bet.hu/#g=${encoded}`;
}

// Usage with complex URL:
const url = generateInstantRedirectUrl("https://www.bet365.com/sport/inplay?affid=12345");
// Result: https://arbify-bet.hu/#g=https%3A%2F%2Fwww.bet365.com%2Fsport%2Finplay%3Faffid%3D12345
```

### Calculator button example:
```javascript
// In calculator, when user clicks "Place Bet" button
function createBetButton(bookmakerName, betUrl) {
  const button = document.createElement('button');
  button.textContent = `Bet on ${bookmakerName}`;
  
  // Generate instant redirect link
  const redirectUrl = `https://arbify-bet.hu/#g=${encodeURIComponent(betUrl)}`;
  
  button.onclick = function() {
    window.open(redirectUrl, '_blank');
  };
  
  return button;
}

// Usage:
const betButton = createBetButton(
  "Bet365",
  "https://www.bet365.com/match/12345/bet"
);
```

---

## Summary

### Dual link ("Open Simultaneously"):
```javascript
const url = `https://arbify-bet.hu/#p=${base64urlJSON}&PWA=true`;
```

### Instant redirect (bookmaker buttons, calculator):
```javascript
const url = `https://arbify-bet.hu/#g=${encodeURIComponent(targetUrl)}`;
```

### Key differences:

| Feature | Parameter | Format | Usage |
|---------|-----------|--------|-------|
| Dual link | `#p=` | Base64URL JSON | Two links simultaneously |
| Instant redirect | `#g=` | URL (encoded) | One link instant redirect |
| PWA flag | `&PWA=true` | Boolean | Mobile PWA view |

---

## Security Notes

- Arbify **only allows HTTP and HTTPS** protocols
- Blocks: `javascript:`, `data:`, `file:`, `ftp:`, etc.
- Automatic URL validation happens server-side
- No-referrer policy for all redirects
