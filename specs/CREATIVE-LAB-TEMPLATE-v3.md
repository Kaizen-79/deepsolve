# 🧪 CREATIVE LAB TEMPLATE, v3.4

**Version:** 3.4
**Date:** 2026-04-04
**Basé sur:** CREATIVE-LAB-TEMPLATE v2.0 + FULL-SEARCH-PROTOCOL v2.0 (CL-4)
**Améliorations v3:** Vérification croisée (Phase 1c), S-Score calibré, Pruning entropique, Query contrariante (Phase 1b), Weak Signal renforcé
**Améliorations v3.1:** 5e moteur arXiv (`--type academic`), papers académiques gratuits
**Améliorations v3.4:** Semantic Scholar retiré du protocole actif, format de sortie canonique renforcé, phases titrées, tableaux comparatifs, validations visuelles, structure compatible dashboard

---

## Principe

Creative Lab = exploration et idéation sur un sujet ouvert.
Input : une idée, une question "et si...", un domaine à découvrir.
Output : connexions créatives inattendues, croisements de domaines, innovations potentielles.

**La règle d'or : le fichier joint est la MATIÈRE BRUTE, pas les conclusions.**
**5 moteurs obligatoires. Brave/web_search INTERDIT.**
**Socle technique : FULL-SEARCH-PROTOCOL-v2.md** (vérification, S-Score, pruning).

## FORMAT DE SORTIE OBLIGATOIRE

Le rapport final doit être rédigé comme un document unique en Markdown, lisible dans Claude Desktop, Cursor + MCP, ChatGPT, Hermes, et exportable vers un dashboard.

### Règles de forme
1. Phases clairement titrées : `PHASE 0`, `PHASE 1`, `PHASE 1d`, etc.
2. Comparatifs, signaux faibles et collisions dans des tableaux.
3. Validations rendues visuellement avec `✅`, `⚠️`, `❌`.
4. Paragraphes courts, 3 à 4 lignes max.
5. Les signaux spéculatifs sont toujours distingués des éléments validés.

### Structure finale obligatoire
1. `## OVERVIEW` : idée explorée, angle choisi, promesse créative
2. `## MATRIX` : matrice de convergence, signaux faibles, contradictions
3. `## OUTPUT` : collision improbable, synthèse convergente, top croisements
4. `## ACTIONS` : pistes d'exploration, priorités, tests recommandés, décision GO ou HOLD
5. `## SOURCES` : sources réellement utilisées, regroupées par moteur

### Test de qualité
Le rapport doit rester :
1. lisible dans Telegram
2. partageable à un client sans contexte oral
3. exploitable pour un futur onglet dashboard
4. exportable en PDF ou Markdown sans nettoyage manuel

---

## ✅ Pre-Flight Checklist

Avant de lancer :
- [ ] Idée ou sujet décrit clairement
- [ ] MISSION-BRIEF-CONVERTER.md consulté, fichier mission généré
- [ ] **Fichier `research/CL-[NOM].md` créé** (MISSION-PERSISTENCE-PROTOCOL.md)
- [ ] Anti-overlap : memory_search("[sujet]"), pas de doublon
- [ ] 5 moteurs disponibles confirmés
- [ ] Checkpoint planifié après Phase 2

> **⚠️ PERSIST :** Chaque phase écrit ses résultats dans `research/` IMMÉDIATEMENT. Voir MISSION-PERSISTENCE-PROTOCOL.md.

---

## PHASE 0 — Cadrage

