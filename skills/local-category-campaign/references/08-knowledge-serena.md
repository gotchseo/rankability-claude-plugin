# Phase 8: Knowledge base and Serena

Goal: the client's Rankability knowledge base holds the verified campaign facts, so Serena, Copywriter and every agent write from the same truth.

## Steps

1. `list_client_sources` and read the existing sources that matter (`get_client_source`): entity record, business profile, offers, brand voice, customer language. **Update matching sources by id; never create duplicates.** Create a new source only when nothing covers the topic (for example market competitors, local context for the city).
2. Only verified facts go into selected (in-use) sources: canonical name, address and phone for the market, licenses and their holders, services, guarantees, financing, differentiators, the category-in-city positioning, and content rules. Unverified items stay out or are labeled.
3. Campaign documents (audits, gap lists, benchmarks) can be stored as sources that are **not selected**, so they're available for reference but don't drive generated content. Sources have a size cap; split long documents by section rather than truncating.
4. Show the user the exact changes (source, field, before and after) and get approval before `update_client_source` or `create_client_source`. Log the source ids in the campaign.
5. **Check Serena.** Ask `consult_serena` 3 to 5 questions whose answers you know from the verified facts, including one trap question with a plausible wrong premise. Confirm Serena answers from the knowledge base and doesn't invent facts. Log the result.
