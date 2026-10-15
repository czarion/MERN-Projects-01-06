<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/banner-dark.svg" />
  <img src="docs/assets/banner-light.svg" alt="ShopKart: Less ordinary. More you. A real living-room photo from the storefront with floating wishlist, bag and order cards." width="100%" />
</picture>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-243e2e?style=flat-square&logo=react&logoColor=d9edac" alt="React 18" />
  <img src="https://img.shields.io/badge/Vite-6-243e2e?style=flat-square&logo=vite&logoColor=d9edac" alt="Vite 6" />
  <img src="https://img.shields.io/badge/Express-5-243e2e?style=flat-square&logo=express&logoColor=d9edac" alt="Express 5" />
  <img src="https://img.shields.io/badge/MongoDB-transactions-243e2e?style=flat-square&logo=mongodb&logoColor=d9edac" alt="MongoDB transactions" />
  <img src="https://img.shields.io/badge/Node-20.19%2B-243e2e?style=flat-square&logo=nodedotjs&logoColor=d9edac" alt="Node 20.19+" />
  <img src="https://img.shields.io/badge/Playwright-e2e-243e2e?style=flat-square&logo=playwright&logoColor=d9edac" alt="Playwright end-to-end tests" />
</p>

## 🖼️ A tour of the store

<table>
  <tr>
    <td width="50%"><img src="docs/assets/screens/home-light.webp" alt="Home page in light mode with the living-room hero" width="100%" /></td>
    <td width="50%"><img src="docs/assets/screens/home-dark.webp" alt="Home page in dark mode" width="100%" /></td>
  </tr>
  <tr>
    <td align="center"><sub><b>Home</b> · editorial hero and collections</sub></td>
    <td align="center"><sub><b>Dark mode</b> · remembered between visits</sub></td>
  </tr>
  <tr>
    <td><img src="docs/assets/screens/catalog-light.webp" alt="Collection page with category tabs, search, sorting and product cards" width="100%" /></td>
    <td><img src="docs/assets/screens/product.webp" alt="Product details for the Wireless Mechanical Keyboard, saved to wishlist" width="100%" /></td>
  </tr>
  <tr>
    <td align="center"><sub><b>Collection</b> · search, categories, sort, in-stock filter</sub></td>
    <td align="center"><sub><b>Product details</b> · stock, add to bag, save</sub></td>
  </tr>
  <tr>
    <td><img src="docs/assets/screens/wishlist.webp" alt="Wishlist with two saved products" width="100%" /></td>
    <td><img src="docs/assets/screens/cart.webp" alt="Shopping cart with quantity controls and total" width="100%" /></td>
  </tr>
  <tr>
    <td align="center"><sub><b>Wishlist</b> · heart to add or remove</sub></td>
    <td align="center"><sub><b>Bag</b> · quantities limited by stock</sub></td>
  </tr>
  <tr>
    <td><img src="docs/assets/screens/checkout.webp" alt="Checkout with shipping details and order summary" width="100%" /></td>
    <td><img src="docs/assets/screens/order.webp" alt="Order confirmation with status timeline and delivery address" width="100%" /></td>
  </tr>
  <tr>
    <td align="center"><sub><b>Checkout</b> · validated Indian address</sub></td>
    <td align="center"><sub><b>Order confirmed</b> · saved snapshot and timeline</sub></td>
  </tr>
</table>

<p align="center">
  <img src="docs/assets/screens/mobile-home-light.webp" alt="Home page on a phone" width="220" />
  &nbsp;
  <img src="docs/assets/screens/mobile-catalog-dark.webp" alt="Collection on a phone in dark mode" width="220" />
  &nbsp;
  <img src="docs/assets/screens/mobile-menu-light.webp" alt="Open mobile navigation menu" width="220" />
</p>
<p align="center"><sub><b>Mobile</b> · responsive layout, slide-down menu, no sideways scrolling</sub></p>

<details>
<summary><b>More screens</b> — sign up, order history, dark collection</summary>
<br />
<table>
  <tr>
    <td width="33%"><img src="docs/assets/screens/register.webp" alt="Create account page" width="100%" /></td>
    <td width="33%"><img src="docs/assets/screens/orders.webp" alt="Order history" width="100%" /></td>
    <td width="33%"><img src="docs/assets/screens/catalog-dark.webp" alt="Collection in dark mode" width="100%" /></td>
  </tr>
  <tr>
    <td align="center"><sub>Create account</sub></td>
    <td align="center"><sub>My orders</sub></td>
    <td align="center"><sub>Collection · dark</sub></td>
  </tr>
</table>
</details>

<sub>All screenshots are taken from the running app. Hero and collection photos are bundled in the frontend; catalog photos come from Unsplash with a local fallback image.</sub>

## ✨ What works

