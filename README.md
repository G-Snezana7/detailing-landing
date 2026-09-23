### Luxury Car Detailing — Premium Landing Page

A modern, high-performance, and fully responsive landing page developed for a premium car care and detailing studio.

This project demonstrates production-ready frontend architecture, strict adherence to design specifications, secure API configurations, and top-tier technical optimization.

### 🚀 Live Demo

**[👉 Click here to view the live website](https://detailing-landing.netlify.app/)**

### 📊 Google Lighthouse Metrics

- **Performance:** 94/100 🟢
- **Accessibility:** 98/100 🟢
- **Best Practices:** 100/100 🟢
- **SEO:** 92/100 🟢

### 🛠️ Technical Stack & Production Features

- **Framework:** Vue 3 (Composition API) built with Vite for lightning-fast Hot Module Replacement (HMR).
- **Production-Ready Lead Gen:** Implemented a high-end modal pop-up form triggered dynamically across components using Vue custom events (`$emit` / `defineEmits`).
- **Smooth UX & States:** Integrated native Vue `<Transition>` component for cinematic modal animations, added conditional rendering (`v-if`/`v-else`) for an instant user-friendly success state, and forced form reset to prevent duplicate submissions.
- **Secure Backend API Integration:** Seamless lead delivery to a commercial backend service via standardized `FormData` objects. Completely free of CORS-vulnerabilities.
- **Environment Safety (.env):** Strictly abides by security best practices. All backend endpoint access keys are injected dynamically via Vite env variables (`import.meta.env`) and securely stored within production CI/CD environment variables, keeping repository history clean.
- **Styles:** Scalable SCSS structured via modern `@use` rules (no deprecated `@import`).
- **Methodology:** Component-scoped styles conforming to strict **BEM (Block, Element, Modifier)** naming conventions.
- **Accessibility (A11y):** Semantic HTML5 structuring (`<header>`, `<main>`, `<section>`), keyboard navigation support (`:focus-visible`), and explicit `aria-*` screen-reader attributes on interactive controls.
- **Performance Optimization:** Compressed WebP images, implemented `loading="lazy"` for below-the-fold assets, and prioritized critical rendering paths to guarantee green Lighthouse zones.

### 💻 Project Setup

To clone and run this application locally:

```bash
# Clone the repository
git clone https://github.com/G-Snezana7/detailing-landing.git

# Navigate into the project folder
cd detailing-landing

# Install dependencies
npm install

# Create local env file and add your key
echo "VITE_WEB3FORMS_KEY=your_key_here" > .env

# Compiles and hot-reloads for development
npm run dev

# Compiles and minifies for production
npm run build
```
