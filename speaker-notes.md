# Speaker Notes

These notes follow the current slide order in `index.html`.
The current deck revision groups slide backgrounds by narrative section; slide order and core speaking points remain the same.

## Slide 1 - Designing at Scale: Challenges, Pitfalls, and Lessons Learned

- Open by framing this as a talk about what really hurts when systems become large and long-lived.
- Say this is based on lessons from industry, not a claim that there is one perfect way to design software.
- Set up the main thesis early: the goal is not perfect design, but design that can survive change.

## Slide 2 - Maurício Aniche

- Maurício, CTO and co-founder at Alura.
- Former Uber, Adyen, and Locaweb.
- Former assistant professor in software engineering at TU Delft.
- Mention the personal tension: I still do not know whether I love academia or industry more.

## Slide 3 - What do I mean by scale?

- Define scale explicitly so the audience knows this is broader than just request volume.
- Say scale means traffic, uptime expectations, lots of state and data, many teams and services, ownership boundaries, regulatory pressure, and systems that must keep evolving for years.
- This matters because each of those dimensions makes change harder in a different way.

## Slide 4 - We love software design

- Start by aligning with the audience: we love software design, and that is why we often place it at the center of software engineering.
- Say this affection is exactly why it is worth challenging one of our favorite assumptions.
- Use this slide to prepare the room for a less comfortable message.

## Slide 5 - The uncomfortable truth

- Engineers love talking about code quality because code is visible and local.
- But in very large systems, ugly code is often not what hurts most.
- What hurts most is usually architecture, infrastructure, and data that become hard to move.
- Examples: changing a cache technology, repartitioning a table, evolving storage layout, changing queue semantics, replacing a foundational dependency, migrating stateful systems without downtime.
- Clarify the nuance: this is not "code does not matter"; it is "other forces often dominate the real cost of change."

## Slide 6 - Every code and architectural decision expires

- In large systems, everything is a trade-off.
- No design gives only benefits; every design also buys you a particular kind of pain.
- The hardest part is that you do not have a crystal ball. You are deciding under uncertainty.
- So the real question is not "What is the right architecture?" but "How will this age, and what pain am I choosing when the context changes?"
- Regret is not a sign of incompetence. Regret is the normal outcome of designing in a changing environment.

## Slide 7 - Story: caching migration at Uber

- Tell the Uber caching migration story here.
- Emphasize that this was not a story about ugly code; it was a story about moving data and behavior safely between technologies.
- Good beats: why the migration was necessary, why "just switch the cache" was misleading, what could go wrong during rollout, and what this taught you about infrastructure-first pain.
- Land the story on the idea that data movement and compatibility are often harder than rewriting code.

## Slide 8 - Refactor safely

- Refactoring at scale is not cleanup. It is the main mechanism by which large systems evolve.
- Walk through these techniques as ways to buy safety and reversibility.
- Feature flags let you control exposure and reduce blast radius.
- Shadow traffic lets you compare old and new behavior before real cutover.
- Dual reads and writes help you bridge old and new worlds.
- Rolling upgrades avoid stop-the-world releases.
- Backward-compatible APIs keep teams unblocked while systems evolve.
- Data migration plans matter because data tends to outlive the code around it.

## Slide 9 - The hard part is changing it without stopping the world

- The hard part is not noticing that something is bad.
- The hard part is changing it under uptime requirements, under traffic, and under business pressure.
- This is where design, operations, rollout strategy, and organizational coordination all come together.

## Slide 10 - Time is part of the design

- Make explicit that large-scale design is not only about structure; it is also about time.
- Schema evolution, deprecation windows, backfills, retries, and dual writes are design concerns, not operational afterthoughts.
- Stress that many systems look fine in the steady state and fail during the transition period.
- If the audience remembers one phrase here, it should be: migration paths are part of the architecture.

## Slide 11 - Socio-technical design matters

- Say clearly that team structure is part of system design whether we like it or not.
- Team boundaries shape architecture, ownership affects change speed, and Conway's Law is a daily operational reality.
- Decision-making processes can also make changes fast or slow, even when the technical solution is obvious.
- Many migrations fail organizationally before they fail technically: no owner, no aligned teams, no shared compatibility window, no migration budget.
- This helps the audience see why large-scale design is never only about code or diagrams.

## Slide 12 - Good large-scale code design

- Use this slide as the bridge from system design to code-level design.
- Good large-scale code design is not static elegance.
- It is changeability under load, new information, and business pressure.
- Elegance still matters, but only if it survives contact with production reality.

## Slide 13 - If changeability is the goal, what should code optimize for?

