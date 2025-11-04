---
title: "Chat Royale"
description: "A Clash Royale agent powered by a custom built Clash Royale MCP server."
date: "Oct 23 2025"
demoURL: "https://chat-royale.com"
repoURL: "https://github.com/Baighasan/Chat-Royale"
---

![Chat Royale](/chat-royale.png)

Chat royale is a platform that allows users to view data from the Clash Royale servers using natural language queries, powered by a custom built Clash Royale MCP Server.

It allows users to ask questions about things like players stats, clan stats, rankings, and more.


### Overview and Motivation

I started exploring MCP technology around the time Anthropic first released it, so it was quite a new technology at the time. Somewhere I read that one use case for MCP was to kind of wrap API endpoints and allow LLMs to use those endpoints and actually "do" things and access stuff outside of its little bubble. I knew that a Clash Royale API existed and I thought it would be pretty cool (and funny) to learn how MCP works by building mine around Clash Royale.

Initially the goal with this was to just learn how MCP works, but I eventually decided to build it out into a full end-to-end website to showcase the technology, which is the final result you see today!

### Technical Architecture

The project consists of 3 services running in their own containers. All 3 of the containers are orchestrated using a docker compose file. The 3 services consist of the MCP server, the backend API (which includes the MCP client), and the frontend. I've made a simple drawing showing this off below.

![Architecture](/architecture.png)

So as you can probably tell, its a pretty simple architecture. Is having each service its own container overkill? Probably, yeah. This could easily be made as a monolith system with the MCP server running on the same machine as the API and frontend, and communicating via stdio. I primarily chose to go with this approach more to learn how to develop and deploy with Docker rather than as a technical design choice. It did come with some interesting challenges along the way, which helped me learn a lot about how to build with containers.

### Building the MCP Server

So I'm not gonna sugarcoat it, building the MCP server was not too difficult. The documentation was straightfoward to follow and creating tools is as simple as adding a decorator on top of a function and writing what you want the tool to do. 

The hardest part of writing a tool is the prompt engineering aspect. That is, writing the function name and especially description in a way that the LLM can easily understand when and how to use the tool. The description needs to explain what the tool is for, clearly explain what each parameter is, and also any other context it needs to know. 

Some tools within the the Clash Royale MCP server actually require the output of other tools. For example, to get the top players on Path of Legends* within Canada, the LLM would first look at the description for the get_location_path_of_legends_player_rankings tool and read that it needs to get the location id from the get_locations tool. It would then get the location id for Canada by executing the respective tool, and using the relevant part of the output to provide the correct parameters to the path of legends tool. This flow is detailed below.

![Tool-Chaining](/tool-chaining.png)

This is what I ended up calling "tool-chaining" when developing. I'm not actually sure what the proper terminology is, but I think it suits it well. 

You can actually extend this example even further if you wanted to. Let's say you wanted to get the stats of the top player on Path of Legends in Canada. Then the LLM would have to first go to the path of legends locations tool, reason that it has to get the location id for Canada using a different tool, execute the path of legends tool, then finally find the tool for player stats and grab that. I think this really demonstrates the power of tool-chaining and what it can enable LLMs to do.

*For non Clash Royale Players, Path of Legends is a Ranked mode

### Containerizing The MCP Server

Testing the MCP server was a bit of a problem. Since I was developing in Python with virtual environments, when I ran the server locally, it worked as expected. However, when attending to add the server to Claude Desktop (At the time this was one of the only apps that supported MCP), the app would try and spin up the server but would fail because the dependencies were not installed locally. Now, I didn't want to install all the dependancies globally, but I also couldn't get it to run the server within a venv (which makes sense since venv should be used for development).

To solve this problem, I looked at how the GitHub MCP server was built, since I could get that working on Claude Deskop. Turns out, all they did was run it in a container using Docker. I knew about containerization in theory, but had never actually used Docker. So, I containerized my server and it worked perfectly!

![Docker-Container](/docker-container.png)

This is actually a perfect example of the problem Docker, or containerization I should say, solves. I quite literally had the classic "It works on my machine" problem, but instead of "machine" it was environment.

### MCP Client, Transport Layers, and Express API



### Frontend Development



### Deployment & DevOps



### Key Learnings



### What's Next

