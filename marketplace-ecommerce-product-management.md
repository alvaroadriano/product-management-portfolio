# Violet Grey Marketplace Integration — FARFETCH

**Role:** Senior Product Manager, Growth Product work  
**Period:** March 2023–May 2025  
**Focus:** Beauty marketplace integration, discovery, personalized recommendations, bundled purchases

## Executive summary

After FARFETCH acquired Violet Grey, I owned product strategy and roadmap work for connecting its U.S. beauty e-commerce business to the FARFETCH marketplace while supporting its standalone storefront. I translated business and customer needs into product requirements, user stories, backlog priorities, and delivery coordination across Engineering, Design, and Data. The work established personalized recommendations and bundled purchasing as cross-sell capabilities.

## Context and product challenge

Violet Grey had a distinct beauty assortment and standalone e-commerce experience. The product challenge was to connect beauty products to FARFETCH’s marketplace and shopping journey while preserving the acquired business’s standalone experience. Customers needed recommendations to feel relevant to the products and context they were viewing; an irrelevant module could add clutter without helping discovery.

## My role

I owned product strategy, roadmap direction, requirements, user stories, and backlog priorities for the Violet Grey marketplace integration and related growth work. I worked with Engineering, Design, and Data to define product details, clarify dependencies, and coordinate delivery. I also supported stakeholder alignment and Agile delivery activities.

Related commerce work included coordinating Apple Pay / one-click payment and logistics integrations with backend engineering. These were part of the broader commerce scope and are not presented as measured outcomes of the recommendation and bundle capability.

## Product decision: relevance before placement

We established a rule for the recommendation experience: show the module only when a relevant recommendation was available. If the system could not provide a relevant item, the module would not be displayed. This kept the experience focused on useful discovery instead of filling space with generic cross-sell content.

This decision shaped the product requirements and the collaboration with Data and Engineering around recommendation availability and presentation.

The decision traded potential placement volume for relevance: the module was useful only when it had a suitable item to show. That gave the team a clear behavior for the no-recommendation case without claiming an algorithm or ranking model I did not own.

## Product scope

- Connect Violet Grey’s beauty catalog to the FARFETCH marketplace experience.
- Support personalized recommendations based on customer or product relevance.
- Enable customers to purchase eligible items together through bundles.
- Preserve the standalone storefront needs of the acquired business.
- Coordinate requirements and dependencies across product, data, design, and engineering.

## How I approached it

- **Balanced marketplace and standalone needs:** considered shared marketplace discovery alongside Violet Grey’s existing storefront.
- **Translated strategy into delivery:** converted the product direction into requirements, user stories, and prioritized backlog work.
- **Used relevance as a quality bar:** avoided rendering a recommendation module when no relevant item was available.
- **Coordinated cross-functional dependencies:** worked with Engineering, Design, and Data, including backend teams for adjacent payment and logistics integrations.

## Outcome and evidence

The marketplace integration established an initial personalized recommendation and bundled-purchase capability, and initial conversions were observed after launch. I do not have a verified baseline, attribution method, or result dataset to quantify the effect or attribute conversion lift to this work. The defensible outcome is the product capability delivered and its initial customer response.

For a follow-up iteration, I would instrument eligible recommendation exposures, clicks, add-to-basket actions, bundle attachment, and downstream conversion, with page performance and checkout completion as guardrails. The [illustrative product brief](sample-violet-grey-product-brief.md) shows a proposed measurement plan; those measures are not historical results.

## What I learned

A recommendation feature needs a clear fallback for when relevance is absent. Suppressing a low-quality placement can protect the customer journey while creating a better foundation for future measurement and iteration. In an acquisition, the product experience also needs to respect what the standalone business still requires.

## What this demonstrates

- Product strategy and roadmap ownership in an acquired-business context
- Marketplace and e-commerce integration
- Personalized discovery and cross-sell product thinking
- Product requirements, user stories, and backlog prioritization
- Cross-functional delivery with Engineering, Design, and Data

## Evidence note

This public case summarizes my contribution and verified product direction. It excludes confidential analytics, customer data, internal roadmaps, and proprietary implementation details. The recommendation relevance rule is described at a product level; no algorithm or architecture is claimed.
