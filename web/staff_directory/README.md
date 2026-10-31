# Staff Directory

- **Category:** Web 2.0
- **Points:** 70
- **Status:** Attempted / Exploitation Analysis
- **Artifacts:** `page.html`

---

## 1. Challenge Overview

An internal employee lookup portal styled as the "E Corp Intranet" (`page.html`). The interface presents a minimalist authentication gateway that transitions into an employee ID lookup panel.

## 2. Source Code & API Endpoint Analysis (`page.html`)

Auditing the client-side JavaScript reveals the underlying REST API architecture:

```javascript
// Authentication Endpoint
const r = await fetch('/api/login', {
  method: 'POST', 
  headers: {'Content-Type':'application/json'},
  body: JSON.stringify({ username, password })
});

// Admin Dashboard Hook
if (document.getElementById('u').value === 'admin') {
  const r2 = await fetch('/api/admin/dashboard');
  ...
}

// Insecure Employee Record Lookup
async function lookup() {
  const id = document.getElementById('lookupId').value;
  const r = await fetch('/api/employee/' + encodeURIComponent(id));
  document.getElementById('dirOut').textContent = JSON.stringify(await r.json(), null, 2);
}
```

## 3. Vulnerability Vectors

1. **Insecure Direct Object References (IDOR):** The `/api/employee/{id}` endpoint permits arbitrary numeric identifiers without ownership validation or role checks.
2. **Broken Authentication / NoSQL / SQL Injection:** The `/api/login` payload accepts JSON input, enabling potential SQL/NoSQL authentication bypass payloads (e.g. `{"username": {"$ne": ""}, "password": {"$ne": ""}}`).
3. **Broken Object Level Authorization (BOLA):** Requesting privileged IDs (`0`, `1`, `admin`) discloses restricted management dossiers and flags.
