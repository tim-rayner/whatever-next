# Ubiquitous language

## Glossary

- **world**: The internet as we know it.

## DDD usage policy for agents

- Use glossary terms as the default language for domain code: entities, value objects, aggregates, domain services, domain events, commands, and queries.
- Use the same domain terms in API input/output fields, acceptance criteria, and tests when they represent domain concepts.
- Do not invent synonyms when a glossary term already exists.
- If a required concept has no glossary entry, propose the new term first, then use it consistently after approval.

## Naming guidance

Prefer names aligned to glossary terms:

- `WorldService`
- `WorldId`
- `WorldCreated`

Avoid unapproved synonyms for the same concept:

- `InternetService`
- `GlobalThing`

## Bounded context and translation

- If a term has different meanings across bounded contexts, qualify names and document both meanings in this glossary (for example `BillingWorld` vs `SocialWorld`).
- Keep domain language in the domain layer; map infrastructure or external API terminology at boundaries (anti-corruption layer).
