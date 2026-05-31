# Ecom API Testing with Postman & Newman

Automated API test suite for the [DummyJSON](https://dummyjson.com/) e-commerce API, built with **Postman** and executed via **Newman** (Postman's command-line runner). The project includes a **GitHub Actions CI/CD pipeline** that runs all API tests automatically on every push.

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Postman | API testing and collection building |
| Newman | Command-line collection runner |
| GitHub Actions | CI/CD — runs tests on every push |
| DummyJSON | Free e-commerce API used for testing |

---

## 📁 Project Structure

```
ecom-api-postman-tests/
│
├── .github/
│   └── workflows/
│       └── newman.yml        # GitHub Actions CI/CD workflow
│
├── collection.json           # Postman collection (exported)
├── environment.json          # Postman environment variables
└── README.md
```

---

## ✅ Test Coverage

| # | Method | Endpoint | Description |
|---|--------|----------|-------------|
| 1 | POST | `/auth/login` | Login and retrieve auth token |
| 2 | GET | `/auth/me` | Get authenticated user profile |
| 3 | GET | `/products` | Get all products |
| 4 | GET | `/products/27` | Get single product by ID |
| 5 | GET | `/recipes` | Get all recipes |
| 6 | GET | `/recipes/search?d=Margherita` | Search recipes by name |
| 7 | GET | `/recipes?sortBy=name&order=asc` | Sort recipes alphabetically |
| 8 | POST | `/recipes/add` | Add a new recipe |
| 9 | PUT | `/recipes/1` | Update an existing recipe |
| 10 | DELETE | `/recipes/1` | Delete a recipe |

---

## 🧪 Assertions

Each request includes test scripts to verify:
- ✅ Status code is 200
- ✅ Response body contains expected fields
- ✅ Response time is acceptable

---

## ⚙️ Environment Variables

| Variable | Description |
|----------|-------------|
| `base_url` | `https://dummyjson.com` |
| `token` | Auth token (set automatically after login) |
| `product_id` | Product ID used in requests |

---

## 🚀 Getting Started

### Prerequisites
- Node.js installed
- Newman installed globally

### Install Newman
```bash
npm install -g newman
```

### Run Collection Locally
```bash
newman run collection.json -e environment.json
```

### Expected Output
```
→ Login API          ✓ Status code is 200
→ Get user profile   ✓ Status code is 200
→ GET Products       ✓ Status code is 200
→ GET single product ✓ Status code is 200
→ GET recipes        ✓ Status code is 200
→ Search recipes     ✓ Status code is 200
→ Sort Recipes       ✓ Status code is 200
→ Add recipe         ✓ Status code is 200
→ Update Recipe      ✓ Status code is 200
→ recipe (DELETE)    ✓ Status code is 200

┌─────────────────────┬───────────────────┐
│                     │ executed │ failed │
├─────────────────────┼──────────┼────────┤
│ iterations          │        1 │      0 │
│ requests            │       10 │      0 │
│ test-scripts        │        8 │      0 │
│ assertions          │        8 │      0 │
└─────────────────────┴──────────┴────────┘
```

---

## 🔄 CI/CD — GitHub Actions

The workflow runs automatically on every push to `main`:

```yaml
name: Newman API Tests
on:
  push:
    branches: [ main ]
  workflow_dispatch:
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v4
    - name: Install Newman
      run: npm install -g newman
    - name: Run Postman Collection
      run: newman run collection.json -e environment.json
```

---

## 👤 Author

**Dipendra Niroula**
QA Intern | Postman · Newman · GitHub Actions · Playwright · Python
[LinkedIn](https://www.linkedin.com/in/) · [GitHub](https://github.com/DipendraNiroula)