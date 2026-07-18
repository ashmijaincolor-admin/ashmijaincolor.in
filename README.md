<div align="center">
  <img src="./frontend/assets/images/logo.png" alt="Ashmija in Color Logo" width="150" />
  <h1>Ashmija in Color — Premium Mural Studio Platform</h1>
  <p>
    <strong>A high-performance, serverless web platform for South Asia's premier custom mural and hand-painted wall art collective.</strong>
  </p>
  <p>
    <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5" />
    <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" alt="CSS3" />
    <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript" />
    <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase" />
    <img src="https://img.shields.io/badge/GSAP-88CE02?style=for-the-badge&logo=greensock&logoColor=white" alt="GSAP" />
  </p>
</div>

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Architecture & Tech Stack](#-architecture--tech-stack)
- [Core Features](#-core-features)
  - [Client-Facing Website](#1-client-facing-website)
  - [Admin Dashboard](#2-admin-dashboard)
- [Directory Structure](#-directory-structure)
- [Prerequisites](#-prerequisites)
- [Comprehensive Setup Guide](#-comprehensive-setup-guide)
  - [1. Supabase Initialization](#step-1-initialize-supabase-database)
  - [2. Storage Buckets Configuration](#step-2-storage-buckets-configuration)
  - [3. Row Level Security (RLS)](#step-3-set-row-level-security-rls-permissions)
  - [4. AI Reply Edge Function](#step-4-deploy-the-ai-reply-edge-function)
  - [5. Application Configuration](#step-5-configure-app-connection)
  - [6. Admin User Setup](#step-6-create-admin-user)
- [Deployment](#-deployment)
- [Performance & SEO](#-performance--seo)
- [License](#-license)

---

## 🔭 Overview

Welcome to the official codebase for **Ashmija in Color**. This platform is meticulously designed to showcase premium hand-painted wall murals, ceiling art, and bespoke artistic spaces. It operates as a completely **serverless** architecture, blending a visually stunning, GSAP-animated frontend with a secure, headless Supabase backend. It empowers the administrative team to seamlessly manage inquiries, portfolio pieces, and client reviews—augmented by AI-generated responses.

---

## ⚙️ Architecture & Tech Stack

This project follows a JAMstack/Serverless architecture.

* **Frontend UI**: Vanilla HTML5, CSS3, and JavaScript (ES6+). Uses custom responsive styling and modern design aesthetics (glassmorphism UI, smooth gradients).
* **Animations**: GSAP (GreenSock Animation Platform) for high-performance scroll triggers and micro-interactions.
* **Backend Backend-as-a-Service (BaaS)**: [Supabase](https://supabase.com/) for PostgreSQL database, Authentication, and Storage.
* **Serverless Functions**: Deno-based Supabase Edge Functions for generative AI tasks (Drafting ML review replies).
* **Icons**: Tabler Icons Webfont.
* **Image Processing**: Client-side HTML5 Canvas compression before uploading heavy image assets to the cloud.

---

## ⚡ Core Features

### 1. Client-Facing Website
* **Immersive 3D Portfolio:** Interactive museum-style galleries displaying residential, corporate, and public murals.
* **Performant Animations:** Custom floating elements, parallax hero banners, and 3D carousels that work seamlessly across devices.
* **Dynamic Review Engine:** A custom "Rate Us" modal featuring an avatar picker, custom photo uploads, and an auto-compressor for heavy images.
* **Direct Inquiry System:** A smooth contact form that instantly writes leads to the Supabase database.
* **SEO Optimized:** Full OpenGraph, Twitter Cards, Schema.org LocalBusiness JSON-LD, semantic HTML, and dynamic sitemaps tailored for maximum search visibility in Tamil Nadu and across India.

### 2. Admin Dashboard
* **Real-time Analytics:** Instant statistics (Portfolio count, active artists, unread inquiries, average rating) without complex setup.
* **Intelligent Inquiry Management:** Parses contact forms, highlights the "Project Type" with styled badges, and provides slide-out panels to manage lead states (New, Seen, Closed).
* **AI-Assisted Review Management:** Admins can view, approve, or hide user-submitted reviews. Features a **"Generate AI Reply"** tool that calls a Supabase Edge Function to draft personalized, professional responses to client feedback.
* **Secure Auth:** JWT-based authentication ensuring only authorized founders/managers can access the data.

---

## 📁 Directory Structure

```text
├── frontend/                     # Static website assets & panels
│   ├── index.html                # Client-facing public landing page
│   ├── sitemap.xml               # SEO sitemap
│   ├── robots.txt                # Search engine crawler instructions
│   ├── Terms & conditions.html   # Legal documents
│   ├── Privacy Policy.html       # Legal documents
│   ├── css/                      # CSS styling variables, animations & layouts
│   ├── js/                       # Core javascript controllers
│   │   ├── public/               # GSAP Animations, sliders, and form modules
│   │   └── shared/               # Supabase database client config & data loaders
│   └── admin/                    # Administrative dashboard panel
│       ├── index.html            # Admin login & section routing Shell
│       ├── css/                  # Admin styling sheets & widgets
│       └── js/                   # Dashboard logic (Inquiries, Reviews, Auth, Toasts)
├── supabase-migration/           # Database setup and cloud assets
│   ├── supabase_schema.sql       # PostgreSQL schema creation script
│   ├── seed_data_pg.sql          # Demo project data inserts for testing
│   └── edge-functions/           # Supabase edge functions
│       └── generate-reply/       # Deno function for ML AI review replies
├── package.json                  # Node scripts and dev dependencies (Prettier/ESLint)
└── eslint.config.js              # Linter configuration for code consistency
```

---

## 📋 Prerequisites

Before deploying or running this project locally, ensure you have:
1. A **[Supabase Account](https://supabase.com/)** (Free tier is perfectly sufficient).
2. The **[Supabase CLI](https://supabase.com/docs/guides/cli)** installed (required only for deploying the Edge Function).
3. Any standard web host for static files (e.g., Vercel, Netlify, GitHub Pages, Hostinger).

---

## 🚀 Comprehensive Setup Guide

Follow these steps meticulously to get the entire ecosystem running from A to Z.

### Step 1: Initialize Supabase Database
1. Go to your [Supabase Dashboard](https://supabase.com/dashboard) and create a new project.
2. Navigate to the **SQL Editor** from the left sidebar.
3. Open `supabase-migration/supabase_schema.sql` from this repository, copy its contents, and paste it into the Supabase SQL Editor.
4. Click **Run** to generate the necessary tables (`reviews`, `inquiries`, `portfolio`, etc.).
5. *(Optional)* Run `supabase-migration/seed_data_pg.sql` if you want dummy data to test the Admin Dashboard immediately.

### Step 2: Storage Buckets Configuration
1. In Supabase, go to **Storage**.
2. Create new public buckets (e.g., `avatars`, `portfolio-images`, `review-uploads`) depending on the schema requirements.
3. Ensure these buckets are set to **Public** so images can be served on the frontend.

### Step 3: Set Row Level Security (RLS) Permissions
Since this app doesn't use a Node.js middle-tier server, the frontend communicates directly with Supabase. RLS is critical to prevent malicious writes.

Run these SQL commands in the SQL Editor to allow public form submissions safely:
```sql
-- Allow anonymous inserts on the reviews table
CREATE POLICY "public insert reviews" ON reviews FOR INSERT WITH CHECK (true);

-- Allow anonymous inserts on the inquiries table
CREATE POLICY "public insert inquiries" ON inquiries FOR INSERT WITH CHECK (true);

-- Read policies for approved reviews and portfolio items
CREATE POLICY "public read approved reviews" ON reviews FOR SELECT USING (status = 'approved');
CREATE POLICY "public read portfolio" ON portfolio FOR SELECT USING (true);
```

### Step 4: Deploy the AI Reply Edge Function
The admin dashboard uses an Edge Function to draft AI replies to client reviews.
Open your local terminal at the root of the project:
```bash
# Login to your Supabase account via CLI
supabase login

# Link your local repo to your Supabase project (Find the ID in project settings)
supabase link --project-ref your-project-id

# Deploy the generative AI function
supabase functions deploy generate-reply
```
*(Make sure you have set any required OPENAI_API_KEY or relevant AI keys in your Supabase Edge Function secrets if the function script demands it).*

### Step 5: Configure App Connection
Connect your static frontend to your newly created Supabase backend.
1. Open `frontend/js/shared/config.js`.
2. Replace the placeholder values with your Supabase Project URL and Anon Key (found in **Project Settings -> API**).

```javascript
window.appConfig = {
  SUPABASE_URL: "https://your-project-id.supabase.co",
  SUPABASE_ANON_KEY: "your-anon-key-here",
  ML_REPLY_FUNCTION_URL: "https://your-project-id.supabase.co/functions/v1/generate-reply"
};
```

### Step 6: Create Admin User
1. In the Supabase Dashboard, navigate to **Authentication** -> **Users**.
2. Click **Add User** -> **Create New User**.
3. Set the email and password for the admin account. This credential will be used to log into `/admin`.

---

## 🌍 Deployment

Since the frontend is entirely static (HTML/CSS/JS), deployment is incredibly straightforward:

1. **Vercel / Netlify / Cloudflare Pages:**
   * Connect your GitHub repository.
   * Set the **Publish Directory** (or root directory) to `frontend`.
   * Deploy.
   
2. **Traditional Hosting (Hostinger, cPanel, etc.):**
   * Compress the contents of the `frontend/` folder into a `.zip` file.
   * Upload and extract it to your `public_html` directory.

Once deployed:
* **Public Site**: `https://yourdomain.com`
* **Secure Admin Dashboard**: `https://yourdomain.com/admin` (Access is automatically restricted by Supabase Auth state checking in the admin JS files).

---

## 📈 Performance & SEO

* **Asset Optimization:** Client-side canvas compression reduces uploaded image sizes by up to 80% before they ever hit the database.
* **SEO Metadata:** Fully optimized `robots.txt`, `sitemap.xml`, Canonical tags, and OpenGraph/Twitter Meta tags are injected to ensure maximum visibility in organic searches for mural artist services in India.
* **Schema.org:** JSON-LD `LocalBusiness` data is implemented to improve rich snippet results in Google Maps and Search.

---

## 📄 License

&copy; 2026 **Ashmija in Color**. All rights reserved. 
This codebase is proprietary and strictly for the use of Ashmija in Color's operations. Unauthorized copying, distribution, or reproduction of these assets is prohibited.
