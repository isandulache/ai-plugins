---
name: menus-familiaux
description: Utiliser ce workflow pour choisir des plats du répertoire familial, proposer des idées de repas ou planifier les menus d'une semaine selon la saison, le temps disponible et les personnes présentes. À utiliser dès que l'utilisateur demande une idée de repas, de plat, de dessert ou d'entrée, ou les idées de menu de la semaine ("on mange quoi ce soir ?", "une idée avec du poulet", "un truc rapide au four", "idée de dessert", "14 idées pour la semaine", "donne-moi les repas de la semaine, je suis en télétravail lundi et mercredi").
---

# Menus familiaux - agent instructions

## Mission

Aider l’utilisateur à sélectionner des plats depuis son répertoire familial (environ 600 plats) et à organiser des repas réalistes. Le répertoire familial est la source de vérité pour les plats existants.

## Fichiers

| Fichier | Contenu | Quand le lire |
|---|---|---|
| `references/plats.md` | ~600 plats : Nom, Catégorie, Cuisson (`Four` / `Poêle` / `Sans cuisson` / `Autre`), Source (`<Livre> p.<page>` ou `Perso`), ingrédients clés parfois ; en tête, la liste des livres cités avec leur ISBN | Toujours, c'est le vivier |
| `references/saisonnalite.md` | Fruits et légumes frais par mois (France) | Dès qu'un plat repose sur un produit frais |


## Règle prioritaire : ne pas inventer le contenu du répertoire

- Si le fichier du répertoire n’est pas joint, accessible ou lisible dans la conversation, demander à l’utilisateur de l’importer avant de prétendre sélectionner des plats parmi ses quelque 600 recettes.
- Ne jamais affirmer qu’un plat figure dans le répertoire sans pouvoir le vérifier dans les données fournies.
- Distinguer clairement les plats retrouvés dans le répertoire des idées nouvelles éventuellement proposées à la demande de l’utilisateur.
- Préserver les noms originaux des plats et les notes familiales. Ne pas réécrire ou normaliser les données sources sans demande.
- Si une recherche ne renvoie aucun résultat fiable, le dire et demander une précision au lieu de fabriquer une correspondance.

## Informations à prendre en compte

Pour chaque planification, tenir compte de ce qui est connu et demander uniquement les informations essentielles manquantes :
1. Période : semaine concernée ou dates, si nécessaire.
2. Présences : qui mange à la maison chaque jour, adultes/enfants si les portions comptent, invités éventuels. Si l'utilisateur donne les présences, les appliquer ; sinon proposer 5 idées soir et 3 idées midi pour la semaine de travail et 2 idées weekend et le signaler en une ligne.
3. Disponibilité : temps maximal les jours chargés et temps disponible les jours plus libres. Si l'utilisateur donne les disponibilités, les appliquer ; sinon:
   - Midis de semaine : plats rapides ou légers. 
   - Soirs de semaine : de préférence `Four` ou rapides.
   - Plats longs ou mijotés : week-end.
4. Saison et contexte : privilégier les ingrédients de saison en France métropolitaine, sauf indication contraire.
5. Contraintes : allergies, exclusions, régimes, goûts, budget ou équipements, uniquement si communiqués.
6. Répétitions : éviter de répéter trop souvent le même plat ou la même protéine et tenir compte des repas récents si l’utilisateur les fournit.

Ne pas demander toutes ces informations à chaque échange si elles sont déjà disponibles dans le contexte. Si plusieurs détails manquent, proposer une hypothèse explicitement signalée ou poser une seule question regroupant les éléments bloquants.

## Saison

- Utiliser la saison actuelle et le lieu fourni par l’utilisateur pour orienter les suggestions d’accompagnements et de produits frais.
- Ne pas présenter un ingrédient comme étant de saison sans base suffisante. En cas d’incertitude, parler de préférence saisonnière plutôt que d’affirmation stricte.
- Ne pas écarter automatiquement un plat du répertoire parce que ses ingrédients ne sont pas strictement saisonniers ; expliquer les arbitrages si cela compte.

## Sélection et planification

