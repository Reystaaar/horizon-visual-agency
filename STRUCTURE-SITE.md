# 🗺️ Cartographie du site — Horizon Visual Agency

> Fichier de référence : il relie chaque élément du site à ce qui en dépend.
> **Avant toute modification, consulter la section concernée pour voir ce qui est relié.**
> Mis à jour au fur et à mesure des changements (voir « Journal des modifications » en bas).

---

## 1. Pages du site

| Fichier | Rôle | Liens sortants |
|---|---|---|
| `index.html` | Accueil (hero animé, problème, garanties, témoignage, méthode, réalisations, CTA, footer) | `projets.html`, `contact.html`, `etude-podblend.html`, `etude-horizon.html`, `#problem`, `#method`, légales |
| `projets.html` | Portfolio / liste des études de cas | `etude-podblend.html`, `etude-horizon.html`, `contact.html`, `index.html` |
| `etude-podblend.html` | Étude de cas — Podblend Studio | `projets.html`, `contact.html`, `index.html`, `etude-horizon.html` (footer) |
| `etude-horizon.html` | Étude de cas — Horizon (notre propre site) | `projets.html`, `contact.html`, `index.html`, `etude-podblend.html` (footer) |
| `contact.html` | Page contact / formulaire / Calendly | `index.html`, `#form` |
| `mentions-legales.html` | Légal | footer |
| `cgv.html` | Légal | footer |
| `confidentialite.html` | Légal | footer |

---

## 2. Design tokens (variables CSS partagées)

Définis dans le `:root` de **chaque** page (dupliqués, pas de CSS externe). Si tu changes une valeur, la répliquer sur toutes les pages concernées.

| Token | Valeur | Sens |
|---|---|---|
| `--cream` | `#fbfbf8` (index/études) / `#f5f2eb` (projets) | Fond |
| `--ink` | `#0a0a0a` | Texte / fonds sombres |
| `--blue` | `#3d95ff` | Accent **global Horizon** + accent de la fiche Horizon |
| `--yellow` | `#fcf240` | Accent secondaire partagé (boutons nav, guillemets) |
| `--accent` | **par client** (voir §5) | Couleur d'accent contextuelle d'une fiche étude de cas |

⚠️ Les tokens sont **copiés dans chaque fichier**. Pas de feuille de style commune → tout changement de token = édition multi-fichiers.

---

## 3. Composants partagés (présents sur plusieurs pages)

| Composant | Classe | Pages | Notes |
|---|---|---|---|
| Barre de progression scroll | `#progress-bar` | index, études, contact | Dégradé `--accent → --yellow` |
| Navbar flottante (pill) | `nav.top` | toutes | Logo + liens + `.nav-cta` ; soulignement au hover (`nav ul a::after`) |
| Bouton WhatsApp flottant | `.wa-btn` | index, études | `wa.me/33658596713` ; animation `waFloat` + magnétique |
| Footer sombre « HORIZON* » | `footer` | index, études | Navigation + études + année dynamique `#dyn-year` |
| Système de révélation au scroll | `.reveal` (index/contact) · `.rev` (études/projets) | toutes | `IntersectionObserver` ajoute `.in` ; délais `.d1..d4` / `.reveal-delay-1..4` |
| **Boutons magnétiques** | script « POLISH » | index → **porté sur études, projets, contact** | Suit la souris sur `.nav-cta,.yt-btn,.cta-dk,.wa-btn`… |

---

## 4. Cartographie des assets (image → où elle est utilisée)

| Asset | Utilisé dans |
|---|---|
| `logo horizon.png` | navbar + footer de **toutes** les pages |
| `horizon-hero.png` | `index` (carte Horizon), `etude-horizon` (galerie, image principale) |
| `podblend-hero.png` | `index` (carte Podblend), `projets`, `etude-podblend` (galerie, image principale) |
| `podblend-logo.webp` | `index` (témoignage), `etude-podblend` (logo fiche) — `filter:invert(1)` |
| `Screenshot …12.54.16 / 13.39.00 / 13.43.10 / 12.55.16 / 13.34.41` | galerie `etude-podblend` |
| `Screenshot …12.53.39 / 12.52.50 / 12.53.02 / 12.53.16 / 13.33.01` | galerie `etude-horizon` |
| favicons / `apple-touch-icon` | `<head>` de toutes les pages |

---

## 5. Identité couleur par client (cohérence index ↔ fiche étude de cas)

**Règle :** la couleur d'accent d'un client dans `index.html` doit être la même que sur sa fiche étude de cas (`--accent`).

| Client | `--accent` | Origine (couleur de la carte dans index) | Éléments pilotés par l'accent sur la fiche |
|---|---|---|---|
| **Horizon** | `#3d95ff` (bleu) | `.project.horizon-theme` (bleu) | progress-bar, `::selection`, hover galerie, puces `recette-list`, hover `yt-btn-primary`, hover liens nav |
| **Podblend** | `#c37832` (cuivre/ambre) | `.project.podblend-theme` (néon ambre `rgba(195,120,50)`→hover `rgba(220,140,60)`) | idem ci-dessus + dégradé `ytm-screen` + glow hover galerie chaud |

> Avant : `etude-podblend.html` utilisait `--blue` partout → **corrigé** en cuivre pour matcher la carte du portfolio.

---

## 6. Tags / étiquettes des études de cas

Style cible = voix « nouvelle agence » : court, premium, orienté résultat (réf. Horizon).

| Fiche | Tags |
|---|---|
| `etude-horizon.html` | `DA Haute Couture` · `Création Intégrale` · `Zéro Template` *(référence du style)* |
| `etude-podblend.html` | `Refonte Premium` · `Autorité Visuelle` · `Landing Conversion` *(adaptés — avant : Design Premium / Stratégie de Marque / Landing Page)* |

> Note : les tags d'un même projet diffèrent selon la page (index, projets, fiche). Ce sont des libellés éditoriaux indépendants — harmoniser si besoin de cohérence stricte.

---

## 7. Journal des modifications

### 2026-06-10 — Session polish (par Claude)
1. **Création de ce fichier** de cartographie.
2. **Couleur par client** : `etude-podblend.html` passe du bleu au **cuivre `#c37832`** (token `--accent`) pour matcher l'identité Podblend de l'index. `etude-horizon.html` reçoit le token `--accent` = bleu (déjà cohérent).
3. **Suppression** du bloc punchline « Quand l'image impose le respect, le prix ne devient plus qu'un détail. » dans `etude-podblend.html`.
4. **Tags Podblend** adaptés au nouveau style : `Refonte Premium / Autorité Visuelle / Landing Conversion`.
5. **Boutons magnétiques** (effet polish de l'index) **portés** sur `etude-podblend`, `etude-horizon`, `projets`, `contact`.
