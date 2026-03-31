# 🥦 VikingEats

**A grocery discovery guide built for Western Washington University students.**

VikingEats helps WWU students find affordable, accessible food in Bellingham, WA — with real store data, bus route info, open/closed hours, a price comparison table, and an interactive map. No app download, no login — just open it in a browser.

🔗 **Live site:** [paytynkdub.github.io/viking-eats](https://paytynkdub.github.io/viking-eats)

---

## 📸 Features

| Feature | Details |
|---|---|
| 🗂 **Store Directory** | 19 Bellingham grocery stores with addresses, descriptions, and scores |
| 🗺 **Interactive Map** | Leaflet map with custom pin markers, popups, and a store sidebar |
| 🚌 **WTA Bus Routes** | Per-store WTA route info with simulated next-arrival times |
| 🕐 **Store Hours** | Live open/closed status calculated from real hours data |
| 💰 **Price Comparison** | Side-by-side table of 30+ common student staples across stores |
| 💳 **EBT Filter** | Instantly filter stores that accept SNAP/EBT benefits |
| ⚖️ **Bulk Foods Filter** | Find stores with bulk food sections (Co-op, WinCo, Costco, CHEF'STORE) |
| 🏷️ **Discount Filter** | Surface budget-friendly stores at a glance |
| 🚶 **Walkability Scores** | Per-store walk and bus accessibility scores (1–10) |
| ⭐ **WWU Student Reviews** | Read and submit student reviews with ratings and majors |
| 🔍 **Search + Filters** | Live search and 15+ filter chips including food type filters |

---

## 🏪 Stores Included

| Store | Address |
|---|---|
| Fred Meyer (Lakeway) | 800 Lakeway Dr |
| Fred Meyer (Bakerview) | 1225 W Bakerview Rd |
| Haggen (36th St) | 210 36th St |
| Haggen (12th St) | 1401 12th St |
| Haggen (Meridian) | 2814 Meridian St |
| Safeway | 1275 E Sunset Dr |
| Community Food Co-op | 1220 N Forest St |
| Grocery Outlet | 1600 Ellis St |
| Trader Joe's | 2410 James St |
| WinCo Foods | 300 E Bellis Fair Pkwy |
| Whole Foods Market | 1030 Lakeway Dr |
| Walmart Supercenter | 4420 Meridian St |
| Costco Wholesale | 4125 Arctic Ave |
| Neighborhood Market | 2019 Harris Ave |
| US Foods CHEF'STORE | 405 Ohio St |
| JJ's In and Out Food Mart | 2219 Douglas Ave |
| N State Street Market | 902 N State St Suite 103 |
| Cornwall Corner Store | 2230 Cornwall Ave |
| Walgreens | 125 Samish Way |

---

## 🛠 Tech Stack

This is a **single-file static website** — everything lives in `index.html`.

- **HTML / CSS / JavaScript** — no build tools, no frameworks, no dependencies to install
- **[Leaflet.js](https://leafletjs.com/)** `v1.9.4` — interactive map (loaded from unpkg CDN)
- **[OpenStreetMap](https://www.openstreetmap.org/)** — free map tiles, no API key required
- **[Google Fonts](https://fonts.google.com/)** — Fraunces (display) + DM Sans (body)
- **GitHub Pages** — free static hosting

> **Note:** The Leaflet map requires an internet connection to load map tiles. If opened in a sandboxed environment (e.g. some iframe previews), it will display a graceful fallback with store cards and WTA links instead of crashing.

---

## 🚀 Deployment

This site is deployed via **GitHub Pages** from the `main` branch root.

To deploy your own copy:

1. Fork or clone this repo
2. Go to **Settings → Pages**
3. Set source to `main` branch, `/ (root)` folder
4. Save — your site will be live at `https://<your-username>.github.io/<repo-name>/`

No build step required. Just push `index.html` and it's live.

---

## 📁 Project Structure

```
viking-eats/
│
├── index.html        # Entire site — data, styles, and logic in one file
└── README.md         # This file
```

All store data, review data, price comparison data, and application logic are contained in `index.html` as inline JavaScript. This makes the site fully portable — just share the file and it works.

---

## 🔧 Customization

### Adding or editing a store
Find the `STORES` array in the `<script>` block of `index.html`. Each store follows this structure:

```js
{
  id: 20,
  name: "Store Name",
  address: "123 Main St, Bellingham, WA 98225",
  lat: 48.7500,
  lng: -122.4800,
  type: "Grocery",           // Display label
  price_tier: 2,             // 1 = budget, 2 = mid, 3 = premium
  ebt: true,                 // Accepts SNAP/EBT?
  bulk: false,               // Has bulk foods section?
  discount: false,           // Discount/bargain store?
  bus_score: 8,              // 1–10
  walk_score: 7,             // 1–10
  student_rating: 4.2,       // 1.0–5.0
  review_count: 0,
  food_tags: ["produce", "pantry", "frozen"],
  description: "Short description shown on the card.",
  website: "https://example.com",
  wta_link: "https://schedules.ridewta.com/",
  hours: {
    mon: [8, 0, 21, 0],      // [openHour, openMin, closeHour, closeMin]
    tue: [8, 0, 21, 0],
    wed: [8, 0, 21, 0],
    thu: [8, 0, 21, 0],
    fri: [8, 0, 21, 0],
    sat: [9, 0, 20, 0],
    sun: [10, 0, 18, 0]
  },
  transit: [
    {
      route: "35",
      name: "Meridian St",
      stops_away: 2,
      freq_min: 30,           // Bus frequency in minutes
      direction: "Toward Downtown"
    }
  ]
}
```

### Adding price comparison data
Find the `PRICE_DATA` object. Add items to existing categories or create a new category:

```js
"🧴 New Category": [
  {
    item: "Item Name",
    unit: "per lb",
    prices: {
      "Fred Meyer (Lakeway)": 1.99,
      "Grocery Outlet": 0.99,
      "Walmart Supercenter": 0.78
    }
  }
]
```

---

## 🔮 Future Improvements

- [ ] Real WWU SSO authentication for verified student-only reviews
- [ ] Live WTA GTFS-RT feed for real-time bus arrivals (replace simulated times)
- [ ] Persistent reviews via a backend (Supabase, Firebase, etc.)
- [ ] Google Places API integration for live hours verification
- [ ] User location detection to sort stores by distance
- [ ] Mobile app wrapper (PWA manifest + service worker for offline use)
- [ ] Crowdsourced price updates with timestamps
- [ ] Accessibility audit (WCAG 2.1 AA compliance pass)

---

## 📋 Data Sources

| Data | Source |
|---|---|
| Store addresses & coordinates | Community-verified via Google Maps + CSV |
| Store hours | Sourced from individual store websites |
| Bus routes | Modeled after [WTA GTFS data](https://www.ridewta.com) |
| WTA Trip Planner | [schedules.ridewta.com](https://schedules.ridewta.com/) |
| Prices | Community-estimated; approximate regular (non-sale) pricing |
| Student ratings & reviews | Simulated seed data; expandable with real submissions |
| Map tiles | © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors |

> **Disclaimer:** Store hours, prices, and EBT acceptance can change without notice. Always verify directly with the store before your trip.

---

## 🤝 Contributing

Pull requests are welcome. If you know of a Bellingham grocery store that should be added, spot a wrong address, or want to update hours — open an issue or submit a PR with the correction.

Please keep the single-file format so the site stays portable and easy to deploy without a build step.

---

## 📄 License

MIT — free to use, modify, and share.

---

*Made with 🌲 for WWU students in Bellingham, WA*
