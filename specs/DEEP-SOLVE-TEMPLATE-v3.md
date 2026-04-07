# 🔥 DEEP SOLVE TEMPLATE, v3.4

**Version:** 3.4
**Date:** 2026-04-04
**Basé sur:** DEEP-SOLVE-TEMPLATE v2.0 + FULL-SEARCH-PROTOCOL v2.0 (CL-4)
**Améliorations v3:** Vérification croisée (Phase 1c), S-Score calibré, Pruning entropique, Query contrariante (Phase 1b)
**Améliorations v3.1:** 5e moteur arXiv (`--type academic`), papers académiques gratuits
**Améliorations v3.4:** Semantic Scholar retiré du protocole actif, format de sortie canonique renforcé, phases titrées, tableaux comparatifs, validations visuelles, structure compatible dashboard

---

## Principe

Deep Solve = résolution profonde d'un problème précis.
Input : un problème, un blocage, une décision technique à trancher.
Output : une solution implémentable, **vérifiée** multi-sources, avec second-order effects analysés.

**Règle absolue : EXA + Tavily + Linkup + Parallel + arXiv obligatoires. Brave/web_search INTERDIT.**
**Socle technique : FULL-SEARCH-PROTOCOL-v2.md** (vérification, S-Score, pruning).

## FORMAT DE SORTIE OBLIGATOIRE

Le rapport final doit être rédigé comme un document unique en Markdown, lisible dans Claude Desktop, Cursor + MCP, ChatGPT, Hermes, et exportable vers un dashboard.

### Règles de forme
1. Phases clairement titrées : `PHASE 0`, `PHASE 1`, `PHASE 1b`, etc.
2. Comparatifs et claims dans des tableaux, jamais dans des blocs de prose denses.
3. Validations rendues visuellement avec `✅`, `⚠️`, `❌`.
4. Paragraphes courts, 3 à 4 lignes max.
5. Une conclusion exécutable, pas seulement une synthèse.

### Structure finale obligatoire
1. `## OVERVIEW` : problème, verdict, recommandation, niveau de confiance
2. `## MATRIX` : matrice de convergence et claims vérifiés ou contestés
3. `## OUTPUT` : solution A, solution B, effets de second ordre
4. `## ACTIONS` : étapes concrètes, dépendances, risques, décision ADOPT ou ADAPT ou SKIP
5. `## SOURCES` : sources réellement utilisées, regroupées par moteur

### Test de qualité
Le rapport doit rester :
1. lisible dans Telegram
2. copiable dans Notion
3. exportable en PDF
4. transformable en onglets dashboard sans réécriture manuelle

---

## ✅ Pre-Flight Checklist

Avant de lancer :
- [ ] Problème décrit précisément (pas "améliorer X" → "X échoue dans condition Y car Z")
- [ ] MISSION-BRIEF-CONVERTER.md consulté, fichier mission généré
- [ ] **Fichier `research/DS-[NOM].md` créé** (MISSION-PERSISTENCE-PROTOCOL.md)
- [ ] Anti-overlap : memory_search("[sujet]"), pas de doublon
- [ ] 5 moteurs disponibles confirmés
- [ ] Checkpoint planifié après Phase 2

> **⚠️ PERSIST :** Chaque phase écrit ses résultats dans `research/` IMMÉDIATEMENT. Voir MISSION-PERSISTENCE-PROTOCOL.md.

---

## PHASE 0 — Cadrage

### Forced Falsification
Avant toute recherche, lister pourquoi les solutions évidentes vont échouer :
- Solution évidente 1 → échoue parce que [raison]
- Solution évidente 2 → échoue parce que [raison]
- Solution évidente 3 → échoue parce que [raison]

Objectif : identifier les vraies contraintes cachées, pas les contraintes supposées.

### Prior Art Sweep
```bash
cd ./search-router
./scripts/search.sh "[problème] existing solutions implementations" --type factual
```
Si solution identique déjà documentée → analyser pourquoi elle n'a pas été adoptée avant de continuer.

---

## PHASE 1 — 5 Moteurs Principaux

Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 1** : 5 queries adaptées à chaque moteur.

```bash
cd ./search-router
./scripts/search.sh "[query EXA : mécanismes techniques profonds]" --type semantic
./scripts/search.sh "[query Tavily : développements 2024-2026]" --type factual
./scripts/search.sh "[query Linkup : définitions, benchmarks]" --type standard
./scripts/search.sh "[query Parallel : big picture, comprehensive]" --type deep
./scripts/search.sh "[query arXiv : papers fondamentaux du domaine]" --type academic
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

---

## PHASE 1d — Cross-Pollination

4 queries structurées, toutes obligatoires :

```bash
# Adjacent : domaine proche mais différent
./scripts/search.sh "[domaine adjacent] [problème équivalent] solution" --type semantic

