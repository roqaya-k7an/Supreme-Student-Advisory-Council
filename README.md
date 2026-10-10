<div align="center">

<img src="docs/assets/seal-1.png" alt="Supreme Student Advisory Council" width="110" />

# Supreme Student Advisory Council

### International Islamic University, Islamabad (IIUI)

**A modern, fully bilingual (English · العربية) platform for student
registration, council representation, and campus competitions.**

<br/>

### [Visit the Live Website](https://supreme-student-advisory-council.netlify.app/)

<br/>

[![Live Demo](https://img.shields.io/badge/LIVE-Visit%20Website-219EBC?style=for-the-badge&labelColor=023047)](https://supreme-student-advisory-council.netlify.app/)
[![Netlify](https://img.shields.io/badge/Deployed%20on-Netlify-00C7B7?style=for-the-badge&logo=netlify&logoColor=white)](https://www.netlify.com/)

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![Bilingual](https://img.shields.io/badge/Bilingual-EN%20%2F%20AR%20(RTL)-FB8500?style=flat-square)

</div>

<br/>

<div align="center">
  <img src="preview/hero.png" alt="Website home page" width="92%" />
</div>

<br/>

---

## Overview

The Supreme Student Advisory Council website is the official online home of the
Council at IIUI. It gives students a single, welcoming place to learn about the
Council, register to join, and take part in competitions and activities.

The entire experience is **bilingual** — one click switches the whole site
between **English** and **Arabic (العربية)** with full right-to-left (RTL)
layout — and it is designed to work seamlessly across phones, tablets, and
desktops.

---

## Features

| Feature | Description |
|---------|-------------|
| **Bilingual experience** | Instant English / Arabic switching with complete RTL support. |
| **Student registration** | A clean, guided sign-up to join the Council. |
| **Competitions & events** | Browse open competitions and register online. |
| **Council & members** | Learn about the Council, its roles, and its members. |
| **Role-based access** | Three distinct access levels — Admin, Council, and Student — enforced on the server. |
| **Secure admin area** | A protected dashboard to manage users, competitions, and registrations. |
| **Fully responsive** | A polished experience across every screen size. |

---

## Roles & Access

The platform has **three access levels**, each unlocking a different part of the
site. Access is enforced on the server (every API request is checked), so it
cannot be bypassed by editing the page or calling the API directly.

<div align="center">

| Role | Access level | Can do |
|:----:|:------------:|--------|
| **Admin** | Full control | Manage users, manage competitions (create · edit · open · close), view all registrations, and reach every page. |
| **Council** | Advisory Council + Competitions | View Advisory Council content and browse / register for competitions. |
| **Student** | Competitions only | View the competitions the Admin has opened and register for them. |

</div>

> The Admin creates every account (name · email · password · role). There is no
> self-signup — only the Admin can create, edit, enable/disable, or delete users.

Full setup and API details are in **[RBAC_SETUP.md](RBAC_SETUP.md)**.

---

## A Look Inside

**Simple, three-step registration**

<div align="center">
  <img src="preview/registration.png" alt="How registration works" width="88%" />
</div>

<br/>

**Responsive mobile layout**

<div align="center">
  <img src="preview/mobile.png" alt="Mobile view" width="300" />
</div>

---

## Built With

<div align="center">

| Layer | Technologies |
|-------|--------------|
| **Front-end** | HTML5 · CSS3 · JavaScript · bilingual & RTL-aware UI |
| **Back-end** | Node.js · serverless functions (Netlify / Vercel) |
| **Auth & access** | JWT sessions · server-enforced role-based access control |
| **Database** | PostgreSQL |
| **Hosting** | Netlify |

</div>

---

## Visual Identity

<div align="center">

| Navy | Teal | Sky | Amber | Orange | Paper |
|:----:|:----:|:---:|:-----:|:------:|:-----:|
| ![](https://img.shields.io/badge/-023047-023047) | ![](https://img.shields.io/badge/-219EBC-219EBC) | ![](https://img.shields.io/badge/-8ECAE6-8ECAE6) | ![](https://img.shields.io/badge/-FFB703-FFB703) | ![](https://img.shields.io/badge/-FB8500-FB8500) | ![](https://img.shields.io/badge/-F5FAFC-F5FAFC) |
| `#023047` | `#219EBC` | `#8ECAE6` | `#FFB703` | `#FB8500` | `#F5FAFC` |

</div>

---

<div align="center">

[Visit the live website](https://supreme-student-advisory-council.netlify.app/)

<br/>

Designed & developed for the **Supreme Student Advisory Council**
International Islamic University, Islamabad

</div>
