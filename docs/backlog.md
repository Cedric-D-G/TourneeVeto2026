# Backlog du POC TournéeVéto

Backlog dérivé du [périmètre MVP](./mvp.md). Les issues ci-dessous sont rédigées pour être créées dans GitHub.

## Convention de labels

- `epic` : issue de type epic.
- `story` : issue de type user story.
- Chaque fonctionnalité possède aussi un label dédié : il est appliqué à son epic et à toutes ses stories pour les relier.
- Les données utilisées dans les scénarios sont fictives et celles des grilles/règles sont des données de démonstration.

## Epic — Chargement hors ligne de l’application (PWA)

**Labels :** `epic`, `offline-app`

**Objectif :** permettre le parcours de visite sur tablette après le chargement initial, sans réseau.

### Story — Charger l’application en mode avion

**Labels :** `story`, `offline-app`  
**Epic parent :** Chargement hors ligne de l’application (PWA)

En tant que vétérinaire, je veux ouvrir l’application déjà chargée lorsque ma tablette est en mode avion afin de préparer et réaliser une visite sans réseau.

**Critères d’acceptation**

```gherkin
Scénario: Ouvrir l’application après un chargement initial en ligne
  Étant donné que l’application a été chargée une première fois en ligne sur la tablette
  Quand je ferme puis relance l’application en mode avion
  Alors l’écran d’accueil s’affiche sans erreur ni requête réseau

Scénario: Signaler une première ouverture sans cache hors ligne
  Étant donné que l’application n’a jamais été chargée sur la tablette
  Quand je tente de l’ouvrir en mode avion
  Alors un message explicite indique que le chargement initial en ligne est nécessaire
```

### Story — Parcourir les fonctions essentielles sans réseau

**Labels :** `story`, `offline-app`  
**Epic parent :** Chargement hors ligne de l’application (PWA)

En tant que vétérinaire, je veux consulter un élevage, une fiche animale, enregistrer un événement et afficher la grille en mode avion afin de poursuivre la visite dans une étable sans connexion.

**Critères d’acceptation**

```gherkin
Scénario: Réaliser le parcours essentiel hors ligne
  Étant donné que l’application et les données de démonstration ont été chargées sur la tablette
  Et que la tablette est en mode avion
  Quand j’ouvre un élevage, consulte une fiche, enregistre un événement et affiche la grille
  Alors chaque écran et l’événement s’affichent sans erreur ni requête réseau

Scénario: Signaler une ressource locale indisponible
  Étant donné que je suis en mode avion et qu’une ressource nécessaire au parcours est absente du cache
  Quand je tente d’ouvrir l’écran qui en dépend
  Alors l’application affiche une erreur explicite au lieu d’un écran vide ou d’un succès trompeur
```

## Epic — Stockage local IndexedDB

**Labels :** `epic`, `local-storage`

**Objectif :** conserver dans le navigateur les données et saisies nécessaires au POC, sans backend ni synchronisation.

### Story — Persister les données de visite dans IndexedDB

**Labels :** `story`, `local-storage`  
**Epic parent :** Stockage local IndexedDB

En tant que vétérinaire, je veux que les événements saisis soient enregistrés dans IndexedDB afin de les retrouver après la fermeture du navigateur, même hors ligne.

**Critères d’acceptation**

```gherkin
Scénario: Retrouver un événement après réouverture
  Étant donné que j’ai enregistré un événement pour un animal
  Quand je ferme complètement puis rouvre le navigateur hors ligne
  Alors l’événement est toujours présent dans l’historique de cet animal
  Et le test confirme que l’enregistrement provient d’IndexedDB

Scénario: Signaler un échec d’écriture locale
  Étant donné que le navigateur ne peut pas écrire dans IndexedDB
  Quand je tente d’enregistrer un événement
  Alors l’application affiche une erreur explicite
  Et elle n’annonce pas que l’événement a été enregistré
```

### Story — Initialiser et lire les données locales du POC

**Labels :** `story`, `local-storage`  
**Epic parent :** Stockage local IndexedDB

En tant que vétérinaire, je veux que les données de démonstration disponibles dans mon navigateur soient lues localement afin de consulter les élevages et animaux sans backend.

**Critères d’acceptation**

```gherkin
Scénario: Consulter les données locales après le chargement de l’application
  Étant donné que les données de démonstration ont été importées ou initialisées dans le navigateur
  Quand j’ouvre l’application hors ligne
  Alors les données disponibles sont lues localement et les écrans concernés sont consultables

Scénario: Signaler une base locale illisible
  Étant donné que la base IndexedDB ne peut pas être ouverte ou lue
  Quand l’application tente d’afficher les données locales
  Alors elle affiche une erreur explicite et ne présente pas les données comme étant à jour
```

## Epic — Import CSV d’un troupeau

**Labels :** `epic`, `herd-csv-import`

**Objectif :** amorcer le suivi avec un CSV conforme au modèle de colonnes documenté et au jeu de test fictif.

### Story — Importer un CSV conforme

