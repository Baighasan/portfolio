---
company: "Tenstorrent"
role: "DevOps Engineer"
dateStart: "01/05/2026"
dateEnd: "Present"
---

At Tenstorrent, I worked on the CI/CD infrastructure (Kubernetes + ARC) that the entire engineering org and open source contributors depend on to build and test TT's AI software stack — orchestrating self-hosted runners on TT hardware for tens of thousands of daily jobs.


Here's a look into what I've built:

- Designed a priority queue system with dynamic resource allocation by implementing Yunikorn (a custom k8s scheduler) that cut wait times for critical CI jobs from over 2 hours down to under 3 minutes
- Built an alert response system using nanoclaw that receives Prometheus/Alertmanager webhooks and autonomously investigates and resolves Kubernetes issues
- Designed it to be fully extensible, so teams can apply it to any cluster by only touching YAML configs and Markdown files, with the codebase structured around skills and agent.md files so anyone can modify it without needing to dig deep into the code