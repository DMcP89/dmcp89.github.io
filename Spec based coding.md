**While I haven't changed my tune on [vibe coding](#vibe-coding-is-not-a-vibe) just yet, one area of AI powered development that seems promising to me is Spec driven development.**

This [article](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-using-markdown-as-a-programming-language-when-building-with-ai/) from Github came across my feed recently and it really peaked my interests. While I have been using LLMs and Agents to supplement my programming work I was still using it mostly as a pair programmer vs handing over controls to them completely. It still felt too risky, too experimental, to use on anything remotely production grade. So the idea of using a spec to introduce some guard rails to the Agents seemed like a novel way to remove some of the risk from the equation. The more I thought about it the more it just made sense. It reminded me of an [old webcomic](https://www.commitstrip.com/en/2016/08/25/a-very-comprehensive-and-precise-spec/?) I used to follow that I would argue first introduced the idea.

![CommitStrip](https://www.commitstrip.com/wp-content/uploads/2016/08/Strip-Les-specs-cest-du-code-650-finalenglish.jpg)
## What is Spec Driven Development

At its core Spec Driven Development is a form of agentic development that relies on carefully created specs instead of prompts to guide the agent through its implementation. A spec can take many forms, the most common I've seen has been Markdown files, but a spec could just as easily be a ticket or an issue in something like JIRA or GitHub provided your agent can access them. Once you have that in place its a similar workflow to any other agentic power workflow, prompt your agent to review the spec and begin its implementation. Once the agent's done its work the spec can either be discarded or folded into your code-base for future work. Specs have to be first class citizens in your code base for this approach to work, drift between spec and implementation can lead to poor results or hallucinations. 

Now you might be thinking to yourself, this sounds like vibe coding with extra steps, but those extra steps are why I find SDD more effective. Building out a spec requires me to actually think critically about what I want implemented. What middle ware should I use for this endpoint, how do I want this function called, what parameters should we require? All these questions that come up while creating a spec don't necessarily arise when in a stream of consciousness with an agent. I've found the results to be more precise and easier to reason about as well, since I wrote the spec I know how its supposed to work, which makes debugging code I did not write myself easier. I think it is a good approach to get the most out of LLM based development while not risking atrophying the skills I've built up over my career. It feels like programming in markdown. Vibe coding will likely always be the top dog in terms of prototyping or POCs, but for my money specs are the way to go for building anything real.

## How I've been using Spec Driven Development

So far I have experimented with spec driven development in two of my open source projects, tinycare-tui and harambot, using two different approaches to spec driven development in each.

For tinycare-tui I've been using GitHub issues as the specs and using GitHub's Copilot as my agent. The agent picks up any issues I assign it and opens a PR with its changes that I can review and eventually merge. I've found this approach is great for small easily defined tasks. Copilot was able to complete the issues assigned to it with little to no intervention on my part. One bottleneck with this approach was having to checkout and test Copilots changes locally. However this is more a mark against my testing suit rather than copilot, if I had proper end to end tests setup I could skip this manual process. I will say the bit I found the most enjoyable about this approach was being able to manage most of the process from the GitHub app on my phone.

<br />
https://github.com/DMcP89/tinycare-tui/issues/4
  
<br />

With Harambot I went with using markdown files for specs and using the Gemini CLI as my agent. Since Harambot is a bit more complex and has a modest user base I wanted to go with something slightly more hands on. I was able to fit this into my workflow rather seamlessly, when I would start to work on a feature instead of opening the relevant python files I would instead start by writing out a specification for the feature in markdown. After all I need is a that a simple prompt to Gemini to review the markdown file and implement the feature. So far I've been storing these specs as artifacts in the projects repo but I think eventually I would like to move to a sort of hybrid approach where the specs are GitHub issues and setting up Gemini CLI with the Github MCP serve so that it can read them from there.


<br />
https://github.com/DMcP89/harambot/blob/release/v1.0.0/.gemini/specs/scoreboard_endpoint.md

<br />
The main pitfall I've found with this approach is a few times as I was writing out a spec I thought to myself "I could have implemented this myself in the time its taken me to write this spec" so you do need to pick and choose where you'll use it.

