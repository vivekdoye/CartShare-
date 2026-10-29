# CartShare-
# CartShare – Collaborative Shopping Ecosystem 🛒

> **Shop Together. Save Together.**
> A front-end only collaborative shopping platform built with **HTML5, CSS3, JavaScript, Bootstrap 5, Bootstrap Icons, LocalStorage & the browser `storage` event**.

---

## 1. About the Project

CartShare lets a group of people share **one shopping cart** in real time.
Create a room, share the generated code (`CS-7X42`), and everyone can add / remove items,
change quantities and watch a **live activity log**. When the group is done, CartShare
generates a clean, **printable group receipt** with participants, delivery fee, discount and grand total.

**No backend / no database is used** — all data is persisted in the browser with `localStorage`,
and multiple browser tabs act as multiple users through `window.addEventListener("storage", …)`.

---
Project Link :-https://vivekdoye.github.io/CartShare-/

## 2. Folder Structure

```
CartShare/
│
├── index.html          # Application shell + all views (hash routes) – THIS is the runnable file
├── login.html          # → opens index.html with route #/login
├── create-room.html    # → #/create
├── join-room.html      # → #/join
├── dashboard.html      # → #/dashboard
├── receipt.html        # → #/receipt
│
├── css/
│   └── style.css       # Theme (Electric Blue + Black + White). Inlined in index.html <style>
│
├── js/
│   ├── auth.js         # Login + user session
│   ├── room.js         # Create room, room-code generator, join/validation
│   ├── cart.js         # Add / remove / change quantity + automatic totals
│   ├── activity.js     # Live activity log (newest first)
│   └── receipt.js      # Receipt generation + printing
│
├── assets/
│   ├── logo.png        # Logo is drawn with CSS + Bootstrap Icons (no broken image links)
│   └── images/         # Hero / empty-state images (served from a reliable stock CDN)
│
└── README.md
```

> **Note:** to keep the project runnable with a simple double-click (no local server,
> no CORS issues), every page is implemented as a **hash route** inside `index.html`:
> `#/home  #/login  #/create  #/join  #/dashboard  #/receipt  #/about`.
> Each section of the JavaScript in `index.html` is labelled with the matching file name
> (`auth.js`, `room.js`, `cart.js`, `activity.js`, `receipt.js`) so it maps 1:1 to the folder structure above.

---

## 3. How to Run

1. Download / open the project folder.
2. Double-click **index.html** (works in Chrome, Edge, Firefox, Safari).
3. Optional but recommended: open **two browser tabs** of the same page —
   that is how the multi-user collaboration is demonstrated.

---

## 4. Feature Checklist (all functional)

| Feature | Where / How it works |
|---|---|
| Login | `#/login` – name + email saved in `localStorage` (`cs_user_v1`) |
| Welcome banner | “Welcome, [Name] 👋” in navbar, hero and login page |
| Create Room | `#/create` – random unique code `CS-XXXX` (no 0/O/1/I confusion) |
| Copy Room Code | Clipboard API with `document.execCommand` fallback + toast |
| Join Room | `#/join` – validates the code: *“Successfully joined CartShare Room!”* / *“Room not found…”* |
| Add Item | Item name + auto-suggest, quantity, price, added-by |
| Remove Item | Trash button in the Action column |
| Change Quantity | `– / +` stepper (minimum 1, logs `5 → 6`) |
| Automatic Totals | `computeTotals()` → subtotal, delivery, discount, grand total, per-person share |
| Free Delivery Progress | `₹650 / ₹1000 · ₹350 more for free delivery!`, ₹1000 ⇒ delivery ₹0 |
| Promo Code | `CARTSHARE10` (10%) / `SAVE15` (15%) → discount line |
| LocalStorage Persistence | Rooms, items, activity, user, active room |
| Tab Synchronization | `window.addEventListener('storage', …)` re-renders cart, totals, activity & participants |
| Activity Log | Newest first, colour-coded dots (blue = add, green = update, red = remove, purple = room/join) |
| Receipt | `#/receipt` – room details, items, subtotal, delivery, discount, grand total, participants |
| Print Receipt | `@media print` hides navbar, buttons, activity log, toasts — only the receipt prints |
| Toasts / Loader / Empty Cart | Custom notifications, spinner overlay, illustrated empty-cart state |
| Responsive | Bootstrap grid: cart + activity side-by-side on desktop, stacked on mobile |

