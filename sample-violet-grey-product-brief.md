# Illustrative Product Brief: Beauty Recommendations and Bundles

> **Portfolio sample — reconstructed, not an original FARFETCH or Violet Grey document.**
> This brief uses public-safe retrospective context. Proposed requirements, assumptions, acceptance criteria, and measurement ideas below are illustrative examples created for this portfolio; they are not confirmed historical specifications or delivered results.

## Verified retrospective context

- Violet Grey was an acquired beauty e-commerce business.
- The product work connected its beauty catalog to the FARFETCH marketplace while considering the standalone business experience.
- The work established an initial personalized recommendation and bundled-purchase capability for cross-sell and upsell, with a baseline for future evaluation.
- No verified conversion, average order value, or revenue lift is claimed here.

## Illustrative problem statement

Customers browsing fashion and beauty products may benefit from relevant beauty recommendations and a clear way to add complementary items to a purchase. The experience should feel useful, preserve product context, and fit the marketplace purchase journey.

## Illustrative objective

Help customers discover relevant beauty products and understand bundle options during marketplace shopping, while giving the business a measurable starting point for future iteration.

## Example users and needs

- **Marketplace shopper:** “When a beauty item is relevant to what I am viewing, help me discover it without disrupting my shopping flow.”
- **Beauty shopper:** “Help me understand which products can be purchased together and what is included.”
- **Commerce team:** “Give us a consistent way to present eligible recommendations and bundles and evaluate customer response.”

## Illustrative scope

- Display relevant beauty recommendations in an agreed marketplace placement.
- Show bundle contents and price information clearly when a bundle is available.
- Support adding an eligible product or bundle to the existing basket flow.
- Provide a graceful fallback when no relevant recommendation or bundle is available.

## Example acceptance criteria

1. A recommendation is shown only when eligible catalog items and required presentation data are available.
2. Each recommendation opens the correct product detail page and preserves the customer's shopping context.
3. A bundle clearly identifies its included items and price before the customer adds it.
4. Adding an item or eligible bundle uses the marketplace basket flow and provides confirmation.
5. Empty, unavailable, or incomplete recommendation data does not block browsing or checkout.
6. The experience has an agreed event plan so exposure and customer actions can be evaluated.

## Illustrative measurement plan

These are proposed metrics for a sample plan, not historical results:

- Recommendation exposure and click-through rate
- Product detail visits from recommendation placements
- Bundle selection and add-to-basket rate
- Downstream conversion and average order value, interpreted with a comparison method
- Guardrails: page performance, basket errors, and checkout completion

Before interpreting results, define event names, eligibility rules, baseline period, attribution window, and comparison approach with Data and Engineering.

## Risks and questions to resolve

- How should recommendation relevance be defined and reviewed?
- Which products are eligible for bundles, and how are price and availability kept accurate?
- Where can recommendations appear without cluttering the shopping journey?
- How should the standalone Violet Grey experience behave when marketplace inventory or presentation differs?
- What operational owner handles catalog data quality and product availability?

## Product approach

Start with a limited, clearly defined placement and eligible assortment. Validate the customer journey and data quality, instrument the experience, then use the baseline to inform subsequent iterations.

## Evidence boundary

The retrospective statements above describe the case at a high level. All detailed product choices in this sample are illustrative and must not be read as the original historical PRD, architecture, or final implementation.
