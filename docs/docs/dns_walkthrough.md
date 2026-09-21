# Plain-English Guide: How DNS and Web Hosting Work

**Author:** ML Intern — FlyRank Search Intelligence  
**Document:** DNS Infrastructure & Routing Walkthrough  

---

## 1. What is DNS? (The Web's Digital Phonebook)

Computers don't speak human language or understand domain names like `flyrank.ai` or `yourname.netlify.app`. Instead, they locate each other on the internet using numerical IP addresses, such as `192.0.2.1` (IPv4) or `2001:db8::1` (IPv6).

The **Domain Name System (DNS)** acts as the internet's phonebook. It translates human-friendly website addresses into computer-friendly IP addresses so your browser knows exactly which server on Earth to contact.

---

## 2. What Happens When Someone Types Your Website Address?

When a teammate or recruiter types your website address into their browser and hits **Enter**, a 4-step sequence occurs in less than 100 milliseconds:

[User's Browser] ──> [DNS Resolver] ──> [Authoritative Nameserver] ──> [Netlify/GitHub Server]


1. **The Request & The Resolver:**
   * Your browser asks the local internet connection: *"Where is `yourname.netlify.app`?"*
   * The request goes to a **DNS Resolver** (usually provided by your Internet Service Provider or service like Cloudflare `1.1.1.1` or Google `8.8.8.8`).

2. **Searching the Hierarchy (Nameserver Lookup):**
   * If the Resolver doesn't have the IP address cached in memory, it asks the **Authoritative Nameserver** responsible for managing records for that domain.

3. **The Answer (DNS Record Response):**
   * The Authoritative Nameserver checks its lookup database, finds the matching record, and sends the IP address back to the DNS Resolver.

4. **Connecting to the Host:**
   * The Resolver delivers the IP address back to your browser.
   * Your browser establishes a secure connection (**HTTPS**) with that IP address, requests the HTML file (`index.html`), and displays your portfolio on screen.

---

## 3. What is a CNAME Record and Why Do We Use It?

When setting up custom domains with hosts like Netlify, Vercel, or GitHub Pages, you frequently work with two primary types of DNS records:

* **A Record (Address Record):** Maps a domain name directly to a fixed numerical IP address (e.g., `example.com` -> `192.0.2.1`).
* **CNAME Record (Canonical Name Record):** Maps one domain name to another domain name instead of a hardcoded IP address (e.g., `www.yourcustomdomain.com` -> `yourname.netlify.app`).

### Why CNAME is Crucial for Modern Hosting:
Cloud hosting platforms use thousands of distributed servers across the globe to deliver web pages quickly. Because hosting providers frequently change IP addresses for load balancing and server maintenance, hardcoding an IP address using an **A Record** can break your site when an IP updates.

A **CNAME Record** acts as an alias pointer. It tells the internet: *"Whenever someone visits `www.myname.com`, don't look for a static IP—go ask `yourname.netlify.app` where the site is currently hosted."* Netlify manages the underlying IP routing automatically behind that alias.

---

## 4. HTTPS & SSL Security

When your site is deployed via Netlify or GitHub Pages, an **SSL/TLS Certificate** is issued automatically via Let's Encrypt. This encrypts all traffic between the user's browser and the web server, ensuring that a secure padlock icon appears in the browser bar (`https://`).

---

## 5. Verification Checklist

- [x] Plain-language explanation suitable for non-technical team members.
- [x] Step-by-step breakdown of DNS Resolvers, Nameservers, and IP responses.
- [x] Clear explanation of CNAME records vs. A records.
- [x] Covers HTTPS automatic SSL configuration on modern static hosts.
