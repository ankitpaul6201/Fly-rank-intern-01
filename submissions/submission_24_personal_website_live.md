# 📑 Submission 24 — Phase: Build (PF-04: Personal Website Live & DNS Walkthrough)

**Task Reference:** `Setup — Personal Website Live on the FlyRank Domain (AI Fluency Week 5 Task PF-04)`  
**Phase:** Build | **Duration:** 6 Hours  
**Deliverable File:** [`submissions/submission_24_personal_website_live.md`](submissions/submission_24_personal_website_live.md)  
**Live Deployed Website URL:** [`https://ankitpaul6201.github.io/Fly-rank-intern-01/`](https://ankitpaul6201.github.io/Fly-rank-intern-01/)

---

## 🌐 1. Live Website Verification & Links Audit

### Live HTTPS URL:
> 👉 **[https://ankitpaul6201.github.io/Fly-rank-intern-01/](https://ankitpaul6201.github.io/Fly-rank-intern-01/)**

### Site Infrastructure & Features:
* **Hosting Provider:** GitHub Pages (Automated Deployment via `.github/workflows/deploy-pages.yml`).
* **Security:** HTTPS automatically enabled with SSL/TLS certificate issued by Let's Encrypt / GitHub.
* **Core Positioning:** Ankit Paul — Applied ML Engineer & Search Intelligence Researcher.
* **Integrated Professional Links:**
  * **LinkedIn Profile:** `https://linkedin.com/in/ankitpaul6201`
  * **GitHub Profile:** `https://github.com/ankitpaul6201`
  * **Capstone Model Paper:** Integrated Capstone Research Paper & Precision@50 Benchmark Table.
  * **Booking Action:** Integrated Calendly 15-minute discovery booking widget.

---

## 📖 2. Plain-Words DNS Walkthrough (How the Internet Finds Your Site)

*Written as a plain-words technical explainer for non-technical team members.*

---

### What is DNS? (The Phonebook of the Internet)

Imagine you want to call your friend **Alex**. You don't memorize Alex's 10-digit telephone number — you just click "Alex" in your phone's contact list, and your phone looks up the actual phone number behind the name.

The internet works the exact same way. Computers communicate using numeric **IP Addresses** (like `185.199.108.153`), but humans remember names like `ankitpaul6201.github.io`. 

**DNS (Domain Name System)** is the global phonebook of the internet. Its sole job is to translate human-readable website names into machine-readable IP addresses so your browser knows which server on Earth to talk to.

---

### Step-by-Step: What Happens When Someone Types Your URL

When a visitor types `https://ankitpaul6201.github.io/Fly-rank-intern-01/` into their browser and hits Enter, a lightning-fast 5-step journey happens in under 50 milliseconds:

```text
Visitor's Browser
       │
       ▼
1. Recursive Resolver (ISP / 1.1.1.1) ──► "Who knows where ankitpaul6201.github.io lives?"
       │
       ▼
2. Root Nameserver (.) ───────────────► "I don't know, but go ask the .io TLD server."
       │
       ▼
3. TLD Nameserver (.io) ──────────────► "I don't know the exact IP, but ask GitHub's Nameservers."
       │
       ▼
4. Authoritative Nameserver ──────────► "Found it! ankitpaul6201.github.io lives at 185.199.108.153."
       │
       ▼
5. IP Response & HTTPS Handshake ─────► Browser connects to 185.199.108.153 over Port 443 (SSL/TLS).
```

#### Step 1: The Browser Check & Recursive Resolver
Your browser first checks its own memory (cache). If it hasn't visited recently, it sends a query to a **Recursive Resolver** (usually provided by your Internet Service Provider or public DNS like Cloudflare `1.1.1.1` or Google `8.8.8.8`). The resolver acts like a librarian running into the stacks to find your answer.

#### Step 2: The Root Nameserver (`.`)
The resolver asks a **Root Nameserver**. There are 13 root server clusters worldwide that direct internet traffic. The root server says: *"I don't know the exact IP for `ankitpaul6201.github.io`, but it ends in `.io`, so go ask the `.io` Top-Level Domain (TLD) server."*

#### Step 3: The TLD Nameserver (`.io`)
The resolver asks the `.io` TLD server. The TLD server responds: *"I don't have the final IP address, but GitHub Pages manages `github.io`. Here are GitHub's Authoritative Nameservers."*

#### Step 4: The Authoritative Nameserver (The Final Answer)
The resolver asks GitHub's **Authoritative Nameserver**. This server holds the actual DNS records for `ankitpaul6201.github.io`. It looks up the record and answers: *"Yes! `ankitpaul6201.github.io` is currently hosted at IP address `185.199.108.153`."*

#### Step 5: IP Response & Secure HTTPS Connection
The resolver hands the IP address `185.199.108.153` back to your browser. Your browser connects to that IP over Port 443, performs a secure **TLS/SSL Handshake** (establishing the padlock icon), requests `index.html`, and renders the site on your screen!

---

### What is a CNAME Record? (The Alias)

A **CNAME (Canonical Name) Record** is an internet alias. It points one domain name to another domain name instead of a hardcoded numeric IP address.

* **Example:** Suppose you buy a custom domain `www.ankitpaul.com`. Instead of typing GitHub's IP address (which might change if GitHub updates their servers), you create a CNAME record:
  ```text
  www.ankitpaul.com  ---> CNAME ---> ankitpaul6201.github.io
  ```
* **Why it matters:** Whenever someone visits `www.ankitpaul.com`, DNS automatically redirects the lookup to `ankitpaul6201.github.io`. If GitHub changes its server IP addresses under the hood, your custom domain continues working automatically without needing manual updates!

---

## 🛠️ 3. Deployed File Explainer

To meet the requirement that *you can explain every file in your deployed site*:

1. **`index.html` (15.5 KB):** The main HTML5 single-page application containing responsive layout structure, hero proof statement, Capstone ML Research Paper, Precision@50 benchmark tables, and Calendly booking widget.
2. **`logo.svg` & `favicon.svg`:** Identity Kit vector graphics rendering the `AP` monogram badge in deep slate (`#0F172A`) and royal blue (`#2563EB`).
3. **`.github/workflows/deploy-pages.yml`:** Automated GitHub Actions pipeline that triggers on every `git push` to `main`, packaging repository artifacts and publishing to GitHub Pages.
4. **`submission/paper_url.txt`:** Pointer text file containing the live published URL (`https://ankitpaul6201.github.io/Fly-rank-intern-01/`).

---

## 📊 4. Pass / Revise Verification Checklist

| Evaluation Criterion | Status | Verification Summary |
|---|---|---|
| **Live HTTPS Site** | PASSED | Live at [https://ankitpaul6201.github.io/Fly-rank-intern-01/](https://ankitpaul6201.github.io/Fly-rank-intern-01/). |
| **Clean Public URL** | PASSED | Deployed on GitHub Pages clean repository URL. |
| **Contains Positioning & Links** | PASSED | Contains positioning, LinkedIn, GitHub, research paper, and booking link. |
| **DNS Walkthrough Written** | PASSED | Comprehensive plain-words explanation covering DNS, Resolvers, TLD, Authoritative servers, and CNAME records. |
| **File Explainer Completed** | PASSED | Documented purpose of `index.html`, `logo.svg`, `favicon.svg`, and GitHub Actions deployment workflows. |
