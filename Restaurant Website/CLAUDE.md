# Foodio - Premium Food Ordering App

## Overview

Foodio is a modern food ordering web application with a premium, minimalist design. Users can browse a curated food menu by category, search items, view order history with status tracking, and sign in/register via a modal. All data is currently static (no backend).

## Tech Stack

- **Framework:** Next.js 16 (App Router)
- **Language:** TypeScript (strict mode)
- **UI:** React 19
- **Styling:** Tailwind CSS 4
- **Animations:** Framer Motion 12
- **Icons:** Lucide React

## Running the Project

```bash
cd foodio
npm install
npm run dev      # starts dev server on port 3000
npm run build    # production build
npm start        # production server
```

## Project Structure

```
foodio/
├── app/                        # Next.js App Router (pages & layouts)
│   ├── layout.tsx              # Root layout - Google Fonts (Playfair Display, Inter), metadata
│   ├── globals.css             # Tailwind import + theme variables (colors, fonts)
│   ├── page.tsx                # Home: Navbar + HeroSection + CategoriesSection + Footer
│   ├── food-menu/page.tsx      # Menu: Navbar + FoodMenuSection + Footer
│   └── my-orders/page.tsx      # Orders: Navbar + MyOrdersSection + Footer
│
├── components/                 # React components (all client except Footer)
│   ├── Navbar.tsx              # Sticky nav, responsive mobile menu, auth modal trigger
│   ├── HeroSection.tsx         # Split hero with CTA, food image, floating badges
│   ├── CategoriesSection.tsx   # Category pills + food grid (4 items per category)
│   ├── FoodMenuSection.tsx     # Full menu with search bar, category filter, sort button
│   ├── FoodCard.tsx            # Food item card with image, price, "Add to Cart"
│   ├── AuthModal.tsx           # Sign in / Register modal with tab switcher
│   ├── MyOrdersSection.tsx     # Orders list container
│   ├── OrderCard.tsx           # Order details + 4-step status stepper
│   └── Footer.tsx              # Footer with logo, copyright, links (server component)
│
├── data/                       # Static mock data
│   ├── menuItems.ts            # FoodItem interface, 12 items across 3 categories
│   └── orders.ts               # Order/OrderItem interfaces, 2 sample orders
│
├── public/images/              # Food photos (image1-3.jpeg)
├── package.json
├── tsconfig.json               # Strict TS, path alias @/* -> ./*
├── next.config.ts              # Image domains: unsplash
└── postcss.config.mjs          # Tailwind PostCSS plugin
```

## Routes

| Route        | Page File              | Components Used                                    |
|-------------|------------------------|----------------------------------------------------|
| `/`         | `app/page.tsx`         | Navbar, HeroSection, CategoriesSection, Footer     |
| `/food-menu`| `app/food-menu/page.tsx`| Navbar, FoodMenuSection, Footer                   |
| `/my-orders`| `app/my-orders/page.tsx`| Navbar, MyOrdersSection, Footer                   |

## Design System

### Colors (defined in `globals.css`)
- **Primary:** `#1A3C34` (deep green) - buttons, nav, headings
- **Cream:** `#FFF8F0` - hero background, card accents
- **Accent:** `#F5EDE3` - category pills, tab switcher background
- **Text Dark:** `#1A1A1A` - primary text
- **Text Muted:** `#6B6B6B` - descriptions, secondary text

### Fonts
- **Playfair Display** (serif) - logo, hero headings, premium feel
- **Inter** (sans) - body text, UI elements, labels

### Patterns
- Rounded-full buttons and pills
- Rounded-3xl cards and modals
- Framer Motion for enter/exit animations and scroll-triggered reveals
- Responsive: mobile-first with `md:` and `lg:` breakpoints

## Key Data Structures

### FoodItem (`data/menuItems.ts`)
```ts
{ name: string, description: string, price: string, image: string }
```
Categories: "Starters" (4), "Main Courses" (4), "Desserts" (4)

### Order (`data/orders.ts`)
```ts
{ id: string, placedAt: string, status: OrderStatus, items: OrderItem[], totalAmount: number, deliveryAddress: string }
```
Status flow: `pending` -> `preparing` -> `ready` -> `completed`

## Component Notes

- **Navbar:** Fragment wrapper (`<>`) renders nav + AuthModal as siblings (modal needs to escape sticky stacking context)
- **FoodCard:** Accepts `animateOnLoad` prop - true for homepage (mount animation), false for menu page (scroll-triggered)
- **AuthModal:** Forms are UI-only (`preventDefault`), no backend submission
- **OrderCard:** Contains StatusBadge and OrderStepper sub-components inline
- **Shopping cart badge:** Hardcoded count of 2 (no cart state management yet)
- **Sort button** in FoodMenuSection is visual only (not functional)

## What's Not Implemented Yet

- Backend / API integration
- Actual authentication (modal is UI-only)
- Cart state management
- Order placement flow
- Payment processing
- Sort functionality on menu page