### 10x Framing
Formuler la version 10x radicale de l'idée :
- **Version actuelle** : [ce qui existe]
- **Version 10x** : [si on poussait à l'extrême ?]
- **Version impossible** : [si toutes les contraintes disparaissaient ?]

L'objectif n'est pas de viser l'impossible : c'est d'ouvrir le champ des possibles avant de chercher.

### Prior Art Sweep
```bash
cd ./search-router
./scripts/search.sh "[sujet] existing approaches implementations 2024 2025" --type factual
```
Ce qui existe déjà = le tremplin, pas le plafond.

---

## PHASE 1 — 5 Moteurs Principaux

Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 1** : 5 queries adaptées à chaque moteur.

```bash
cd ./search-router
./scripts/search.sh "[query EXA : concepts profonds du sujet]" --type semantic
./scripts/search.sh "[query Tavily : recherches récentes]" --type factual
./scripts/search.sh "[query Linkup : mécanismes précis]" --type standard
./scripts/search.sh "[query Parallel : vue d'ensemble]" --type deep
./scripts/search.sh "[query arXiv : papers académiques fondamentaux]" --type academic
```

---

## PHASE 1b — Query Contrariante

Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 1b** :

```bash
./scripts/search.sh "[sujet] criticism limitations failure doesn't work why it fails" --type factual
```

---

## PHASE 1c — Vérification Croisée

Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 1c** :
1. Extraire les 3-5 claims clés de Phase 1
2. Re-vérifier chaque claim avec des queries indépendantes
3. Classifier : VÉRIFIÉ / CONTESTÉ / NON VÉRIFIÉ / RÉFUTÉ
4. Seuls VÉRIFIÉ et CONTESTÉ passent en Phase 2

**Note CL :** pour les concepts exploratoires (cross-pollination), la vérification est optionnelle. Ne pas tuer les signaux faibles par excès de rigueur.

---

## PHASE 1d — Cross-Pollination Élargie

6 queries structurées, toutes obligatoires :

```bash
# Adjacent : domaine proche mais différent
./scripts/search.sh "[domaine adjacent] [principe similaire] approach" --type semantic

# Lointain : domaine apparemment sans rapport (source des vraies innovations)
./scripts/search.sh "[domaine lointain inattendu] [pattern similaire]" --type semantic

# Historique : comment ce domaine a évolué
./scripts/search.sh "[sujet] history evolution pre-digital analog approaches" --type factual

# Opposé : anti-pattern, ce qui échoue toujours
./scripts/search.sh "[sujet] failure modes limitations why it doesn't work" --type factual

# Biomimicry : équivalent dans le vivant (OBLIGATOIRE Creative Lab)
./scripts/search.sh "[principe du sujet] biological equivalent nature organism" --type semantic

# Anti-consensus : ce que les experts croient à tort (OBLIGATOIRE Creative Lab)
./scripts/search.sh "[sujet] controversial counterintuitive expert disagreement" --type deep
```

**Second-Order Discovery :** si un terme nouveau et intrigant émerge → lancer une query dédiée dessus.

---

## PHASE 2 — Synthèse Vérifiée

### Pruning entropique
Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 3a** :
- Pertinence directe (oui/partiel/non)
- Spécificité (données concrètes vs discours général)
- Fraîcheur (<2 ans, 2-5 ans, >5 ans)
- Éliminer les résultats "partiel + générique + >5 ans"

**Exception CL :** un résultat ancien mais provenant d'un domaine inattendu (biomimicry, historique) est conservé même s'il a >5 ans. Le pruning s'applique strictement aux résultats du même domaine.

### Matrice de convergence avec S-Score
Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 3b** :

| Concept | EXA | Tavily | Linkup | Parallel | arXiv | Cross-Poll | Vérifié ? | S-Score |
|---------|-----|--------|--------|----------|-------|------------|------------|---------|
| Concept A | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | OUI | 0.92 |
| Concept B | ✅ | | | ✅ | | | n/a | 0.29 |

```
S = C₀ × (1 - I)
  C₀ = sources confirmantes / moteurs totaux
  I  = contradictions / vérifications effectuées
```

**Note CL :** pour les concepts de cross-pollination non vérifiés (Phase 1c optionnelle pour eux), utiliser C₀ seul comme score de convergence et mentionner "non vérifié" dans la colonne.

### Weak Signal Detection (renforcé v3)
Chercher les concepts qui :
- Apparaissent une seule fois mais dans une source inattendue
- Créent une dissonance cognitive (contredisent l'intuition)
- Viennent d'un domaine distant mais ont un mécanisme transposable

**Nouveau v3 :** pour chaque signal faible identifié, lancer une **mini-vérification** (1 query) :
```bash
./scripts/search.sh "[signal faible] applications implementations results" --type semantic
```
Si la mini-vérification trouve ≥1 résultat concret → promouvoir en "signal à explorer".
Si 0 résultat → conserver comme "spéculatif, non validé".

---

## ⛔ CHECKPOINT OBLIGATOIRE

**STOP ici. Présenter à the user :**
- Matrice de convergence avec S-Scores calculés
- Top insights Phase 1 + Phase 1d
- Claims CONTESTÉ identifiés avec contradictions
- Signaux faibles classés (à explorer / spéculatif)
- Proposition pour la collision Phase 3

Attendre le go explicite avant Phase 3.

---

## PHASE 3 — Collision Créative

### Sortie A — Collision improbable
Prendre les 2 concepts les plus incompatibles trouvés → forcer leur fusion.
- Concept X (le plus classique du sujet) × Concept Y (le plus bizarre/lointain trouvé)
- Que se passe-t-il si on les combine ? Qu'est-ce que ça invente ?
- Présenter l'innovation potentielle qui en émerge.

### Sortie B — Synthèse convergente
Les concepts validés (S ≥ 0.70) → quelle innovation réaliste ils permettent ?
La voie la plus robuste, la plus directement exploitable.

the user choisit A, B, ou les deux.

---

## PHASE 4 — Livrables

Format obligatoire :
- [ ] `## OVERVIEW` avec angle, promesse et niveau de confiance
- [ ] `## MATRIX` avec tableaux de convergence, signaux faibles et contradictions
- [ ] `## OUTPUT` avec collision improbable, synthèse convergente et top croisements
- [ ] `## ACTIONS` avec next steps, priorités, décisions et risques
- [ ] `## SOURCES` avec regroupement par moteur
- [ ] Claims CONTESTÉ ou RÉFUTÉ listés comme caveats
- [ ] POST-ACTION CHECKLIST complétée

---

## POST-ACTION CHECKLIST

```
[ ] Insights sauvegardés (memory_search mis à jour)
[ ] Croisements prometteurs notés dans DECISIONS-LOG.md
[ ] Ticket créé si exploration suivante planifiée
[ ] Sources marquées pour référence future
[ ] Signal faible le plus prometteur → trigger de suivi créé
```

---

## Changelog

| Version | Date | Changement |
|---------|------|------------|
| v2 (PROMPT) | 2026-01-xx | Version originale Creative Lab |
| 2.0 | 2026-02-26 | Phase 0, Phase 1b, Weak Signal Detection, Collision A+B, Confidence scoring |
| 3.0 | 2026-03-27 | Vérification croisée (Phase 1c, optionnelle pour cross-poll), S-Score calibré, Pruning entropique (exception domaines distants), Query contrariante (Phase 1b), Weak Signal renforcé (mini-vérif), socle FULL-SEARCH-PROTOCOL-v2. Source : CL-4 |
| 3.1 | 2026-03-27 | 5e moteur arXiv (`--type academic`). Matrice S-Score 6 colonnes |
| 3.2 | 2026-03-28 | MISSION-PERSISTENCE-PROTOCOL intégré (write-through obligatoire, fichier research/) |
| 3.4 | 2026-04-04 | Semantic Scholar retiré du template actif. Format de sortie renforcé : phases titrées, tableaux comparatifs, validations ✅/❌, structure partageable et compatible dashboard. |
