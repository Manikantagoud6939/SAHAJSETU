# SAHAJSETU — Unified Grassroots Ecosystem

Welcome to the official repository for **SAHAJSETU**, an integrated socio-economic digital platform powering grassroots commerce, direct agricultural trade, and community food rescue.

---

## 📱 Separate Standalone Applications

This ecosystem is engineered with dedicated, role-specific web applications that can also be installed as standalone Android Apps (PWA / TWA):

### 1. 🏬 **Local Shop AI App** (`shop.html` / `/shop`)
*Dedicated Operating System for Micro-Retailers & Kiranas*
- **Voice-Powered POS Terminal:** Ambient speech billing in vernacular dialects (Hindi, Tamil, Marathi, Bengali, Hinglish) with sub-second line itemization.
- **Fast Product Catalog & Quick Picker:** Add items, calculate CGST/SGST, and print thermal receipts.
- **Smart Inventory & Stock Velocity:** Predictive reordering warnings before critical staples deplete.
- **Customer Khata (Digital Credit Ledger):** Track neighborhood Udhar with 1-click WhatsApp payment reminders with UPI links.
- **FarmLink Procurement:** Order fresh produce directly from local farmer clusters at wholesale rates.

### 2. 🌾 **FarmLink Farming App** (`farming.html` / `/farming`)
*Dedicated Marketplace & Dispatch Portal for Farmers & FPOs*
- **Harvest Listing Studio:** Post upcoming and harvested lots with quality grades, minimum order sizes, and dispatch dates.
- **Live Mandi Price Radar:** Real-time benchmarking against Lasalgaon, Azadpur, and regional APMC mandis (+28% to +42% higher net realization).
- **Logistics & Cold-Chain Tracking:** Monitor transit trucks with GPS and temperature assurance.
- **Kisan Direct UPI & Escrow Wallet:** Instant bank withdrawals upon digital store gate delivery verification.

### 3. 🌐 **SahajSetu Ecosystem Hub** (`index.html`)
*Parent Brand & Multi-Product Launchpad*
- Unifies **Local Shop AI**, **FarmLink Marketplace**, and **FoodShare Network** (zero-waste surplus food redistribution).
- Interactive simulators, economic triad visualization, investor deck preview, and regional pilot application forms.

---

## 🏛️ Company Structure

### **Parent Brand: SAHAJSETU**
> *"Sahaj" (Effortless) + "Setu" (Bridge)*
A platform designed to empower local economies by connecting micro-retailers, farmers, and community institutions through vernacular, AI-enabled, and zero-barrier infrastructure.

---

## 🚀 How to Run / View

You can open any of the application portals directly in your browser:

```powershell
# Open Parent Hub
Start-Process "index.html"

# Open Local Shop AI App
Start-Process "shop.html"

# Open FarmLink Farming App
Start-Process "farming.html"
```

Or run via any local web server:

```powershell
npx serve .
# or
python -m http.server 3000
```
