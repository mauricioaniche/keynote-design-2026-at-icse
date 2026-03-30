# Speaker Notes

These notes follow the current slide order in `index.html`. I reused and adapted the useful parts from `talk.txt`, and for slides without existing notes I added suggested speaking prompts.

## Slide 1 - Designing at Scale: Challenges, Pitfalls, and Lessons Learned

- Open by framing this as a talk about what really hurts when systems become large.
- Say this is based on lessons from industry, not a claim that there is one perfect way to design software.
- Set up the main thesis early: the goal is not perfect design, but design that can survive change.

## Slide 2 - Mauricio Aniche

- Mauricio, CTO and co-founder at Alura.
- Former Uber, Adyen, and Locaweb.
- Former assistant professor in software engineering at TU Delft.
- Mention the personal tension: I still do not know whether I love academia or industry more.

## Slide 3 - We love software design

- Start by aligning with the audience: we love software design, and that is why we often place it at the center of software engineering.
- Say this affection is exactly why it is worth challenging one of our favorite assumptions.
- Use this slide to prepare the room for a less comfortable message.

## Slide 4 - The uncomfortable truth

- Engineers love talking about code quality because code is visible and local.
- But in very large systems, ugly code is often not what hurts most.
- What really hurts is infrastructure, architecture, and data that become hard to move.
- Examples: changing a cache technology, repartitioning a table, evolving storage layout, changing queue semantics, replacing a foundational dependency, migrating stateful systems without downtime.
- The point is not that code does not matter. The point is that, at scale, other things often dominate the pain.

## Slide 5 - Bad code is unpleasant, but survivable

- At scale, code quality is often not the dominant constraint. Architecture, state, and infrastructure are usually harder to change.
- Bad infrastructure or hard architectural boundaries can freeze whole organizations.
- Local messes are often manageable. Global constraints are what trap you.
- Clarify the nuance: this is not "code quality does not matter"; it is "code quality is often not the first thing that kills you."

## Slide 6 - In an agentic world, code is even less of a problem

- AI lowers the cost of reading, understanding, and patching ugly local code.
- But it does not lower the cost of migrating the wrong infrastructure or untangling the wrong architecture.
- If anything, this makes the asymmetry even stronger: local cleanup gets cheaper, systemic mistakes stay expensive.

## Slide 7 - Every code and architectural decision expires

- In large systems, everything is a trade-off.
- No design gives only benefits; every design also buys you a particular kind of pain.
- The hardest part is that you do not have a crystal ball. You are deciding under uncertainty.
- So the real question is not "What is the right architecture?" but "What pain am I choosing today, and how bad will it be when the context changes?"
- Architectural decisions that once looked reasonable later become liabilities.
- Regret is not a sign of incompetence. Regret is the normal outcome of designing in a changing environment.

## Slide 8 - Refactoring at scale

- Refactoring is not cleanup. Refactoring is the main mechanism by which large systems evolve.
- Care less about static judgments like "this code smells" and more about dynamic questions.
- Ask: how do I change this safely, how do I migrate incrementally, and how do I keep the system working while replacing its internals?
- This is where large-scale design becomes an operational discipline, not only a code-reading discipline.

## Slide 9 - The hard part is changing it without stopping the world

- The hard part is not noticing that something is bad.
- The hard part is changing it under uptime requirements, under traffic, and under business pressure.
- This is where design, operations, rollout strategy, and organizational coordination all come together.

## Slide 10 - Story: caching migration at Uber

- Tell the Uber caching migration story here.
- Emphasize that this was not a story about ugly code; it was a story about moving data and behavior safely between technologies.
- Good beats: why the migration was necessary, why "just switch the cache" was misleading, what could go wrong during rollout, and what this taught you about infrastructure-first pain.
- Land the story on the idea that data movement and compatibility are often harder than rewriting code.

## Slide 11 - Refactor safely

- Walk through these techniques as ways to buy safety and reversibility.
- Feature flags let you control exposure and reduce blast radius.
- Shadow traffic lets you compare old and new behavior before real cutover.
- Dual reads and writes help you bridge old and new worlds.
- Rolling upgrades avoid stop-the-world releases.
- Backward-compatible APIs keep teams unblocked while systems evolve.
- Data migration plans matter because data tends to outlive the code around it.

