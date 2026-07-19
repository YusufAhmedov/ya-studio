# Human gates — when to ask the human

Agents are autonomous within the agreed scope, but on three classes of decisions they
must behave differently. The coordinator holds these gates; an executor that hits a
gate returns the question to the coordinator (it does not ask the human directly).

## 🔴 MUST ask the human
Stop and wait for an explicit decision:
- Publishing outward: pushing to Figma Community, sharing the file, posting to a
  portfolio, social posts.
- Money: connecting paid services, plans, paid generations.
- Secrets & access: Figma PAT, tokens, API keys — never print values, never commit them.
- Product scope change: what we promise the user, the audience, privacy, price.
- Irreversible: deleting/overwriting someone else's Figma files or pages, others' artifacts.

## 🟡 SHOULD confirm
Propose an option with a recommendation, but wait for confirmation:
- Feature prioritization (what's Must, what's Should).
- Visual style and brand tone, choice of references.
- Naming of the product, screens, key entities.
- Architectural forks that are expensive to change later.

## 🔵 Agent decides
Act without asking, recording anything significant in the decision-log:
- Small details within the agreed scope and style.
- Picking a specific library component for an obvious task.
- Layer names, section order, technical build details.

> If unsure which class a decision belongs to — treat it as the stricter one and ask.
> Asking is cheaper than redoing.
