# Arbify Quick Reference Card / Gyors Referencia Kártya

## Minimális példa / Minimal Example

```javascript
const data = {
  bookmaker1: "Name1", bookmaker2: "Name2",
  link1: "https://site1.com", link2: "https://site2.com"
};
const b64 = btoa(JSON.stringify(data)).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,'');
const url = `https://arbify.hu/#p=${b64}`;  // alap / basic
const urlPWA = `https://arbify.hu/#p=${b64}&PWA=true`;  // PWA
```

## URL Struktúra / URL Structure

```
https://arbify.hu/#p=<BASE64URL>&PWA=true
                    │            │
                    │            └─ Opcionális / Optional
                    └─ Kötelező / Required
```

## JSON Sablon / JSON Template

```json
{
  "bookmaker1": "string vagy empty / string or empty",
  "bookmaker2": "string vagy empty / string or empty", 
  "link1": "https://... KÖTELEZŐ / REQUIRED",
  "link2": "https://... KÖTELEZŐ / REQUIRED"
}
```

## Base64URL Konverzió / Base64URL Conversion

1. JSON → string: `JSON.stringify(data)`
2. String → base64: `btoa(jsonString)` vagy / or `Buffer.from(jsonString, 'utf8').toString('base64')`
3. Base64 → Base64URL:
   - `+` → `-`
   - `/` → `_`
   - Eltávolítani / Remove: `=`

## Példa Kimenet / Example Output

**Input:**
```json
{"bookmaker1":"Tippmix","bookmaker2":"BetSafe","link1":"https://tippmix.hu","link2":"https://betsafe.com"}
```

**Base64:**
```
eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUiLCJsaW5rMiI6Imh0dHBzOi8vYmV0c2FmZS5jb20ifQ==
```

**Base64URL** (remove `==`):
```
eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUiLCJsaW5rMiI6Imh0dHBzOi8vYmV0c2FmZS5jb20ifQ
```

**Final URL:**
```
https://arbify.hu/#p=eyJib29rbWFrZXIxIjoiVGlwcG1peCIsImJvb2ttYWtlcjIiOiJCZXRTYWZlIiwibGluazEiOiJodHRwczovL3RpcHBtaXguaHUiLCJsaW5rMiI6Imh0dHBzOi8vYmV0c2FmZS5jb20ifQ
```

## Gyakori Hibák / Common Errors

| ❌ Hibás / Wrong | ✅ Helyes / Correct |
|-----------------|-------------------|
| `"link1": "/path"` | `"link1": "https://site.com/path"` |
| `"link1": "site.com"` | `"link1": "https://site.com"` |
| `...Q==&PWA=true` | `...Q&PWA=true` |
| `?p=base64url` | `#p=base64url` |

## Nyelvspecifikus Példák / Language-specific Examples

