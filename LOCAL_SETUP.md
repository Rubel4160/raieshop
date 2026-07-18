# RAIESHOP — Local (Windows CMD) Setup Guide

Ei guide follow kore tumi nijer PC te RAIESHOP chalu korte parba.

---

## Step 1: Node.js Install koro

1. Browser e jao: **https://nodejs.org**
2. **LTS** version ta download koro (Windows Installer `.msi`)
3. Install koro — sob "Next > Next > Finish" (kichu change korte hobe na)
4. Install sesh hole **CMD khulo** (Windows key → type `cmd` → Enter) ar check koro:

```cmd
node -v
npm -v
```

Version number dekha gele Node thikmoto install hoyeche (v20+ lagbe).

---

## Step 2: Project Folder Ready koro

1. `raieshop-source.zip` extract koro (Right click → "Extract All")
2. Extracted folder e jao
3. **Address bar e click kore `cmd` lekho → Enter** — oi folder e CMD khulbe
   (ba manually: `cd C:\Users\YourName\Downloads\raieshop-source`)

---

## Step 3: Database Setup (2 ta option — jekono ekta)

### Option A (EASY — Recommended): Neon Free Cloud Database

1. Jao: **https://neon.tech** → "Sign Up" (Google/GitHub diye login)
2. **"Create Project"** → name daw `raieshop` → Create
3. Dashboard e **"Connection string"** copy koro — emon dekhabe:
   ```
   postgresql://user:pass@ep-xxxx.aws.neon.tech/neondb?sslmode=require
   ```
4. Eta tomar `DATABASE_URL`

### Option B: Local PostgreSQL Install

1. Jao: **https://www.postgresql.org/download/windows/** → installer download
2. Install koro — superuser password ta **mone rekho** (jemon: `postgres`)
3. Start Menu → **SQL Shell (psql)** khulo → 4 bar Enter dao (connect hobe)
4. Eta run koro:
   ```sql
   CREATE DATABASE app_db;
   ```
5. Tomar `DATABASE_URL` hobe:
   ```
   postgresql://postgres:TOMAR_PASSWORD@localhost:5432/app_db
   ```

---

## Step 4: .env File Banao

Project folder e CMD te:

```cmd
notepad .env
```

"Create new file?" → **Yes** → ei 2 line paste koro (DATABASE_URL e tomar copy kora string daw):

```
DATABASE_URL=postgresql://user:pass@host/dbname?sslmode=require
ADMIN_PASSWORD=raieshop123
```

**Ctrl+S** → close Notepad.

---

## Step 5: Packages Install

CMD te (project folder ei thako):

```cmd
npm install
```

2–4 minute lagbe. Warning/audit message hole ignore koro.

---

## Step 6: Database Tables + Products Load

```cmd
npx drizzle-kit push
npx tsx src/db/seed.ts
```

✅ "Changes applied" ar "Seed complete: 16 products inserted" dekhle hoise.

---

## Step 7: Website Chalu Koro 🚀

```cmd
npm run dev
```

Ebar browser e jao:

- **Website:** http://localhost:3000
- **Admin Panel:** http://localhost:3000/admin → password: `raieshop123`

Bondho korte: CMD te **Ctrl+C** → `Y` → Enter.

---

## Production mode e chalate chaile (fast, live er moto):

```cmd
npm run build
npm run start
```

---

## Common Problems & Fixes

| Problem | Fix |
|---------|-----|
| `node is not recognized` | CMD bondho kore abar khulo (Node install er por) |
| `port 3000 is in use` | `npm run dev -- -p 3001` → localhost:3001 |
| drizzle-kit push error | `.env` er `DATABASE_URL` thik ache kina check koro |
| npm install error | `npm cache clean --force` kore abar try koro |
| Folder path e space thakle | `cd "C:\My Folder\raieshop-source"` quote diye daw |

---

## Website er sob Feature

- Home / Shop / Flash Sale / Product details — full ecommerce
- Cart + Wishlist (browser e save thake)
- Checkout → real order number (`RAI-XXXXXX-XXXXX`)
- Track Order (order number + phone)
- Customer account login/register
- Admin panel: products add/edit/delete, order status update, dashboard
- Contact: +8801825124160 (src/lib/site.ts e change kora jay)
