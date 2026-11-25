# Bandhan Pictures: Launch Guide (bandhanpictures.com.np)

You have 3 files:

| File | What it is |
|---|---|
| `index.html` | The complete website (photos are inside it) |
| `Code.gs` | The backend. It saves everything to your Google Sheet and Drive and emails you |
| `LAUNCH-GUIDE.md` | This guide |

Total time: about 30 minutes, plus waiting for the domain.

---

## Step 1: Create the Google Sheet (2 minutes)

1. Go to https://sheets.google.com and press **Blank spreadsheet**.
2. Rename it **Bandhan Pictures Data**.

## Step 2: Add the backend (10 minutes)

1. In that sheet open **Extensions > Apps Script**.
2. Delete the sample code. Open `Code.gs`, copy everything, and paste it in.
3. Edit the three lines at the top:
   - `OWNER_EMAIL`: your email (you get a message for every new booking, order, message and review)
   - `ADMIN_PASSWORD`: a strong password for your admin login
   - `ROOT_FOLDER_ID`: already set to your BANDHAN PICTURES folder. Leave it.
4. Press **Save** (disk icon).
5. In the function dropdown choose **setup** and press **Run**. Google will ask you to allow access:
   Choose your account, press **Advanced**, then **Go to project (unsafe)**, then **Allow**.
   (The warning is normal for your own scripts.)
6. Press **Deploy > New deployment**.
   - Type (gear icon): **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Press **Deploy** and **copy the Web app URL**. It starts with `https://script.google.com/macros/s/...`

> If you change `Code.gs` later: **Deploy > Manage deployments > pencil icon > Version: New version > Deploy**. The URL stays the same.

## Step 3: Connect the website to the backend (2 minutes)

1. Open `index.html` in Notepad (or any text editor). Do not use Word.
2. Press Ctrl+F and search for `PASTE_YOUR_WEB_APP_URL_HERE`.
3. Replace it with the Web app URL from Step 2 (keep the quotes). Save.

## Step 4: Test it on your computer (3 minutes)

1. Double-click `index.html` to open it in Chrome.
2. Make a test booking. Check your Sheet: a **bookings** tab appears with the row, and you get an email.
3. Open the admin: triple-click the "(c) Bandhan Pictures" text at the very bottom of the page.
   Username `admin`, password = what you set in `ADMIN_PASSWORD`.
4. In admin, change a booking to Confirmed, upload a photo in **Hero & Photos**, and open Work Tracking. Open the Track work page and look up your test booking (reference + phone).

## Step 5: Put the website online (10 minutes)

Use any free static host. Easiest: **Netlify**.

1. Go to https://app.netlify.com/drop (create a free account).
2. Make a folder named `bandhan-site` and put only `index.html` inside.
3. Drag the folder onto the Netlify page. Your site is live at a `something.netlify.app` address.

(Cloudflare Pages and GitHub Pages work the same way.)

## Step 6: Your .com.np domain

1. Go to https://register.com.np and register `bandhanpictures.com.np`.
   - The .np domain registration is free.
   - Individuals need a citizenship certificate. Organizations need their company registration certificate.
   - Approval can take a working day or more.
2. In Netlify: **Domain management > Add a domain** and type `bandhanpictures.com.np`.
   Netlify shows the DNS records to add (an A record and a CNAME for `www`).
3. In the register.com.np DNS panel, add exactly those records. Wait up to a few hours.
4. Netlify then gives you a free HTTPS certificate.

---

## How your data is saved

| What | Where |
|---|---|
| Bookings, orders, messages, reviews, subscribers | Your Google Sheet (one tab for each) |
| Uploaded photos | Drive > BANDHAN PICTURES > Photos |
| Site content (packages, products, blog, settings, films, team) | `content.json` in your BANDHAN PICTURES folder |
| Staff accounts | Private inside the Apps Script (passwords are scrambled) |
| Every new booking/order/message/review | Email to `OWNER_EMAIL` |

**Backup tip:** in Google Sheets use File > Make a copy now and then, and copy the BANDHAN PICTURES folder.

## Things to know

- **Admin password and staff:** the owner password you put in `Code.gs` can be changed from admin > Settings. Staff are made in admin > Staff & Access.
- **Client tracking is live:** when you change a stage, clients see it immediately.
- **Photos:** upload from admin (they are saved to Drive and shown on the site). Photos over about 5 MB are shrunk automatically.
- **Videos:** use video links (YouTube, Instagram). Video file upload is not included in this version.
- **Limits of free Google:** about 100 emails a day. Plenty for a studio.
- **If the website cannot reach Google** (no internet), the customer's booking is kept on their device and sent next time they open the site.
- **Changing the logo, colors, or text** inside the code: ask Claude and give it `index.html`.
- **Do not share** your Apps Script web address in public posts; it is only used by the website.
