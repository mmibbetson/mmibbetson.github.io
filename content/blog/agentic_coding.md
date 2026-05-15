+++
title       = "Reflections On Agentic Coding"
date        = 2026-05-15
description = """
TODO
"""
[taxonomies]
tags = ["programming", "ai"]
+++

<!-- TODO: Inject a sense that this will be a somewhat philosophical article -->
I'll state upfront that I'm not pro-LLM. I've never been a _'vibe-coder'_ or a _'prompt engineer'_ or aspired to be anything of the sort. I have many grievances with these tools, and I value programming as a craft to be studied and mastered for the joy it can bring. However, I am also a curious person. I'd like to think I prefer to understand things before I dismiss them; I'm an employee in a capitalist labour market; I'm sometimes very lazy. Suffice it to say that these things, among others, are motivation enough for spending some time familiarising myself with agentic programming tools and toying with some of the technologies involved.

<!-- TODO: Reduce focus on MCPeek as a concrete thing, broad-strokes coverage of the fact that I've build something as credibility but this article will not be about what I built. I need to lay the foundation of what I actually intend to share and where it's coming from. -->

## The Benefits of Agentic Workflows

### Velocity

In the wake of large language models, many people like to emphasise that the important part of being a programmer has nothing to do with typing and everything to do with thinking. There is truth to that statement, but I **enjoy** typing out the code myself. I spent time improving my typing speed and learning a [new keyboard layout](https://colemakmods.github.io/mod-dh/) because it was **fun**. I won't argue that other people need to do this, but it's a valid reason to do something. Agentic code takes a lot of that particular joy out of programming (for me) but, by the same token, it removes the monotony of writing boilerplate I've produced many times before.

If I'm not the one inputting the syntax, I'm also somewhat separated from the direct implementation concerns; the line-by-line decision making of programming is reduced. By shifting these microdecisions off of my shoulders, the number of steps between conceptualising the work and materialising it is reduced. This can help produce and refine a working artifact much faster than if both design and implementation require my full attention.

Supposedly some people use agents to work on multiple problems in parallel. I've been told this works but I simply cannot reproduce this workflow effectively. Either the changes I'm prompting for are iterated on too quickly, (requiring my input intermittently and constantly pulling me between contexts) or the code I'm working on is too interrelated and trying to make parallel changes would result in tedious conflicts. The closest thing I can get to a 'parallel' workflow is reading documentation or reviewing a pull request while my current plan is being executed. Your mileage may vary.

### Design

The greatest benefit of coding agents in my experience has been the emphasised focus on design. When my primary responsibility is to conceptualise, research, and design a given unit of code, and the implementation is mostly automated, I can allocate far more of my attention and time to the correctness of the idea. This exercises the most engaging programming muscles, and can result in equivalent or superior quality work --- so long as I also dedicate a chunk of the freed-up time to verifying the produced code. I regularly spend just as much time verifying that my unit tests are correctly aligned with my acceptance criteria and cover edge cases as I do writing out the initial plan for the code under test.

Trying to compose the available agentic tools into an effective workflow has also incentivised better design practice, because the planning and execution cycles naturally push me toward self-contained abstractions that can be tested in isolation. I find myself designing modules of code in distinct planning sessions, constraining the context only to what new functionality is needed and where it may interface with the boundaries of other modules. This should usually be the goal with module design, but the discipline to plan and design carefully before jumping into implementation is not such an effortless skill that it prevails in the majority of cases.

Having a text-regurgitating homunculus with StackOverflow and GitHub piped into its bloodstream allows me to consider a broader possibility space while designing. I may have biases in what I consider to be viable design for any given scenario, and I can screen that against other perspectives with minimal friction. This often results in clarifying my understanding of the problem at hand and spotting design holes missed due to initial assumptions.

### Comfort

There are many aspects of writing high quality software that are necessary but unsexy. For many programmers, digressing from novel system design or detailed logic to do a security audit is unappealing. For others, performance audits may be similarly unstimulating. I've found that being able to regularly scan source code with an agent to flag potential issues and then investigate based on a breakdown report has improved my consistency in doing the 'boring parts' of my craft.

Alternatively, there are areas of programming I've been interested in familiarising myself with for a long time that I never committed to investing in due to a high perceived barrier to entry. Being able to quickly skim the surface of unfamiliar waters with an agent makes diving in less daunting; I can comprehend more clearly how deep the unknown is without needing to submerge myself. This has helped me decide where to invest my time in learning new things, and I've found myself diving more often than before.

## The Cost of Agentic Workflows

### Financial Cost

As a veritable _'AI skeptic'_ and occasional [Ed Zitron](https://www.wheresyoured.at/) listener/reader, I've been cautious of the financial implications of LLM use. It's widely known that the costs of using these tools is [highly subsidised](TODO) at time of writing (early-mid 2026). This is exacerbated by subscription models [obfuscating token consumption](TODO) further.

To try and get a clearer picture while working on MCPeek, I opted to use [OpenCode Zen](https://opencode.ai/zen) and pay per-token to get clear monitoring on my usage patterns. It disturbed me to find out how rapidly I could burn money and achieve nothing by being slightly unclear on a plan instruction, or getting lazy and prompting the agent to think for me rather than working through an idea in my own head. It would easily have been possible to work through $20.00 in an hour of development using Claude Sonnet 4.5 (I dare not use Opus for fear of its mighty token costs).

I understand that at current prices, the numbers are probably okay for a business to take on and accelerate their competent developers without needing to hire more hands. I don't know how long that will remain true as prices continue to increase, but for the private individual it's already asking a bit much. I don't enjoy the thought of a future where a class of useful programming tools are gated behind corporate funding, though maybe I'm naive and that's always been the case.

### Cognitive Cost

Something that sprouts from having agents available to automate busywork is that more and more busywork appears to replace itself. I'm able to spend hours directing an agent to perform menial tasks that I would typically never prioritise over doing something more productive because the barrier to entry for doing the menial tasks is now so low. This is something that [Cal Newport has covered](todo) when researching on impact of new technologies, and I don't know whether there's an elegant answer to preventing this kind of 'busywork-creep' as we adopt agentic coding further. All the talk of rapid development and greater focus on design doesn't mean much if we're too busy directing our agents to produces reams of under-verified documentation doomed to never be read, or writing follow-up emails to a coworker, or tweaking the templating of a perfectly functional CI pipeline, etc.

The more I adopt and integrate LLMs to 'enhance my thinking', the more I feel my instincts guiding me towards not thinking at all. When my subconscious mind believes it can achieve an outcome without expending energy, it will guide me to do just that. In the deepest depths of my development cycle on MCPeek, I had a constant nagging itch to just prompt the LLM every time I'd begin to summon a complex thought. Although I was driven to offload thinking, that same feeling also held a powerful impetus to _keep going_. When the LLM output signals that I'm producing work, or achieving something, it can become a hedonic cycle of pursuing rewards for "being productive" without actually producing much of value. There's an insidious mental vacancy wrapped in a facade of hyper-efficiency.

## Harm Reduction for the Modern Developer

### Using the Right Tools

Given the negative impacts of programming agentically, it's important to me to wrest control over my workflow; to keep it precisely tailored to my benefit and within my comprehension. For this reason, I avoid the maximalist trap of agentic integrations grafted onto large existing tools. Using small, composable tools to build my workflow keeps separate the responsiblity of the agent and the other tools. Working in an agent [TUI](https://en.wikipedia.org/wiki/Text-based_user_interface) session to plan and iterate on my design, and then opening [Helix](https://helix-editor.com/) separately to review and tweak keeps those acts separate. It incentivises maintaining quality prompts to prevent the agent from needing constant intervention. When all of my tools are sitting in a muddled pile together, defining a clear workflow becomes an act of futility.

Furthermore, if I'm relying on an agent to produce the low level semantics of my program, I need to create an environment that enables me to rely on its output as much as possible. High quality static analysis is critical in enabling LLMs to operate effectively, empowering them to adjust based on structured feedback immediately without reprompting. Languages and toolchains that enable LLMs to derive maximum relevant information statically are more enjoyable and effective to work with this way than those that don't<sup>*</sup>. Languages that have high syntactic consistency are similarly preferable; when there is only one way to write something, all instances of it which appear in the training data will look the same, and therefore the model is more likely to produce something correct than be mislead by arbitrary syntactic or conventional differences.

<!-- TODO: Add styling for github markdown note blocks? Also definitely make these indented quote block things more visually distinct with styling -->
> [!NOTE]
> <sup>*</sup> I name no languages here to avoid coupling an idea to an implementation.

### Governance & Shared Mental Models

A revelation that came to me late in defining my workflow for MCPeek was that the pace I can produce code for a project at times exceeds my capacity to hold the full context of the project in my mind. I've opted to implement a simple design decision record pattern into my PR process, whereby all commits are reviewed and a brief structured markdown document is produced that preserves the context and motivation for the changes, the affected surface area, and why particular decisions were made in the implementation & design. The LLM can be leveraged to produce this document for review quite easily, as it should have context on the changes from all of the planning and execution in the current session. I feel much more comfortable that the evolving gestalt concept of a software project is derivable from information available at any time in version control, especially as the amount of work produce climbs higher than my context ceiling. This is not a refined approach, but I believe it grasps at something important for maintaining a degree of comprehension that's necessary for building good software.

### Budgeting Your Resources

A prevailing concern among people I respect regarding LLM-produced code is that code quality is being sacrificed for convenience. A large part of finding a workflow that I considered acceptable involved ensuring that my intentions for design and implementation are translated clearly and effectively into to the resulting code. I **cannot emphasise enough** that rigorous, intentional, clear articulation of design parameters is a prerequisite for producing anything of value with coding agents. Rapidly promptng and reprompting in a barely-conscious cycle, blindly grasping for the right thing without knowing where I'm aiming is a hallmark that I'm not actually making anything useful. This might seem self-evident, but I know I'm not the only person that falls into this pattern --- it's just so much easier than thinking deeply.

Much like my mental energy, my finances are a limited resource best spent in the planning and design portion of agentic programming: Using a higher quality model to ensure maximum quality of the implementation plan and acceptance criteria makes it feasible to use cheaper models for the execution; if the plan is precise and rigorous enough, the actual implementation phase for many scenarios can be a very mechanical and well-defined task without much disambiguation. There have been some novel techniques found to save costs on prompts by reducing the number of tokens in the models' output, like the [caveman](https://github.com/JuliusBrussee/caveman) skill<sup>*</sup>. So long as relevant information is consistently retained while truncating responses to only the bare essentials, this is an unintrusive cost-saving measure that's entirely within my control to tweak and adjust over time. As for methods that reduce input tokens, I reject this idea as the most of the important work to be done in using an agent involves the quality of your input. Besides, the cost is much heavier on output than input.

> <sup>*</sup> Please do not import a dependency through a package manager to integrate a markdown file into your workflow. Just copy the skill into your own configuration and adjust as necessary.

## Reflection

<!-- TODO: ive digressed into a more technical discussion in the last bit, i need to create an appropriate bridge for the emotional/psychological stakes that i plan to end all of this on -->
The last thing I've come to believe that I want to mention here is that if I'm going to be working with agentic coding regularly and I care about programming as a craft, about being an intentional creator, then I need to have a hobby project I can work on regularly without using any of this generative tooling. It's one thing to be familiar and historically proficient in a skill, it's another to get my hands dirty regularly and remain current with that skill. Something as simple as inputting the correct syntax is still a skill that will decay without exercise; to keep moving forward, it's sometimes necessary to look back and remember how I got to where I am.

My thoughts & feelings on agentic programming and LLMs in general are still very mixed. I've been able to make good use of the technology to learn, grow, and build useful software rapidly. But there's a subtle dread that I just can't seem to shake. I feel I might be losing something I'm not able to precisely identify. I get the sense that a lot of people around me are feeling the same way.

Maybe I'll have a word for when the tools I have now become too expensive to continue using and I have to contend with the state of programming post-bubble-burst.
