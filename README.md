# ⚡ @net/ureq — Minimal Blocking HTTP Client for Zeta

**Port of the Rust `ureq` crate (v2.x). Synchronous HTTP/1.1 client.**
**No async runtime. No TLS yet. Just simple blocking requests.**

---

## 📦 Package

```
zorbs add @net/ureq
```

## 🔧 API

### One-Shot Requests

```zeta
// Simple GET
let resp = ureq::get("http://example.com/api/data");
let body = resp.body;  // Vec<u8>
let status = resp.status.code;

// Simple POST
let resp = ureq::post("http://api.example.com/submit", "hello world");
```

### Agent (shared configuration)

```zeta
let mut agent = Agent::new();
agent.set("User-Agent", "my-zeta-app/1.0");
agent.timeout_ms(10000);

let resp = agent.get("http://api.example.com/data").call();
let resp = agent.post("http://api.example.com/submit")
    .set("Content-Type", "application/json")
    .send_string("{\"key\": \"value\"}")
    .call();
```

### Response

```zeta
if resp.status.is_success() {
    let body_str = resp.body as str;
    let content_type = resp.headers.get("Content-Type");
}
```

## 📦 What's Inside

| Feature | Status |
|---|---|
| GET / POST / PUT / DELETE / PATCH / HEAD | ✅ |
| Custom headers | ✅ |
| Timeouts | ✅ |
| URL parsing | ✅ |
| Response parsing | ✅ |
| Chunked transfer | 🔜 |
| HTTPS/TLS | 🔜 (planned) |
| Connection pooling | 🔜 (planned) |
| Redirect following | 🔜 (planned) |
| Cookie support | 🔜 (planned) |

## 📄 License

MIT OR Apache-2.0
