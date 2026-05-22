# Product Requirements Document: Lab Access Website

## 1. Overview

**Product:** Lab Access - Company Website
**Type:** Single-page static website (HTML, CSS, JS)
**Purpose:** Informative marketing website for Lab Access, a diagnostic centre offering medical lab services, health screenings, and wellness packages.

---

## 2. Goals

- Establish an online presence for Lab Access
- Clearly communicate services offered to potential patients
- Provide easy access to contact information and location
- Build trust through professional presentation and social proof
- Drive walk-ins and phone inquiries

---

## 3. Target Audience

- Local residents seeking lab/diagnostic services
- Patients referred by doctors for specific tests
- Corporate clients looking for employee wellness packages
- Health-conscious individuals interested in preventive screenings

---

## 4. Site Structure (Single Page Sections)

### 4.1 Navigation Bar
- Fixed/sticky top navigation
- Logo (left) + nav links (right)
- Links: Home, About, Services, Packages, Testimonials, Contact
- Smooth scroll to corresponding sections
- Mobile hamburger menu

### 4.2 Hero Section
- Headline: tagline communicating trust and care (e.g., "Accurate Diagnostics. Trusted Results.")
- Subheadline: brief value proposition
- CTA button: "Book a Test" or "Contact Us" (scrolls to contact section)
- Background: clean medical/lab imagery or gradient

### 4.3 About Section
- Brief company description (2-3 paragraphs)
- Key highlights (icon + text):
  - Certified laboratory
  - Experienced technicians
  - Quick turnaround on results
  - Affordable pricing

### 4.4 Services Section
- Card-based layout displaying core services:
  - **Routine Blood Tests** (CBC, blood sugar, lipid profile, etc.)
  - **Urine & Stool Analysis**
  - **Liver & Kidney Function Tests**
  - **Thyroid Panel**
  - **Diabetes Screening (HbA1c, Glucose)**
  - **Infection Screening (HIV, Hepatitis, STI panels)**
  - **Hormonal Assays**
  - **X-Ray & Imaging** (if applicable)
- Each card: icon, title, short description

### 4.5 Wellness Packages Section
- 3-4 tiered packages displayed as pricing-style cards:
  - **Basic Wellness** - essential blood work + vitals
  - **Comprehensive Health Check** - expanded panel + organ function
  - **Executive Screening** - full-body check including imaging
  - **Women's / Men's Health** - gender-specific panels
- Each card: package name, included tests (bullet list), price (or "Contact for pricing"), CTA button

### 4.6 Why Choose Us Section
- 3-4 key differentiators with icons:
  - NAFDAC/CAP certified (or relevant local accreditation)
  - Same-day results for most tests
  - Home sample collection available
  - Affordable and transparent pricing

### 4.7 Testimonials Section
- 3 patient testimonial cards (carousel or grid)
- Each: quote, patient name (first name + last initial), rating stars

### 4.8 Contact / Location Section
- Address with embedded Google Map
- Phone number (clickable tel: link)
- Email address (clickable mailto: link)
- Operating hours table
- Simple contact form: Name, Phone, Email, Test/Service of interest, Message
- WhatsApp link/button (if applicable)

### 4.9 Footer
- Company name and short tagline
- Quick links (repeat nav)
- Social media icons (Facebook, Instagram, Twitter/X)
- Copyright notice

---

## 5. Design Requirements

### Visual Style
- **Color Palette:** Medical blue (#1A73E8 or similar) as primary, white background, light gray sections for contrast, green accent for CTAs
- **Typography:** Clean sans-serif (e.g., Inter, Poppins, or Open Sans)
- **Imagery:** Professional, clean lab/medical stock photos; avoid overly clinical or intimidating visuals
- **Tone:** Professional, approachable, trustworthy

### Layout
- Max content width: ~1200px, centered
- Alternating white/light-gray section backgrounds for visual separation
- Generous whitespace
- Card-based layouts for services and packages

---

## 6. Technical Requirements

### Stack
- **HTML5** - semantic markup
- **CSS3** - custom styles, no framework required (optionally use CSS variables for theming)
- **Vanilla JavaScript** - minimal, for interactivity only

### Features (JS)
- Smooth scroll navigation
- Mobile hamburger menu toggle
- Scroll-based active nav link highlighting
- Simple form validation (client-side)
- Testimonial carousel (optional, can be static grid)
- Scroll reveal animations (subtle fade-in on scroll)

### Performance
- No external CSS/JS frameworks (keep it lightweight)
- Optimized images (WebP preferred, with fallbacks)
- Total page weight target: < 1MB
- Google Fonts loaded via `<link>` with `display=swap`

### Responsiveness
- Mobile-first approach
- Breakpoints: 480px, 768px, 1024px, 1200px
- All sections must be fully functional on mobile

### Accessibility
- Semantic HTML (header, nav, main, section, footer)
- Alt text on all images
- Sufficient color contrast (WCAG AA)
- Keyboard navigable
- Skip-to-content link

### SEO
- Proper meta tags (title, description, keywords)
- Open Graph tags for social sharing
- Structured data (LocalBusiness schema)
- Single H1, logical heading hierarchy

---

## 7. Content Requirements

| Section        | Content Needed                              | Source       |
| -------------- | ------------------------------------------- | ------------ |
| Hero           | Tagline, subheadline                        | To be written |
| About          | Company description, founding story         | Client       |
| Services       | List of services + short descriptions       | Client       |
| Packages       | Package names, included tests, pricing      | Client       |
| Testimonials   | 3 patient quotes (can use placeholder)      | Client       |
| Contact        | Address, phone, email, hours                | Client       |
| Images         | Lab photos, team photo, logo                | Client       |

---

## 8. File Structure

```
lab-access/
├── index.html
├── css/
│   └── styles.css
├── js/
│   └── main.js
├── images/
│   ├── logo.svg
│   ├── hero-bg.webp
│   └── ...
└── README.md
```

---

## 9. Out of Scope (v1)

- Online test booking / appointment system
- Patient portal / results login
- Payment processing
- Blog / news section
- Multi-language support
- Backend / database

---

## 10. Success Metrics

- Page loads in under 2 seconds
- Mobile-friendly (passes Google Mobile-Friendly Test)
- All sections visible and navigable on all screen sizes
- Contact form submits correctly (frontend validation; backend handling is out of scope for v1)
- Lighthouse score: 90+ on Performance, Accessibility, Best Practices, SEO