**Labels :** `story`, `herd-csv-import`  
**Epic parent :** Import CSV d’un troupeau

En tant que vétérinaire, je veux importer le CSV de l’élevage au format documenté afin de retrouver les animaux dans l’application sans ressaisie.

**Critères d’acceptation**

```gherkin
Scénario: Importer le fichier de test conforme
  Étant donné que je sélectionne le CSV de test conforme au modèle documenté
  Quand je lance l’import
  Alors tous les animaux valides du fichier apparaissent dans le troupeau
  Et chaque animal apparaît une seule fois avec son identifiant

Scénario: Ne pas importer un fichier sans animal valide
  Étant donné que je sélectionne un CSV conforme dont aucune ligne d’animal n’est valide
  Quand je lance l’import
  Alors l’application affiche une erreur explicite
  Et aucun animal n’est ajouté au troupeau
```

### Story — Vérifier le format et l’intégrité du CSV avant import

**Labels :** `story`, `herd-csv-import`  
**Epic parent :** Import CSV d’un troupeau

En tant que vétérinaire, je veux que le fichier et ses colonnes soient validés avant l’import afin d’éviter des données de troupeau incomplètes ou incohérentes.

**Critères d’acceptation**

```gherkin
Scénario: Rejeter un fichier au format ou aux colonnes non conformes
  Étant donné que je sélectionne un fichier illisible ou dépourvu d’une colonne obligatoire du modèle
  Quand je lance l’import
  Alors l’application indique explicitement le problème de format ou de colonne
  Et aucune donnée partielle n’est importée

Scénario: Préserver les données existantes si l’import est invalide
  Étant donné qu’un troupeau existe déjà dans l’application
  Quand je tente d’importer un fichier invalide
  Alors les animaux déjà présents restent inchangés
  Et aucune ligne du fichier invalide n’est ajoutée
```

## Epic — Fiche animale et ajout d’événement

**Labels :** `epic`, `animal-record`

**Objectif :** consulter les informations individuelles utiles et consigner les événements associés à l’animal.

### Story — Consulter la fiche d’un animal

**Labels :** `story`, `animal-record`  
**Epic parent :** Fiche animale et ajout d’événement

En tant que vétérinaire, je veux ouvrir la fiche d’une vache depuis le troupeau afin de consulter son identification, sa généalogie disponible, son statut reproducteur et son historique.

**Critères d’acceptation**

```gherkin
Scénario: Afficher les informations de la vache de test
  Étant donné que le troupeau contient une vache du jeu de test
  Quand j’ouvre sa fiche depuis la liste
  Alors sa fiche affiche son numéro d’identification, la généalogie disponible, son statut reproducteur et l’historique de ses événements

Scénario: Traiter un identifiant d’animal introuvable
  Étant donné qu’aucun animal ne correspond à l’identifiant demandé
  Quand je tente d’ouvrir sa fiche
  Alors l’application indique que l’animal est introuvable
  Et n’affiche pas la fiche d’un autre animal
```

### Story — Ajouter un événement daté à un animal

**Labels :** `story`, `animal-record`  
**Epic parent :** Fiche animale et ajout d’événement

En tant que vétérinaire, je veux ajouter un événement daté à la fiche d’un animal afin de garder une trace de son suivi individuel pendant la visite.

**Critères d’acceptation**

```gherkin
Scénario: Enregistrer un événement valide
  Étant donné que j’ai ouvert la fiche d’un animal existant
  Quand je saisis un événement avec une date valide et l’enregistre
  Alors l’événement est associé à cet animal et apparaît dans son historique
  Et il reste présent après rechargement hors ligne

Scénario: Refuser un événement sans date valide
  Étant donné que j’ai ouvert la fiche d’un animal existant
  Quand je tente d’enregistrer un événement sans date ou avec une date invalide
  Alors l’application indique que la date doit être corrigée
  Et aucun événement invalide n’est ajouté à l’historique
```

## Epic — Grille de régie minimale

**Labels :** `epic`, `management-grid`

**Objectif :** présenter les actions et examens issus du jeu de données d’exemple, sans calcul clinique automatique.

### Story — Consulter les actions prévues par animal

**Labels :** `story`, `management-grid`  
**Epic parent :** Grille de régie minimale

En tant que vétérinaire, je veux voir les actions prévues pour chaque animal avec leur date afin de repérer les éléments à traiter durant la visite.

**Critères d’acceptation**

```gherkin
Scénario: Afficher les actions et dates du jeu de test
  Étant donné le jeu de données de démonstration fixé pour le test
  Quand j’ouvre la grille de régie
  Alors chaque action associée à un animal est affichée avec cet animal et sa date prévue
  Et les résultats correspondent aux données du jeu de test

Scénario: Signaler une grille indisponible
  Étant donné que les données nécessaires à la grille ne peuvent pas être lues
  Quand j’ouvre la grille de régie
  Alors l’application affiche une erreur explicite
  Et ne présente pas une grille vide comme si aucune action n’était prévue
```

### Story — Filtrer la grille à la date de visite

