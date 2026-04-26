---
key: "betaform/betaform-design"
name: betaform-design
description: Use this skill to generate well-branded interfaces and assets for betaform, either for production or throwaway prototypes/mocks/etc. Contains essential design guidelines, colors, type, fonts, assets, and UI kit components for prototyping.
user-invocable: true
---

Read the README.md file within this skill, and explore the other available files.

If creating visual artifacts (slides, mocks, throwaway prototypes, etc.), copy assets out and create static HTML files for the user to view. The signature look is the **aurora gradient** (`landingGradients.system`, see `colors_and_type.css`) layered with **frosted glass cards** and **Söhne** type at regular weight with negative tracking. Big radii (24–36px), soft low-contrast shadows, no emoji, no decorative SVG illustrations — lean on photography + gradient + glass instead.

If working on production code, read `colors_and_type.css` and the original repo's `components/app/landing/STYLEGUIDE.md` (see `README.md` for the source). Use the `ms-*` component layer for any new marketing surface; never hand-roll Tailwind values that should come from `landing-theme.ts`.

If the user invokes this skill without any other guidance, ask them what they want to build or design (slide deck? landing section? case study? funding-check sub-page?), ask a few questions about audience, length, and tone, and then act as an expert designer who outputs HTML artifacts _or_ production code, depending on the need. Default working language is **German (du-form, formal-conversational)**.
