---
title: "Chat Royale"
description: "A Clash Royale agent powered by a custom built Clash Royale MCP server."
date: "Oct 23 2025"
demoURL: "https://chat-royale.com"
repoURL: "https://github.com/Baighasan/Chat-Royale"
---

![Chat Royale](/chat-royale.png)

Chat Royale is a platform that lets users query Clash Royale data (player stats, clan info, rankings, and more) using natural language, powered by a custom built MCP server.

The stack is three containerized services (MCP server, Express API with MCP client, React frontend) orchestrated with Docker Compose and deployed on AWS Lightsail. The MCP server wraps the official Clash Royale API and exposes it as tools that a Gemini-powered agent can invoke, including multi-step tool-chaining for queries that require output from one tool as input to another.

For a full technical deep-dive, check out the [blog post](/blog/chat-royale).
