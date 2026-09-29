# Phase 5: Brand and entity audit

Goal: one consistent identity for the client everywhere search engines and AI read, and a strong tie between the client and "<category> in <city>". Read-only: claim, edit or submit nothing.

## Brand and NAP

1. **Canonical identity:** the legal name (state business registry), the market's Google profile name, the site's schema name, and the name customers use. Decide one canonical name, address format and phone for the market.
2. **Collect every variation** from: the site's HTML and JSON-LD on key pages, the Tracker answers (`get_tracker_results` shows how each AI names and describes the client), and third-party profiles (Google, Apple Maps, Bing Places, Yelp, Angi, HomeAdvisor, BBB, Yellow Pages, Nextdoor, Facebook, LinkedIn, chamber of commerce, review platforms, industry directories).
3. **Phone register:** list every phone number found with where it appears. Call tracking numbers are expected on the site; wrong or unknown numbers on profiles and schema are not.
4. **Brand collisions:** businesses with the same or similar names, in the market or nearby, that AI or directories could confuse with the client.
5. **Category association:** how strongly the web ties the client to "<category> in <city>". Check whether the client appears in the AI-cited "best <category> in <city>" lists, whether profiles list the category, and whether the market profile's primary category is the category (owner access needed to confirm).

## Entity map

Build the identity card: organizations (parent, acquired companies), people (owners, license holders), credentials (license numbers, their holders and status), locations, offerings, place entities (city, county, neighborhoods, landmarks, utilities, regulators), competitor entities, the official profile set for `sameAs`, and "do not confuse" entities. Finish with a loose-ends table: each item, why it matters, who resolves it, and how. Many need the client or a captcha-protected lookup: log those as handoffs.

## Output

The brand audit template in [templates.md](templates.md): executive summary, findings by severity, a copy-paste "source of truth" pack, a prioritized fix plan (7-day, 30-day, monthly monitoring), the NAP section, collisions, category association and the entity map. Attach it (internal) and log it.