---

## 5. Viva Demo Script (60 seconds)

1. **Login** as *Vivek* → “Welcome, Vivek 👋” appears.
2. **Create Room** → name *Weekend Grocery* → code like **CS-7X42** is generated → **Copy Room Code**.
3. Click **Open Dashboard** (or **Load Demo Room**).
4. Press the **new-tab icon** → the same room opens in a second tab → add *“Milk”*
   → the first tab updates instantly (cart, totals, activity log) — this is the **storage-event** collaboration.
5. Change a quantity with `+ / –`, remove an item, watch the **Live Activity** feed.
6. Apply promo `CARTSHARE10` → discount appears and grand total recalculates.
7. Press **Generate Receipt → Print Receipt** → only the receipt is printed.

---

## 6. Key JavaScript Functions (for explanation)

| Function | Purpose |
|---|---|
`loadRooms()` / `saveRooms()` | Read/write the entire rooms object from `localStorage` (writing triggers the `storage` event in other tabs)
`mutateRoom(code, fn)` | Safe read → mutate → save of a single room
`generateRoomCode()` | Creates a guaranteed-unique `CS-XXXX` code
`createRoom()` / `joinRoom()` | Room creation and validated joining
`setActiveRoom()` / `activeRoom()` | Room of the current tab (`sessionStorage`) with `localStorage` fallback
`addItem()` / `removeItem()` / `changeQty()` | Cart operations with activity logging
`computeTotals(room)` | Single source of truth for subtotal, delivery, discount, grand total, progress
`pushActivity(room, text, type)` | Adds an entry to the live activity log (newest first)
`avatarFor(name)` | Deterministic initials + colour for every participant
`buildReceiptHTML(room)` | Builds the receipt used for both preview and printing
`printReceipt()` | Injects the receipt into `#printArea` and calls `window.print()`
`window.addEventListener('storage')` | Real-time multi-tab (multi-user) synchronisation

---

## 7. Project Description (for report / synopsis / PPT)

**One-line:** CartShare – Collaborative Shopping Ecosystem is a browser-based shopping platform that lets a group
create a shared room, build one common cart in real time and instantly generate a printable group receipt.

**Short (150 words):** CartShare is a responsive front-end web application built with HTML5, CSS3, JavaScript (ES6)
and Bootstrap 5 that allows a group of shoppers to collaborate on a single shopping cart. A user logs in with just a
name and email, creates or joins a room using a unique code such as `CS-7X42`, adds and removes items, changes
quantities and follows a live activity feed that records who added, updated or removed each product. Subtotal,
delivery fee, discount, free-delivery progress and grand total are calculated automatically, and a clean printable
receipt can be generated for the whole group. All data is persisted in the browser using LocalStorage, and multiple
browser tabs stay synchronised through the browser `storage` event, which simulates real-time multi-user
collaboration without any server or database.

**Keywords:** Collaborative shopping · Shared cart · Real-time tab synchronisation · LocalStorage · Bootstrap 5 ·
JavaScript ES6 · Dynamic billing calculation · Receipt generation · Responsive UI

> The full abstract, module-wise description, workflow table, storage design, advantages, limitations, future scope,
> conclusion and **viva Q&A** are available inside the application on the **Description page** (`#/description`),
> where every section has a one-click **Copy** button.

---

## 8. Tech Stack

HTML5 · CSS3 · JavaScript (ES6) · Bootstrap 5.3 · Bootstrap Icons · Google Fonts · LocalStorage · sessionStorage

---

*Generated by CartShare – Shop Together. Save Together.*
