---
company: "Tenstorrent"
role: "Platform Engineer"
dateStart: "01/05/2026"
dateEnd: "Present"
---

At Tenstorrent, I worked on the CI/CD infrastructure (Kubernetes + ARC) that the entire engineering org and open source contributors depend on to build and test TT's AI software stack — orchestrating self-hosted runners on TT hardware for tens of thousands of daily jobs.


Here's a look into what I've built:

- Designed a priority queue system with dynamic resource allocation by implementing Yunikorn (a custom k8s scheduler) that cut wait times for critical CI jobs from over 2 hours down to under 3 minutes
- Built an alert response system using nanoclaw that receives Prometheus/Alertmanager webhooks and autonomously investigates and resolves Kubernetes issues
- Expanded CI from a single k8s cluster serving jobs to an active-active, multi-cluster architecture enabling high availability and automatic failover