**Labels :** `story`, `management-grid`  
**Epic parent :** Grille de régie minimale

En tant que vétérinaire, je veux filtrer la grille selon la date de visite afin de concentrer mon attention sur les actions prévues ce jour-là.

**Critères d’acceptation**

```gherkin
Scénario: Afficher uniquement les actions prévues à la date choisie
  Étant donné que la grille contient des actions à plusieurs dates
  Quand je filtre sur une date de visite
  Alors seules les actions prévues à cette date sont affichées
  Et la liste correspond au jeu de test

Scénario: Signaler une date de filtre invalide
  Étant donné que la grille est affichée
  Quand je saisis une date de filtre invalide
  Alors l’application signale que la date doit être corrigée
  Et conserve la grille précédente sans appliquer un filtre invalide
```

## Epic — Visite et rapport imprimable

**Labels :** `epic`, `visit-report`

**Objectif :** clore la visite par un aperçu de rapport imprimable contenant les informations pertinentes de la visite.

### Story — Préparer le rapport de la visite

**Labels :** `story`, `visit-report`  
**Epic parent :** Visite et rapport imprimable

En tant que vétérinaire, je veux créer un contexte de visite avec un élevage et une date afin de regrouper les événements consignés lors de cette visite dans un rapport.

**Critères d’acceptation**

```gherkin
Scénario: Créer une visite pour un élevage
  Étant donné qu’un élevage de démonstration est disponible
  Quand je démarre une visite à une date valide pour cet élevage
  Alors la visite est associée à l’élevage et à la date choisie

Scénario: Refuser une visite sans élevage ou date valide
  Étant donné que je démarre une nouvelle visite
  Quand l’élevage est absent ou que la date est invalide
  Alors l’application indique les informations à corriger
  Et ne crée pas de visite incomplète
```

### Story — Prévisualiser et imprimer le rapport

**Labels :** `story`, `visit-report`  
**Epic parent :** Visite et rapport imprimable

En tant que vétérinaire, je veux prévisualiser et imprimer un rapport de visite afin de disposer d’une trace partageable sur place.

**Critères d’acceptation**

```gherkin
Scénario: Prévisualiser le contenu attendu du rapport
  Étant donné qu’une visite comprend au moins un événement
  Quand je génère l’aperçu avant impression
  Alors le rapport affiche l’élevage, la date de visite, les statuts reproducteurs et les événements de cette visite

Scénario: Exclure la navigation de l’impression
  Étant donné que l’aperçu du rapport est affiché
  Quand je lance l’impression ou l’enregistrement en PDF
  Alors le document contient le rapport et ne contient pas la navigation de l’application

Scénario: Signaler l’absence d’événement pour la visite
  Étant donné qu’aucun événement n’a été consigné durant la visite
  Quand je tente de générer le rapport
  Alors l’aperçu indique explicitement qu’aucun événement n’est associé à la visite
  Et n’inclut pas les événements d’une autre visite
```

## Epic — Bilan de biosécurité simplifié

**Labels :** `epic`, `biosecurity-review`

**Objectif :** recueillir les réponses au questionnaire de démonstration et afficher les pratiques prioritaires selon le jeu de règles fixe.

### Story — Répondre au questionnaire de biosécurité

**Labels :** `story`, `biosecurity-review`  
**Epic parent :** Bilan de biosécurité simplifié

En tant que vétérinaire, je veux répondre au questionnaire de biosécurité de démonstration afin de documenter les pratiques de l’élevage.

**Critères d’acceptation**

```gherkin
Scénario: Enregistrer les réponses au questionnaire
  Étant donné que le questionnaire de démonstration est affiché hors ligne
  Quand je réponds à ses questions et enregistre le bilan
  Alors les réponses sont conservées et affichées dans le bilan

Scénario: Signaler les réponses manquantes
  Étant donné que le questionnaire comporte une question obligatoire sans réponse
  Quand je tente d’enregistrer le bilan
  Alors l’application identifie la question sans réponse
  Et n’indique pas que le questionnaire est complété
```

### Story — Afficher les pratiques prioritaires du bilan

**Labels :** `story`, `biosecurity-review`  
**Epic parent :** Bilan de biosécurité simplifié

En tant que vétérinaire, je veux voir les pratiques prioritaires déterminées par le jeu de règles fixe afin de présenter les points d’attention du bilan.

**Critères d’acceptation**

```gherkin
Scénario: Déterminer les priorités selon les réponses de démonstration
  Étant donné que le questionnaire est complété avec les réponses du jeu de test
  Quand j’affiche le bilan de biosécurité hors ligne
  Alors les réponses sont visibles
  Et les pratiques marquées prioritaires correspondent au jeu de règles fixe

Scénario: Signaler un jeu de règles indisponible
  Étant donné que les réponses sont enregistrées mais que le jeu de règles ne peut pas être lu
  Quand j’affiche le bilan
  Alors l’application affiche une erreur explicite
  Et ne présente pas une liste de priorités vide comme un résultat calculé
```