# Lointain : domaine apparemment sans rapport
./scripts/search.sh "[domaine lointain inattendu] [principe similaire]" --type semantic

# Historique : comment ce problème était résolu avant
./scripts/search.sh "[problème] historical solutions pre-2000 approaches" --type factual

# Opposé : anti-pattern, pourquoi ça échoue
./scripts/search.sh "[problème] failure modes anti-patterns why it fails" --type factual
```

**Second-Order Effects query :**
```bash
./scripts/search.sh "[solution envisagée] long term consequences unintended effects" --type deep
```

---

## PHASE 2 — Synthèse Vérifiée

### Pruning entropique
Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 3a** :
- Pertinence directe (oui/partiel/non)
- Spécificité (données concrètes vs discours général)
- Fraîcheur (<2 ans, 2-5 ans, >5 ans)
- Éliminer les résultats "partiel + générique + >5 ans"

### Matrice de convergence avec S-Score
Suivre **FULL-SEARCH-PROTOCOL-v2.md Phase 3b** :

| Concept | EXA | Tavily | Linkup | Parallel | arXiv | Cross-Poll | Vérifié ? | S-Score |
|---------|-----|--------|--------|----------|-------|------------|------------|---------|
| Concept A | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | OUI | 0.92 |
| Concept B | ✅ | ✅ | | | | | CONTESTÉ | 0.29 |

```
S = C₀ × (1 - I)
  C₀ = sources confirmantes / moteurs totaux
  I  = contradictions / vérifications effectuées
```

### Second-Order Effects
Pour chaque solution candidate (S ≥ 0.40) :
- Si cette solution fonctionne → qu'est-ce qui change à 6 mois ?
- Quels systèmes adjacents sont affectés ?
- Quel risque de régression introduit-elle ?

---

## ⛔ CHECKPOINT OBLIGATOIRE

**STOP ici. Présenter à the user :**
- Matrice de convergence avec S-Scores calculés (pas estimés)
- Top 2-3 solutions candidates avec second-order effects
- Claims CONTESTÉ identifiés avec les contradictions trouvées
- Recommandation motivée

Attendre le go explicite avant Phase 3.

---

## PHASE 3 — Solution Technique

### Sortie A — Collision improbable
Prendre les 2 concepts les plus éloignés trouvés → forcer leur combinaison.
Présenter le croisement et ce qu'il donne concrètement.

### Sortie B — Solution convergente
Synthèse des concepts validés (S ≥ 0.70).
Solution la plus robuste, la plus directement implémentable.

the user choisit A, B, ou les deux.

---

## PHASE 4 — Livrables

Format obligatoire :
- [ ] `## OVERVIEW` avec verdict et recommandation
- [ ] `## MATRIX` avec tableaux de convergence et claims
- [ ] `## OUTPUT` avec solution A, solution B et second-order effects
- [ ] `## ACTIONS` avec plan d'implémentation, dépendances, risques et décision finale
- [ ] `## SOURCES` avec regroupement par moteur
- [ ] Claims CONTESTÉ ou RÉFUTÉ listés comme caveats
- [ ] POST-ACTION CHECKLIST complétée

---

## POST-ACTION CHECKLIST

```
[ ] Solution validée et documentée
[ ] memory_search mis à jour (chunk clé sauvegardé)
[ ] DECISIONS-LOG.md mis à jour si décision architecturale
[ ] Ticket créé si implémentation planifiée
[ ] Trigger de reconsidération créé si SKIP
```

---

## Changelog

| Version | Date | Changement |
|---------|------|------------|
| 1.4 | 2026-02-07 | Version originale |
| 2.0 | 2026-02-26 | Phase 0, Cross-Poll, Second-Order Effects, Confidence scoring |
| 3.0 | 2026-03-27 | Vérification croisée (Phase 1c), S-Score calibré, Pruning entropique, Query contrariante (Phase 1b), socle FULL-SEARCH-PROTOCOL-v2. Source : CL-4 |
| 3.1 | 2026-03-27 | 5e moteur arXiv (`--type academic`). Matrice S-Score 6 colonnes. Minimum requis : EXA + Tavily + arXiv |
| 3.2 | 2026-03-28 | MISSION-PERSISTENCE-PROTOCOL intégré (write-through obligatoire, fichier research/) |
| 3.4 | 2026-04-04 | Semantic Scholar retiré du template actif. Format de sortie renforcé : phases titrées, tableaux comparatifs, validations ✅/❌, structure partageable et compatible dashboard. |
