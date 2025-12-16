# UniMarket: A Trust-Based Open Source Marketplace for University Students

**Name:** JJ Parm
**Semester:** Fall 2025  
**Personal Website:** https://github.com/jjpark00

---

## Abstract

UniMarket is a localized, open-source mobile marketplace application designed exclusively for university students. While generic platforms like Facebook Marketplace or Craigslist exist, they lack the safety verification and academic specificity required by students. UniMarket solves this by enforcing .edu email verification and integrating features like ISBN scanning for textbooks. This project utilizes an Agile development framework and open-source governance to foster a student-led developer community. By prioritizing trust, safety, and community contribution, UniMarket aims to create a sustainable circular economy within the campus ecosystem. This paper outlines the motivation, technical architecture, risk management strategies, and community governance models required to bring this hypothetical project to fruition.

---

## 1. Introduction

### 1.1 Background & Literature Review

The concept of the “Circular Economy” has gained significant traction in university environments, where the turnover of goods is cyclically driven by academic semesters. According to a study by the *Journal of Sustainable Consumption* (2023), the average university student generates approximately 640 pounds of waste annually, a significant portion of which consists of reusable furniture, textbooks, and electronics. While general-purpose marketplaces like Facebook Marketplace, Craigslist, or eBay exist, they are ill-suited for the hyper-local and trust-sensitive nature of a campus ecosystem.

Research indicates that **trust** and **convenience** are the two primary barriers to student participation in the second-hand economy. A survey conducted by *Campus Safety Magazine* (2022) revealed that 60% of students feel uncomfortable meeting strangers off-campus for transactions. Furthermore, the friction of coordinating logistics without transportation limits students’ ability to trade heavy items like furniture. UniMarket addresses these gaps by creating a “walled garden” marketplace—accessible only to verified students—thereby embedding a layer of institutional trust that anonymous platforms cannot match.

### 1.2 Motivation

My personal motivation for this project stems from a chaotic move-out experience during my sophomore year. I attempted to sell a mini-fridge and a set of engineering textbooks via Facebook Marketplace. The process was fraught with inefficiencies: I received dozens of spam messages, faced low-ball offers from non-students, and ultimately had to abandon the fridge due to a buyer’s no-show. This experience highlighted a glaring gap in campus infrastructure. We have apps for studying, dining, and transportation, but no dedicated digital infrastructure for the exchange of goods. UniMarket is proposed not just as an app, but as a digital public good designed to foster sustainability, safety, and community connection.

---

## 2. Project Vision & Market Analysis

### 2.1 Target Audience

- **Primary Users:** University students living in dorms or apartments who need to buy/sell affordable goods safely.  
- **Secondary Users:** Faculty and staff seeking a trustworthy community market.  
- **Core Contributors:** Computer Science and Design students looking for real-world open-source experience.

### 2.2 Competitor Analysis

To ensure UniMarket’s viability, we analyzed existing solutions used by students. The table below summarizes the key deficiencies in current platforms that UniMarket aims to solve.

| Feature | Facebook Marketplace | Craigslist | eBay | **UniMarket** |
| :--- | :--- | :--- | :--- | :--- |
| **Verification** | Low (Anyone with FB profile) | None (Anonymous) | Medium (Email/Phone) | **High (.edu Email Required)** |
| **Safety** | Low (Stranger Danger) | Very Low | High (Shipping only) | **High (Campus Safe Zones)** |
| **Relevance** | Low (General Public) | Low | Low | **High (Curated for Students)** |
| **Fees** | None | None | High (10–15%) | **None (Open Source)** |

As shown, while platforms like eBay offer safety, they incur high fees and shipping logistics that are unnecessary for students living in the same dorm. Conversely, Craigslist is free but lacks accountability. UniMarket occupies the unique niche of being **free, hyper-local, and verified**.

---

## 3. Technical Architecture

UniMarket is built on a **microservices-oriented architecture** to ensure scalability and maintainability. This structure allows independent development of features, making it easier for students to contribute without breaking the entire system.

### 3.1 Technology Stack

To ensure scalability and ease of contribution for student developers, we selected a modern, widely-used stack:

- **Frontend:** **React Native** & **Expo** (Cross-platform support for iOS/Android)  
- **Backend:** **Node.js** with **Express** (Lightweight and familiar to most CS students)  
- **Database:** **MongoDB** (NoSQL structure allows flexible product listings)  
- **Authentication:** **Firebase Auth** (Specifically for .edu email verification)  
- **Deployment:** **Vercel** (Frontend) & **AWS EC2** (Backend)

### 3.2 Implementation Details

**1) RESTful API Design**  
The backend exposes RESTful API endpoints for handling user requests.

- `POST /api/auth/verify`: Handles the SMTP handshake to verify university emails.  
- `GET /api/items/search?isbn=...`: Integrates with the Google Books API to auto-fill textbook details when a student scans a barcode.  
- `POST /api/transaction/meetup`: Uses geolocation data to suggest the nearest “Safe Trade Zone” (e.g., Student Union, Police Station).

**2) Database Schema (MongoDB)**  
Given the unstructured nature of second-hand goods (a textbook has different attributes than a bicycle), a NoSQL database is optimal. Below is a simplified schema design for an item:

```javascript
const ItemSchema = new mongoose.Schema({
  title: { type: String, required: true },
  category: { type: String, enum: ['Textbook', 'Furniture', 'Electronics'] },
  price: Number,
  seller: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
  location: { type: { type: String, default: 'Point' }, coordinates: [Number] },
  status: { type: String, default: 'Available' }
});
```

**3) Security & Privacy**  
Security is paramount. We implement **JWT (JSON Web Tokens)** for session management. Unlike commercial apps that sell user data, UniMarket’s open-source mandate ensures strictly minimal data collection. Location data is obfuscated to a 500-meter radius to protect student privacy in dorms.

---

## 4. Methodology & Workflow

### 4.1 Agile Development

The project follows a semester-aligned Agile methodology (Agile Alliance, 2001). Development is broken into 2-week sprints to accommodate students’ academic schedules.

- **Sprint 1–2:** MVP Development (Auth, Listing, Chat)  
- **Sprint 3:** Beta Testing with a small pilot group (e.g., one dorm)  
- **Sprint 4:** Feedback implementation and full launch

### 4.2 Workflow Diagram

We utilize GitHub for version control and project management. Features are tracked using Kanban boards (To Do, In Progress, Done), and automated testing pipelines run on every Pull Request to prevent regressions (GitHub, n.d.).

**Figure 1.** *UniMarket Agile Development Workflow & System Architecture.*  
<img width="161" height="442" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/380e8b20-c73a-4307-b0bf-8336b98c84a1" />
*(Note: The diagram illustrates the data flow from the student user to the mobile app, processed by the Node.js server, and stored in the MongoDB database.)*

---

## 5. Risk Management Strategy

Managing an open-source project involves significant risks. We have categorized potential risks and established mitigation strategies based on the **Risk Impact/Probability Matrix**.

### 5.1 Technical Risks

- **Risk:** Data breaches exposing student email addresses.  
- **Mitigation:** All personally identifiable information (PII) is encrypted at rest using AES-256 standards. We will conduct monthly security audits and establish a “Bug Bounty” program where CS students are rewarded for finding vulnerabilities.

### 5.2 Operational Risks

- **Risk:** The platform becomes a “ghost town” (low liquidity of goods).  
- **Mitigation:** We will launch with a “Seeding Strategy,” partnering with the University Housing Office to promote the app during Move-In/Move-Out weeks. We will also incentivize early adopters with “Founding Member” badges.

### 5.3 Governance Risks

- **Risk:** Maintainer burnout or graduation leading to project abandonment.  
- **Mitigation:** This is the most critical risk for student-led projects. We address this through the **Succession Pipeline** described in the Sustainability section, ensuring that junior students are onboarded to leadership roles at least one semester before seniors graduate.

---

## 6. Governance & Community

### 6.1 Code of Conduct

To maintain a healthy open-source ecosystem, UniMarket enforces strict governance based on the **Contributor Covenant v2.1**.

- **Inclusivity:** We explicitly welcome contributors from non-technical backgrounds (e.g., design, marketing).  
- **Respectful Review:** Code reviews must be constructive. Comments like “this code is bad” are prohibited; “consider using this pattern for efficiency” is encouraged.

### 6.2 The Pull Request (PR) Lifecycle

Every contribution goes through a rigorous lifecycle to ensure quality:

1. **Issue Assignment:** Contributors claim a ticket from the “Good First Issue” label on GitHub.  
2. **Development:** Code is written locally on a feature branch.  
3. **Automated Testing (CI):** GitHub Actions automatically runs unit tests (Jest) when a PR is opened.  
4. **Peer Review:** A maintainer reviews the logic and style.  
5. **Merge:** Only after passing tests and review is code merged into the `main` branch.

---

## 7. Sustainability & Technical Debt

### 7.1 Managing Technical Debt

In the MVP phase, we rely heavily on Firebase for speed. However, as the user base grows, this creates a “vendor lock-in” risk and potential cost issues (Fowler, 2009).

- **Mitigation Strategy:** We plan to decouple the authentication service in Phase 2, migrating to a self-hosted solution if costs skyrocket. Code is modularized to make this transition smoother.

### 7.2 The “Student Developer Club” Model

The project’s sustainability relies on the “Student Developer Club” model. Senior students will mentor juniors to take over maintainer roles upon graduation, ensuring the project survives beyond the founder’s tenure. This creates a continuous cycle of learning and leadership, making UniMarket not just a product, but an educational institution.

---

## 8. Conclusion

UniMarket is more than just a trading app; it is a digital infrastructure for campus sustainability. By solving the immediate pain points of safety and relevance, it improves student quality of life. Furthermore, its open-source nature provides a practical learning sandbox for future developers. Through structured project management, rigorous risk analysis, and inclusive community governance, UniMarket demonstrates how technology can foster trust and collaboration within a university environment.

---

## 9. References

1. Agile Alliance. (2001). *The Agile Manifesto.* `http://agilemanifesto.org`  
2. Campus Safety Magazine. (2022). *Student Safety Survey regarding Online Marketplaces.*  
3. Fowler, M. (2009). *Technical Debt Quadrant.* `https://martinfowler.com/bliki/TechnicalDebtQuadrant.html`  
4. GitHub. (n.d.). *Open Source Guides.* `https://opensource.guide`  
5. Journal of Sustainable Consumption. (2023). *Waste Generation in Higher Education Institutions.*  
6. Sommerville, I. (2015). *Software Engineering* (10th ed.). Pearson.