## Slide 12 - Good large-scale code design

- Good large-scale code design is not static elegance.
- It is changeability under load, new information, and business pressure.
- Elegance still matters, but only if it survives contact with production reality.
- Use this slide as the bridge from system design to code-level design.

## Slide 13 - OO is great. Really?

- Acknowledge the bias: I wrote two books on OO, one in Portuguese and one in English.
- Many of us were trained to think that good business software naturally gravitates toward OO-heavy design.
- OO is powerful when you truly need substitution, rich domain behavior, extension points, and flexibility.
- The point here is not to attack OO. It is to question whether it is always the right default.

## Slide 14 - Code challenges in large-scale software systems

- Much of the real work is orchestrating work, enforcing workflow, moving data around, calling services, handling errors, managing concurrency, dealing with authentication and authorization, and navigating ownership boundaries.
- In that world, procedural code is often more direct, cheaper, and more honest.
- OO can add abstraction, indirection, and boilerplate before it buys real value.
- In microservice-heavy systems, explicit error handling and concurrency often matter more than elegant polymorphism.

## Slide 15 - Story: permission management at Uber

- Tell the permission-management story as an example where code design is really about coordination and safety at scale.
- Good beats: many services, fine-grained security, workflow enforcement, ownership boundaries, and the operational cost of getting it wrong.
- Use it to reinforce that large-scale design challenges are often socio-technical and cross-service, not just local code-structure problems.

## Slide 16 - Story: lack of design flexibility at Adyen

- Tell the Adyen counter-example where the lack of the right abstraction had real business cost.
- This is the point where you show you are not saying "abstractions never matter."
- The lesson is: choose abstractions when the pressure is real and evidenced, not because purity says you should.

## Slide 17 - Let's get concrete

- Reset the room: if architecture is uncertain and design decisions age, what should we optimize for instead?
- The goal is not permanence.
- The goal is not purity.
- The goal is not elegance alone.
- The real goal is to make future change less catastrophic.

## Slide 18 - Optimize for reversibility, not timelessness

- Favor designs you can undo, reshape, or replace.
- Get comfortable with half-life designs: today's answer only needs to survive until the next meaningful context shift.
- Reversibility is often more valuable than theoretical timelessness.

## Slide 19 - Make failure visible

- Hidden failure modes are the most dangerous because teams discover them too late.
- Prefer designs that fail loudly, locally, and observably.
- If something will hurt, let it hurt in a way you can detect, localize, and roll back.

## Slide 20 - Treat data and infrastructure as first-class

- Data and infrastructure boundaries deserve first-class design attention because they outlive code fashion.
- This is where migration cost concentrates.
- Spend more design energy here than we usually do.

## Slide 21 - Take the simplest path and do not overengineer

- Take the simplest path that still preserves room to move later.
- The future will prove your predictions wrong eventually, so avoid paying abstraction tax too early.
- Simple is not naive; simple is often the most adaptable starting point.

## Slide 22 - Go for code abstractions only when you have evidence you need them

- Choose abstractions when recurring pressure proves they are needed.
- Abstractions should follow stable variation, not imagined variation.
- Simpler code is easier to refactor when assumptions expire.

## Slide 23 - Be ready to refactor

- Today's optimization may become tomorrow's bottleneck.
- Refactor not too soon, but not too late.
- Design with the migration path in mind, not just the steady state.

## Slide 24 - What's in it for you, researchers?

- Invite the researchers to widen the target beyond code smells.
- Interesting problems here include architectural reversibility, infrastructure migration patterns, large-scale refactoring strategies, and how decisions age as organizations and traffic evolve.
- If we want relevant software engineering research, we need to study where the pain actually is.

## Slide 25 - Get away from the coziness of your research lab :)

- Deliver this as a light provocation, not an attack.
- Encourage more field work, more time inside real production systems, and more contact with industry constraints.
- The affectionate message is that real systems will challenge and improve our theories.

## Slide 26 - A summary

- Every design decision is a trade-off under uncertainty.
- At scale, architecture and infrastructure hurt more than code ugliness.
- Refactoring and migration are the core large-scale design skills.
- At code level, concurrency, error handling, workflow enforcement, and service-to-service communication often matter more than code beauty alone.
- Our abstractions should match the real shape of the work.
- The goal is not perfect design, but reversible and survivable design.
