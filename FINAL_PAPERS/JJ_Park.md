## UniMarket: A Trust-Based Open Source Marketplace for University Students
JJ Park, Fall 2025, https://github.com/jjpark00


### Introduction

**Abstract**

UniMarket is a localized, open-source mobile marketplace application designed exclusively for university students. While generic platforms like Facebook Marketplace or Craigslist exist, they lack the safety verification and academic specificity required by students. UniMarket solves this by enforcing .edu email verification and integrating features like ISBN scanning for textbooks. This project utilizes an Agile development framework and open-source governance to foster a student-led developer community. By prioritizing trust, safety, and community contribution, UniMarket aims to create a sustainable circular economy within the campus ecosystem (Sommerville, 2015).

**Background & Motivation**

For university students, buying and selling used goods—textbooks, dorm furniture, and electronics—is a semesterly ritual. However, existing platforms present significant friction. Meeting strangers from Craigslist can be unsafe, and general marketplaces lack specific categories for academic needs. According to a survey of campus life, over 60% of students feel uncomfortable meeting strangers off-campus for trade.

As a student living in a dorm, I experienced this frustration firsthand when trying to sell my mini-fridge. I received spam messages on Facebook and had to coordinate awkward meetups with non-students. I realized there was a need for a "closed-loop" marketplace where trust is built-in through university affiliation. UniMarket was born from this motivation: to build a safe, efficient, and student-centric trading platform that leverages the technical talent of the student body through an open-source model.


#### Project Vision & Community

**Target Audience**
The primary users are university students who need to buy or sell affordable goods safely on campus. Secondary users include faculty and staff who seek a trustworthy community market.

**Contributor Community**
UniMarket is designed as an educational open-source project. We actively invite:
* **CS Students:** To contribute code and improve features such as recommendation algorithms.
* **Design Students:** To refine UI/UX for better accessibility.
* **Student Council:** To act as community moderators and governance partners.  


#### Technical Stack & Methodology

**Technical Stack**
To ensure scalability and ease of contribution for student developers, we selected a modern, widely-used stack:
* **Frontend:** React Native (Cross-platform support for iOS/Android).
* **Backend:** Node.js with Express (Lightweight and familiar to most CS students).
* **Database:** MongoDB (NoSQL structure allows flexible product listings).
* **Authentication:** Firebase Auth (Specifically for .edu email verification).

__Methodology & Workflow__         

The project follows a semester-aligned Agile methodology (Agile Alliance, 2001). Development is broken into 2-week sprints to accommodate students' academic schedules.
* **Sprint 1-2:** MVP Development (Auth, Listing, Chat).
* **Sprint 3:** Beta Testing with a small pilot group (e.g., one dorm).
* **Sprint 4:** Feedback implementation and full launch.

We utilize GitHub for version control and project management. Features are tracked using Kanban boards (To Do, In Progress, Done), and automated testing pipelines run on every Pull Request to prevent regressions (GitHub, n.d.).


#### Governance & Sustainability

**Governance Strategy**
To maintain a healthy open-source ecosystem, UniMarket enforces strict governance:
1. **Code of Conduct:** We prioritize inclusivity and respect. Any harassment in comments or code reviews results in a ban.
2. **Contribution Guidelines:** All PRs must pass automated tests and require at least one peer review from a maintainer.
3. **Safety & Moderation:** A "User Reputation System" allows the community to self-regulate. Disputes are handled by a rotation of student moderators.

__Managing Technical Debt__

In the MVP phase, we rely heavily on Firebase for speed. However, as the user base grows, this creates a "vendor lock-in" risk and potential cost issues (Fowler, 2009). To mitigate this, we plan to decouple the authentication service in Phase 2, migrating to a self-hosted solution if costs skyrocket. Code is modularized to make this transition smoother. Additionally, the project’s sustainability relies on the "Student Developer Club" model, where senior students mentor juniors to take over maintainer roles upon graduation.


### Conclusion      

UniMarket is more than just a trading app; it is a digital infrastructure for campus sustainability. By solving the immediate pain points of safety and relevance, it improves student quality of life. Furthermore, its open-source nature provides a practical learning sandbox for future developers. Through structured project management and community governance, UniMarket demonstrates how technology can foster trust and collaboration within a university environment.


### References     

Agile Alliance. (2001). *The Agile Manifesto*. http://agilemanifesto.org.

Fowler, M. (2009). *Technical Debt Quadrant*. https://martinfowler.com/bliki/TechnicalDebtQuadrant.html

GitHub. (n.d.). *Open Source Guides*. https://opensource.guide.

Sommerville, I. (2015). *Software Engineering* (10th ed.). Pearson.