| | Area | What you get |
| :-: | --- | --- |
| 🏠 | **Storefront** | Public browsing, editorial hero, four linked collections, live featured products |
| 🔎 | **Discovery** | Debounced search, category tabs, price/name sort, in-stock filter, reset, shareable filter URLs |
| 👤 | **Accounts** | Validated sign-up, normalized email, bcrypt hashes, HttpOnly JWT cookie, return to the page you wanted |
| ❤️ | **Wishlist** | Add **and** remove from the heart anywhere, shared saved state, add to bag from the list |
| 🛍️ | **Bag** | Persistent cart, quantity controls, stock limits, exact INR totals, live navbar count |
| 💳 | **Checkout** | Indian address validation, server-calculated totals, free shipping, **COD** or **Razorpay Test Mode** |
| 📦 | **Orders** | Confirmation, history, ownership checks, purchase-time item snapshots, status timeline |
| 🧮 | **Inventory** | Order + stock + cart updated in **one MongoDB transaction** — no overselling the last unit |
| 🌗 | **Experience** | Light/dark theme, skeletons, toasts, helpful empty and error states, image fallback |
| ♿ | **Accessibility** | Landmarks, labeled controls, visible focus, skip link, live notifications, reduced-motion support |

## 🧭 How it works

```mermaid
flowchart LR
    UI["⚛️ React + Router + Context"] -->|"Axios · HttpOnly cookie"| API["🚂 Express API"]
    API --> DB[("🍃 MongoDB replica set")]
    API --> COD["💵 Cash on delivery"]
    API --> RP["💳 Razorpay Test Mode"]
    RP --> SIG["Verify payment signature"]
    COD --> TX["🔒 Transaction<br/>order + stock + cart"]
    SIG --> TX
    TX --> HIST["📦 Confirmation & history"]
```

<details>
<summary><b>What happens when you press “Place order”</b></summary>

```mermaid
sequenceDiagram
    autonumber
    actor C as Customer
    participant W as React app
    participant A as Express API
    participant M as MongoDB
    C->>W: Place order (COD)
    W->>A: POST /orders/cash-on-delivery + address
    A->>A: Validate session, origin and address
    A->>M: Start transaction
    A->>M: Re-read cart and prices, check stock
    A->>M: Create order with item snapshots
    A->>M: Decrease stock, remove purchased items from cart
    A->>M: Commit
    A-->>W: 201 Created + order id
    W-->>C: "Thank you for your order."
```

If two customers race for the last unit, only one transaction commits; the other gets a stock conflict and nothing is half-written.
</details>

**Stack**

| Layer | Tools |
| --- | --- |
| Frontend | React 18, React Router 7, Vite 6, Axios, Context API, lucide-react |
| Backend | Express 5, Mongoose 9, bcrypt, jsonwebtoken, cookie-parser, express-rate-limit, Razorpay SDK |
| Database | MongoDB replica set (local via `mongodb-memory-server`, or Atlas) |
| Testing | `node:test`, Supertest, nock, Playwright, GitHub Actions |

## 🧪 Tests

```bash
npm test          # API tests on an isolated MongoDB replica set
npm run build     # production build of every page

# with `npm run dev` running in another terminal:
cd Lab-03-ShopKart-Product-Discovery/frontend
npm run test:e2e  # Playwright browser journeys
```

- **6 API test groups** — wishlist/cart isolation, stock limits, mocked Razorpay verification and replay, input validation, unauthorized writes and origins, COD totals, duplicate checkout, and two buyers racing for the last unit.
- **2 browser journeys** — sign-up to sign-out with wishlist, bag, address validation, COD and order history; plus sorting, empty results, theme persistence and mobile navigation.
- **CI** runs setup, API tests, the build and both browser journeys on every push to `main`.

The browser tests use installed Google Chrome. Without it, run `npx playwright install chromium` and then `E2E_CHROME_CHANNEL=chromium npm run test:e2e`. Razorpay responses are mocked in tests; a live Test Mode payment needs your own keys and is not claimed as verified.


## 🔐 Security and limits

- Passwords are hashed with bcrypt; sessions live in **HttpOnly** cookies (Secure in production).
- Order ownership, request-origin checks, account rate limits and server-side validation guard every customer route.
- `.env` files, dependencies, build output, local database files and test artifacts are git-ignored; only example env files are tracked.
- Not included: real payments, refunds, admin dashboard, password recovery or courier booking. See [docs/PROJECT_REVIEW.md](docs/PROJECT_REVIEW.md) for the full list of findings and boundaries.

---

<p align="center">
  Made by <a href="https://github.com/czarion"><b>Ishan Saini</b></a>
  <br />
  <sub>Photography: Unsplash · Fonts: DM Sans, Manrope, Playfair Display</sub>
</p>