- Use this as an explicit transition, because the previous part of the talk was mostly about systems and migrations.
- Ask the room to shift from "What architecture wins?" to "What coding style makes future change cheaper?"
- This sets up the OO discussion as a consequence of the main thesis, not as a separate opinion.

## Slide 14 - OO is great. Really?

- Acknowledge the bias: I wrote two books on OO, one in Portuguese and one in English.
- Many of us were trained to think that good business software naturally gravitates toward OO-heavy design.
- OO is powerful when you truly need substitution, rich domain behavior, extension points, and flexibility.
- The point here is not to attack OO. It is to question whether it is always the right default.

## Slide 15 - Code challenges in large-scale software systems

- Much of the real work is orchestrating work, enforcing workflow, moving data around, calling services, handling errors, managing concurrency, dealing with authentication and authorization, and navigating ownership boundaries.
- In that world, procedural code is often more direct, cheaper, and more honest.
- OO can add abstraction, indirection, and boilerplate before it buys real value.
- In microservice-heavy systems, explicit error handling and concurrency often matter more than elegant polymorphism.

## Slide 16 - Story: permission management at Uber

- Tell the permission-management story as an example where code design is really about coordination and safety at scale.
- Good beats: many services, fine-grained security, workflow enforcement, ownership boundaries, and the operational cost of getting it wrong.
- Use it to reinforce that large-scale design challenges are often socio-technical and cross-service, not just local code-structure problems.

## Slide 17 - This is not permission to write sloppy code

- Slow down a little here to remove the most obvious misreading of the talk.
- Say that readable, testable, disciplined code still matters a lot.
- The point is not that local code quality is irrelevant; the point is that it is only one part of large-scale design.
- Bad code still hurts. It is just often easier to repair than a bad boundary, a bad migration path, or the wrong data decision.

## Slide 18 - Story: code flexibility at Adyen

- Tell the Adyen counter-example where the lack of the right abstraction had real business cost.
- This is the point where you show you are not saying "abstractions never matter."
- The lesson is: choose abstractions when the pressure is real and evidenced, not because purity says you should.

## Slide 19 - Let’s get concrete

- Reset the room: if architecture is uncertain and design decisions age, what should we optimize for instead?
- The goal is not permanence.
- The goal is not purity.
- The goal is not elegance alone.
- The real goal is to make future change less catastrophic.

## Slide 20 - Optimize for reversibility, not timelessness

- Favor designs you can undo, reshape, or replace.
- Get comfortable with half-life designs: today's answer only needs to survive until the next meaningful context shift.
- Reversibility is often more valuable than theoretical timelessness.

## Slide 21 - Make failure visible

- Hidden failure modes are the most dangerous because teams discover them too late.
- Prefer designs that fail loudly, locally, and observably.
- If something will hurt, let it hurt in a way you can detect, localize, and roll back.

## Slide 22 - Treat data and infrastructure as first-class

- Data and infrastructure boundaries deserve first-class design attention because they outlive code fashion.
- This is where migration cost concentrates.
- Spend more design energy here than we usually do.

## Slide 23 - Take the simplest path and do not overengineer

- Take the simplest path that still preserves room to move later.
- Predictions age quickly, so avoid paying abstraction tax too early.
- Simple is not naive; simple is often the most adaptable starting point.

## Slide 24 - Be ready to refactor

- Today's optimization may become tomorrow's bottleneck.
- Do not blame the past, learn from it.
- Refactor not too soon, but not too late.

## Slide 25 - What’s in it for you, researchers?

- Invite the researchers to widen the target beyond classic code-quality conversations.
- Frame the opportunity at a higher level: study software as something that changes over time, not only as a static artifact.
- Encourage the audience to include data, infrastructure, operations, and team structure in their models of software systems.
- Emphasize decisions, trade-offs, and how they age, not only local properties of code.
- The research contribution can be theory, empirical work, tools, methods, or measurement, as long as it helps us understand or improve real change.
- If we want relevant software engineering research, we need to study where the pain actually is.

## Slide 26 - Bring research closer to production reality

- Deliver this as an invitation, not an attack.
- Encourage more field work, more time inside real production systems, and more contact with operational constraints.
- The affectionate message is that real systems will challenge and improve our theories.

## Slide 27 - A summary

- Scale is multi-dimensional: traffic, data, uptime, teams, services, regulation, and time.
- The hardest design problems are often architectural, infrastructural, data-heavy, and organizational.
- The only certainty is that today's decisions will age, and refactoring will eventually be necessary.
- Time, rollout, ownership, and compatibility are part of the design itself.
- Code should stay simple, disciplined, and shaped by real pressure.
- The goal is not timelessness, but reversible and survivable systems.
- After the last summary point, let the contact panel appear on the right and close by inviting people to continue the conversation by email or on Twitter.