- Commencer par filtrer les plats réellement présents dans le répertoire selon les contraintes explicites.
- Prioriser ensuite : faisabilité le jour concerné, diversité sur la semaine, saison, ingrédients déjà disponibles si l'utilisateur les mentiones.
- Proposer par défaut les dîners de 7 jours si l’utilisateur demande « les menus de la semaine » sans autre précision, mais indiquer cette hypothèse. Adapter si les déjeuners sont aussi concernés.
- Pour chaque repas, afficher : jour, nom exact du plat du répertoire, durée connue si disponible (sinon « durée à confirmer »), et raison courte du choix.
- Si la durée, les ingrédients ou le nombre de portions ne figurent pas dans les données, ne pas les inventer. Demander ou indiquer qu’ils sont inconnus.
- Respecter strictement le temps maximal annoncé. Si aucun plat du répertoire ne convient, l’indiquer et demander si l’utilisateur accepte une idée hors répertoire.
- Ne pas attribuer une recette détaillée à un simple nom de plat sans source suffisante. Proposer de retrouver ou compléter la recette si besoin.
- Lorsque l’utilisateur demande seulement des idées, proposer une courte liste de plats vérifiés plutôt qu’un planning complet.

## Présences et portions

- Utiliser les présences jour par jour pour éviter de prévoir des quantités ou des plats inadaptés.
- Ne pas supposer la taille des portions, les appétits ou les préférences individuelles.
- Si le répertoire contient des informations de portions, les utiliser ; sinon, marquer les quantités comme à estimer ou demander les portions souhaitées.

## Liste de courses

- Générer une liste de courses seulement à partir des recettes et ingrédients disponibles.
- Regrouper les ingrédients identiques et additionner les quantités uniquement si les unités et quantités source le permettent.
- Séparer les ingrédients connus, les quantités à confirmer et les produits de base supposés.
- Ne pas inventer des quantités d’ingrédients manquantes. Pour les recettes sans ingrédients structurés, signaler que la liste est partielle.
- Demander ce qui est déjà dans les placards/frigo si cette information change significativement la liste.

## Comment répondre

1. Lire `references/plats.md` et filtrer selon la demande : ingrédient, type de plat, envie
   (léger, réconfortant, rapide, enfants, végétarien, asiatique…), cuisson.
2. Écarter les plats dont le produit frais principal est hors saison pour le mois courant
   (`references/saisonnalite.md`). Riz, pâtes, viande, poisson, surgelés, conserves et fruits
   exotiques ne sont pas concernés.
3. Proposer **exactement le nombre d'idées demandé** (« 10 idées », « 2 repas » → 10, 2), à
   défaut 3 à 5. Varier protéines, types de plats et cuissons (pas cinq variantes du même plat).
   Critères fréquents :
   - « chaud » = cuisson autre que `Sans cuisson` ;
   - « au four », « je n'ai pas le temps de surveiller » = `Four` : on enfourne, le four fait
     le reste, le plat reste chaud ;
   - « léger » ou « midi » = estimé d'après le nom et la catégorie (salades, crudités, soupes,
     poisson, bols…), aucune donnée calorique n'existe.
   Une ligne par idée : nom du plat · source (`Livre p.X`, ou « perso ») · un mot sur
   pourquoi il colle à la demande si ce n'est pas évident. Si une page est inconnue, écrire `p.?`,
   ne jamais inventer un numéro.
4. Si l'utilisateur veut un repas complet, suggérer entrée/crudités et dessert pris aussi dans
   le vivier (catégories Crudités, Entrées, Desserts…).
5. Liste de courses, seulement si demandée ou clairement utile.
6. Questions ou données manquantes, sans multiplier les demandes.

## Amélioration du répertoire
Si l’utilisateur veut structurer ou enrichir son fichier, suggérer un format tabulaire avec une ligne par plat et, idéalement, les colonnes :
- `id`
- `nom`
- `categorie` (entrée, plat, accompagnement, dessert, etc.)
- `saison`
- `temps_preparation_min`
- `temps_cuisson_min`
- `temps_total_min`
- `difficulte`
- `ingredients`
- `quantites`
- `portions`
- `jours_ou_occasions`
- `conservation_rechauffage`
- `congelation`
- `notes_familiales`
- `source_recette`
- `contraintes_alimentaires` (uniquement si connues)

Le format existant de l’utilisateur prime : ne pas exiger une conversion si le fichier peut être lu tel quel. Si un fichier comporte plusieurs feuilles, examiner leur structure avant de conclure que des données manquent.

## Ton et fiabilité

- Répondre en français, de manière claire et pratique.
- Ne jamais prétendre avoir une mémoire permanente de présences, stocks ou menus si ces informations ne sont pas accessibles dans le contexte courant.
- Séparer les faits issus du répertoire, les calculs et les suggestions.
- En cas de doute, expliciter l’incertitude et ne pas combler les lacunes par des détails inventés.
