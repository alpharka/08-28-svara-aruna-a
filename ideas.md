# Svara & Aruna — Design Direction

## Three stylistic approaches

### Theme Name: Modern Javanese Editorial
Very brief intro: A quiet, tactile editorial invitation inspired by batik geometry, rice-paper texture, and contemporary Indonesian print design. Warm, intimate, and ceremonial without feeling ornate.
Probability: 0.07

### Theme Name: Coastal Airy
Very brief intro: A sun-washed invitation shaped by sea glass, linen, and late-afternoon light. Relaxed, luminous, and spacious with an easy destination-wedding mood.
Probability: 0.03

### Theme Name: Botanical Nocturne
Very brief intro: A moonlit garden composition with ink-black grounds, pressed foliage, and restrained metallic accents. Poetic and cinematic, with a more dramatic emotional register.
Probability: 0.08

## Chosen approach: Modern Javanese Editorial

### Design Movement
Contemporary Indonesian editorial design with references to Javanese batik parang rhythm, letterpress stationery, rice-paper tactility, and museum-catalogue composition.

### Core Principles
1. Ceremonial restraint: let spacing, rule lines, and material texture create richness instead of decorative excess.
2. Asymmetric storytelling: use offset columns, vertical annotations, and editorial pacing rather than a stack of centered cards.
3. Honest warmth: pair a deep earthy field with soft parchment and a single copper accent so the experience feels personal, not corporate.
4. Quiet movement: reveal content like turning printed pages—slow entrances, gentle parallax, and tactile hover feedback.

### Color Philosophy
The visual world uses ink-black brown for depth, parchment for memory and paper, muted clay for human warmth, and a restrained copper accent for ceremony. The signature brand color is **Svara Copper** (#B86B4B), an ownable terracotta-metal tone that feels like hand-burnished foil on a wedding program.

### Layout Paradigm
A scrollable editorial folio: each chapter is anchored by a left-side section index, offset text blocks, and framed image moments. On desktop, the page alternates between a narrow annotation rail and a generous content field; on mobile, the rail becomes compact eyebrow metadata.

### Signature Elements
- Fine copper registration rules and small chapter numerals.
- A visible circular S/A monogram seal with a broken ring, used as the primary emblem.
- Subtle rice-paper grain and batik-inspired diagonal micro-patterns behind major transitions.

### Interaction Philosophy
Interactions should feel like handling stationery. Buttons use crisp press states and copper ink shifts, inputs gain a deliberate underline, and lightbox transitions feel like lifting a photograph from an album. No interaction should feel loud or gamified.

### Animation
Use transform and opacity only. Reveal headings, body copy, event rows, and gallery tiles with a 30–70ms cascade as they enter view. Let the cover seal drift by a few pixels and let the copper registration line draw in once. Keep ordinary transitions under 240ms and disable non-essential motion under `prefers-reduced-motion: reduce`.

### Typography System
Display: Cormorant Garamond, using italic and semibold contrast for names and chapter titles. Body: DM Sans, with compact uppercase labels and generous line-height for longer copy. Use no more than these two families.

### Brand Essence
Svara & Aruna is an intimate digital wedding folio for guests who value the small details—the story, the place, and the promise—presented with Indonesian editorial character. Personality: **tactile, poised, affectionate**.

### Brand Voice
Headlines are concise and literary; CTAs are warm and direct; microcopy is gracious without being generic. Example lines: “Dua arah, satu rumah.” and “Simpan tanggalnya, lalu hadirkan doamu.”

### Wordmark & Logo
The emblem is a broken circular seal containing a custom S/A ligature: the S forms the outer sweep while a single diagonal A stroke crosses the seal like a registration mark. The wordmark pairs a high-contrast serif “Svara” with a small tracked “ARUNA” caption rather than using the couple names in a default font.

### Signature Brand Color
Svara Copper — #B86B4B.

## Style Decisions

- Use a light parchment editorial field with deep ink-brown sections; do not use purple gradients, neon glow, or generic wedding-template cards.
- Keep the primary cover visually distinct from the intro: cover is a dark ceremonial seal, intro is a warm editorial spread.
- Treat all guestbook content as user-generated plain text and never seed it with fabricated wishes.
- Use placeholder couple and event information centrally in one CONFIG object so replacements are straightforward.

## Style Decisions

- The hero now uses a visible vertical annotation rail and a copper registration rule so the cover and intro read as a folio rather than a generic centered landing page.
- The S/A identity is rendered as an inline broken-ring ligature mark with a continuous S sweep and diagonal A registration stroke.
- Parang-inspired diagonal rhythm is repeated as a restrained transition pattern in the story and tanda kasih chapters.
- Copper is used as a consistent editorial punctuation system across the emblem, rules, numerals, links, and action states.
- Copy keeps the Indonesian editorial voice concise, literary, affectionate, and gracious.
