# L'ORÉE — Spa & Bien-être

Site web du spa **Maison L'Orée** (Paris VIIIᵉ), porté vers **Next.js** à partir
de la maquette générée avec Claude Design.

Page unique, bilingue (FR/EN), avec :

- Hero plein écran, animations d'entrée au scroll et parallax (GSAP / ScrollTrigger)
- Sections soins, beauté & fitness, espaces bien-être, horaires, footer
- Menu plein écran, bascule de langue FR/EN (mémorisée en `localStorage`)
- Modale de **réservation** en plusieurs étapes (avec calendrier)
- Modale **boutique** avec panier en direct

## Stack

- [Next.js 15](https://nextjs.org/) (App Router) + React 19
- [GSAP](https://gsap.com/) (ScrollTrigger) pour le parallax
- Polices Google via `next/font` (Bodoni Moda, Cormorant Garamond, Jost)
- CSS global classique (aucun framework UI), images depuis Unsplash

## Démarrer

```bash
npm install
npm run dev      # http://localhost:3000
```

Autres commandes :

```bash
npm run build    # build de production
npm run start    # sert le build de production
npm run lint     # ESLint (next/core-web-vitals)
```

## Structure

```
app/
  layout.jsx      # <html>, polices next/font, métadonnées
  page.jsx        # rend <App />
  globals.css     # tout le style du site
components/
  App.jsx         # composant racine (état, langue, modales, scroll)
  Nav.jsx         # Header, MenuOverlay, LanguageToggle, StickyCTA
  Sections.jsx    # Hero, Intro, TreatmentGrid, Wellbeing, CtaBlock, Hours, Footer
  ui.jsx          # primitives (Logo, Button, Reveal, Img, icônes…)
  BookingModal.jsx
  BoutiqueModal.jsx
lib/
  content.js      # contenu bilingue FR/EN + URLs des images
  useParallax.js  # hook parallax GSAP
design-reference/ # maquette d'origine Claude Design (référence, non utilisée par l'app)
```

## Notes sur le portage

- Le **panneau « Tweaks »** de Claude Design (typo, couleur d'accent, mise en page
  ajustables en direct) dépendait du protocole iframe de l'outil de design ; il a
  été retiré. Ses valeurs par défaut sont appliquées directement
  (police titres *Bodoni Moda*, accent `#B89B6E`, hero centré, cartes minimales).
  Les variantes correspondantes restent présentes dans le CSS si besoin de les
  réactiver.
- Les images proviennent d'Unsplash via `<img>` avec dégradé de repli en cas
  d'erreur de chargement. `images.unsplash.com` est autorisé dans
  `next.config.mjs` pour une éventuelle migration vers `next/image`.
- La maquette d'origine (HTML + JSX chargés via Babel dans le navigateur) est
  conservée dans `design-reference/`.