### JavaScript/Node.js
```javascript
const data = {bookmaker1:"A",bookmaker2:"B",link1:"https://a.com",link2:"https://b.com"};
const b64url = btoa(JSON.stringify(data)).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,'');
console.log(`https://arbify.hu/#p=${b64url}`);
```

### Python
```python
import json, base64
data = {"bookmaker1":"A","bookmaker2":"B","link1":"https://a.com","link2":"https://b.com"}
b64url = base64.b64encode(json.dumps(data).encode()).decode().replace('+','-').replace('/','_').rstrip('=')
print(f"https://arbify.hu/#p={b64url}")
```

### PHP
```php
$data = ["bookmaker1"=>"A","bookmaker2"=>"B","link1"=>"https://a.com","link2"=>"https://b.com"];
$b64url = rtrim(strtr(base64_encode(json_encode($data)), '+/', '-_'), '=');
echo "https://arbify.hu/#p=$b64url";
```

### Ruby
```ruby
require 'json'
require 'base64'
data = {bookmaker1:"A",bookmaker2:"B",link1:"https://a.com",link2:"https://b.com"}
b64url = Base64.strict_encode64(data.to_json).tr('+/', '-_').gsub(/=+$/, '')
puts "https://arbify.hu/#p=#{b64url}"
```

### Go
```go
import ("encoding/json"; "encoding/base64"; "strings")
data := map[string]string{"bookmaker1":"A","bookmaker2":"B","link1":"https://a.com","link2":"https://b.com"}
j, _ := json.Marshal(data)
b64 := base64.StdEncoding.EncodeToString(j)
b64url := strings.TrimRight(strings.NewReplacer("+","-","/","_").Replace(b64), "=")
// https://arbify.hu/#p= + b64url
```

### C#
```csharp
using System; using System.Text; using Newtonsoft.Json;
var data = new {bookmaker1="A",bookmaker2="B",link1="https://a.com",link2="https://b.com"};
var json = JsonConvert.SerializeObject(data);
var b64 = Convert.ToBase64String(Encoding.UTF8.GetBytes(json));
var b64url = b64.Replace('+','-').Replace('/','_').TrimEnd('=');
Console.WriteLine($"https://arbify.hu/#p={b64url}");
```

### Java
```java
import java.util.*; import java.util.Base64; import com.google.gson.Gson;
Map<String,String> data = Map.of("bookmaker1","A","bookmaker2","B","link1","https://a.com","link2","https://b.com");
String json = new Gson().toJson(data);
String b64 = Base64.getEncoder().encodeToString(json.getBytes());
String b64url = b64.replace('+','-').replace('/','_').replaceAll("=+$","");
System.out.println("https://arbify.hu/#p=" + b64url);
```

## CLI Eszközök / CLI Tools

### Bash (Linux/Mac)
```bash
# Encode
echo -n '{"bookmaker1":"A","bookmaker2":"B","link1":"https://a.com","link2":"https://b.com"}' | \
  base64 | tr '+/' '-_' | tr -d '='

# Full URL
echo "https://arbify.hu/#p=$(echo -n '{"bookmaker1":"A","bookmaker2":"B","link1":"https://a.com","link2":"https://b.com"}' | base64 | tr '+/' '-_' | tr -d '=')"
```

### PowerShell (Windows)
```powershell
$json = '{"bookmaker1":"A","bookmaker2":"B","link1":"https://a.com","link2":"https://b.com"}'
$bytes = [System.Text.Encoding]::UTF8.GetBytes($json)
$b64 = [Convert]::ToBase64String($bytes)
$b64url = $b64.Replace('+','-').Replace('/','_').TrimEnd('=')
"https://arbify.hu/#p=$b64url"
```

## Tesztelés / Testing

1. Generálj linket / Generate link
2. Nyisd meg: [test.html](test.html)
3. Ellenőrizd a kimenetit / Verify output
4. Kattints a gombra / Click button
5. Ellenőrizd a működést / Verify functionality

## Ellenőrző Lista / Checklist

Mielőtt elküldesz egy linket / Before sending a link:

- [ ] Mindkét URL teljes (https://...)
- [ ] Both URLs are complete (https://...)
- [ ] JSON érvényes / JSON is valid
- [ ] Base64URL konverzió helyes (-, _)
- [ ] Base64URL conversion is correct (-, _)
- [ ] Nincs záró = jel / No trailing = signs
- [ ] PWA flag csak ha szükséges / PWA flag only if needed
- [ ] Link tesztelve / Link tested

## Hasznos Linkek / Useful Links

- 📖 [Részletes útmutató / Detailed guide](LINK_GENERATION_GUIDE.md)
- 🤖 [AI prompt sablon / AI prompt template](AI_PROMPT.md)
- 🧪 [Teszt oldal / Test page](test.html)
- 📝 [README](README.md)

---

**Tipp:** Mentsd el ezt a fájlt könyvjelzőkbe gyors hozzáféréshez!  
**Tip:** Bookmark this file for quick access!
