# Interactive Portfolio Builder Skill

Un **Agent Skill** réutilisable pour concevoir des portfolios interactifs, gamifiés et soignés (HTML5 / CSS3 / Vanilla JS), combinant :

- **Discipline design Hallmark** : tokens CSS `:root`, animations GPU (`transform` / `opacity` uniquement), contrastes `>= 4.5:1`, `tabular-nums`, `prefers-reduced-motion` et audit `sloplint.mjs`.
- **Architecture interactive & animations sur mesure** : préchargeur avec CSS critique inline, emblème réactif au scroll, chorégraphies **GSAP + ScrollTrigger** personnalisables (avec garde-fous anti-blocage), fenêtres de jeux intégrées avec croix `✕`, boutons `.btn-attention`, visualiseurs 3D `<model-viewer>` (`.glb`), fiches compétences et système de quêtes / XP.
- **CV A4 imprimable & outils carrière** : modale CV prête pour l’impression PDF 1 page (`@media print`), puces d’impact chiffrées, liens cliquables et modèle de lettre de motivation.

---

## Installation rapide

Copiez le dossier `interactive-portfolio-builder/` dans votre répertoire global de skills :

```bash
mkdir -p ~/.gemini/config/skills/interactive-portfolio-builder
cp SKILL.md ~/.gemini/config/skills/interactive-portfolio-builder/SKILL.md
```

*(Compatible également avec `~/.agents/skills/` ou `~/.claude/skills/`.)*

---

## Contenu du dépôt

- [`SKILL.md`](./SKILL.md) — Instructions complètes du skill pour l’agent IA.
- [`interactive-portfolio-builder/SKILL.md`](./interactive-portfolio-builder/SKILL.md) — Structure prête à copier directement dans un dossier `skills/`.

---

## Auteur

**John-Mary AYIVI**  
Portfolio de référence : https://github.com/shinkiflinn-ops/portfolio-pro
