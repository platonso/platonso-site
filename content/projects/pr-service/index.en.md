---
title: "PR Reviewer Service"
date: 2025-11-16
description: "An automated service for assigning reviewers to Pull Requests"
tags: ["go", "backend"]

---

[![GitHub - pr-service](https://img.shields.io/badge/GitHub-pr--reviewer--service-blue?logo=github&logoColor=white)](https://github.com/platonso/avito-pr-service)

---

### About the Project

The service addresses the challenge of automatically assigning reviewers when Pull Requests are created. The primary goal is to eliminate manual coordination and accelerate the code review process by automatically selecting reviewers from the author's team.

### Key Features

**Team Management.** Each user belongs to a team. Reviewers are assigned exclusively from the PR author's team, ensuring relevant and contextual reviews.

**Flexible Availability Control.** User activity status allows excluding employees on leave or temporarily unavailable from the reviewer pool.

**Automatic Assignment.** When a PR is created, the service automatically assigns up to two reviewers from the active members of the author's team.

**Reassignment.** If an assigned reviewer cannot participate for any reason, the system allows replacing them with another active member from the same team.

**Analytics.** The service provides statistics on reviewer activity and general Pull Request information to evaluate workload and processes.

### Architectural Decisions

The logic is divided into domain areas:
- Team management
- User management
- Pull Request processing
- Statistics collection

### Tech Stack
- Go 1.22+
- PostgreSQL
- Docker