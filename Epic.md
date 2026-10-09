# Backlog du POC TournéeVéto

Backlog dérivé de [`docs/mvp.md`](./docs/mvp.md). Toutes les données et règles métier restent fictives et simplifiées, conformément à [`PRODUCT.md`](./PRODUCT.md).

Chaque issue Epic porte l'étiquette `epic` et une étiquette propre à la fonctionnalité. Ses user stories portent l'étiquette `story` et cette même étiquette de fonctionnalité.

---

## Epic — Liste de tournée du jour

**Étiquettes :** `epic`, `tournee-du-jour`

**Objectif :** permettre au vétérinaire de préparer et consulter la liste des élevages à visiter aujourd'hui.

### Story — Ajouter un élevage à la tournée

**Étiquettes :** `story`, `tournee-du-jour`

En tant que vétérinaire praticien, je veux ajouter un élevage à la tournée du jour afin de préparer les visites que je dois réaliser.

**Critères d'acceptation**

```gherkin
Scénario: Ajouter un élevage connu
  Étant donné que je consulte la tournée du jour
  Quand j'ajoute un élevage disponible dans les données locales
  Alors cet élevage apparaît dans la liste de la tournée

Scénario: Refuser un élevage déjà présent
  Étant donné qu'un élevage figure déjà dans la tournée du jour
  Quand je tente de l'ajouter une seconde fois
  Alors l'application ne crée pas de doublon et m'indique que l'élevage est déjà présent
```

### Story — Consulter la tournée du jour

**Étiquettes :** `story`, `tournee-du-jour`

En tant que vétérinaire praticien, je veux consulter les élevages de ma tournée du jour afin de retrouver rapidement les visites à réaliser.

**Critères d'acceptation**

```gherkin
Scénario: Afficher les élevages prévus
  Étant donné que plusieurs élevages sont inscrits à la tournée du jour
  Quand j'ouvre la liste de tournée
  Alors chaque élevage inscrit est affiché

Scénario: Afficher une tournée vide
  Étant donné qu'aucun élevage n'est inscrit à la tournée du jour
  Quand j'ouvre la liste de tournée
  Alors un état vide m'indique qu'aucune visite n'est prévue
```

---

## Epic — Fiche élevage hors ligne

**Étiquettes :** `epic`, `fiche-elevage`

**Objectif :** rendre consultables hors ligne l'identité, le résumé du cheptel et l'historique court d'un élevage.

### Story — Consulter l'identité et le cheptel

**Étiquettes :** `story`, `fiche-elevage`

En tant que vétérinaire praticien, je veux consulter l'identité et le résumé du cheptel d'un élevage afin de disposer de ses informations de référence pendant la visite.

**Critères d'acceptation**

```gherkin
Scénario: Afficher une fiche disponible localement hors ligne
  Étant donné que la fiche d'un élevage est déjà disponible sur l'appareil
  Et que l'appareil est hors ligne
  Quand j'ouvre cette fiche
  Alors l'identité et le résumé du cheptel s'affichent sans erreur réseau

Scénario: Signaler une fiche indisponible
  Étant donné que la fiche demandée n'est pas disponible sur l'appareil
  Quand j'essaie de l'ouvrir hors ligne
  Alors l'application indique que la fiche est indisponible et ne présente pas de données fictives comme si elles étaient réelles
```

### Story — Consulter l'historique court

**Étiquettes :** `story`, `fiche-elevage`

En tant que vétérinaire praticien, je veux consulter l'historique court d'un élevage afin de prendre connaissance des visites précédentes utiles.

**Critères d'acceptation**

```gherkin
Scénario: Afficher l'historique local
  Étant donné qu'un élevage possède des entrées d'historique enregistrées localement
  Quand j'ouvre sa fiche hors ligne
  Alors les entrées disponibles de son historique court sont affichées

Scénario: Afficher l'absence d'historique
  Étant donné qu'aucune entrée d'historique n'est enregistrée pour l'élevage
  Quand j'ouvre sa fiche
  Alors l'application indique qu'aucun historique n'est disponible
```

---

## Epic — Grille de régie

**Étiquettes :** `epic`, `grille-de-regie`

**Objectif :** permettre la saisie des actions de régie par vache avec sauvegarde locale immédiate.

### Story — Saisir les actions de régie

**Étiquettes :** `story`, `grille-de-regie`

En tant que vétérinaire praticien, je veux cocher ou saisir les actions de régie d'une vache afin de consigner les constats réalisés pendant la visite.

**Critères d'acceptation**

```gherkin
Scénario: Consigner une action de régie
  Étant donné que j'ai ouvert la grille d'un élevage contenant des vaches
  Quand je coche ou renseigne une action parmi vêlage, tarissement, insémination ou diagnostic de gestation
  Alors la valeur saisie est associée à la vache concernée

Scénario: Empêcher une saisie sur une vache introuvable
  Étant donné qu'une vache n'appartient pas au cheptel de l'élevage ouvert
  Quand une action est demandée pour cette vache
  Alors l'application refuse la saisie et indique que la vache est introuvable dans cet élevage
```

### Story — Sauvegarder et retrouver la grille

**Étiquettes :** `story`, `grille-de-regie`

En tant que vétérinaire praticien, je veux que mes modifications de grille soient sauvegardées localement dès leur saisie afin de ne pas perdre mes constats hors ligne.

**Critères d'acceptation**

```gherkin
Scénario: Retrouver les actions après rechargement hors ligne
  Étant donné que j'ai enregistré plusieurs actions dans la grille
  Quand je recharge l'application sans réseau puis rouvre la grille
  Alors les actions précédemment enregistrées sont toujours présentes

Scénario: Signaler un échec de sauvegarde locale
  Étant donné que le stockage local ne peut pas enregistrer une modification
  Quand je modifie une action de la grille
  Alors l'application m'indique explicitement que la sauvegarde a échoué et que la modification n'est pas confirmée
```

---

## Epic — Parcours intégral hors ligne et PWA

**Étiquettes :** `epic`, `parcours-hors-ligne`

**Objectif :** rendre l'application installable et permettre le parcours tournée → fiche → grille → rapport sans réseau, grâce au précache des ressources nécessaires.

### Story — Installer l'application

**Étiquettes :** `story`, `parcours-hors-ligne`

En tant que vétérinaire praticien, je veux installer TournéeVéto comme une PWA afin de retrouver l'application sur ma tablette pendant mes visites.

**Critères d'acceptation**

```gherkin
Scénario: Installer l'application sur un navigateur compatible
  Étant donné que les ressources de l'application ont été chargées et que le navigateur est compatible
  Quand je choisis d'installer TournéeVéto
  Alors l'application peut être ajoutée à l'appareil et s'ouvre comme une application installée

Scénario: Signaler l'indisponibilité de l'installation
  Étant donné que le navigateur ne prend pas en charge l'installation PWA
  Quand je consulte les options d'installation
  Alors l'application reste utilisable dans le navigateur et n'affiche pas une installation comme réussie
```

### Story — Parcourir les écrans sans réseau

**Étiquettes :** `story`, `parcours-hors-ligne`

En tant que vétérinaire praticien, je veux parcourir les écrans de tournée, fiche, grille et rapport sans réseau afin de réaliser une visite en bâtiment d'élevage.

**Critères d'acceptation**

```gherkin
Scénario: Parcourir les écrans précachés en mode avion
  Étant donné que l'application a été chargée et que ses ressources nécessaires sont précachées
  Quand je coupe le réseau puis parcours tournée, fiche, grille et rapport
  Alors chaque écran s'affiche sans erreur 404 ni erreur de connexion

Scénario: Signaler une ressource locale manquante
  Étant donné qu'une ressource nécessaire n'est pas disponible dans le cache hors ligne
  Quand je demande l'écran qui en dépend sans réseau
  Alors l'application affiche une erreur explicite au lieu d'un écran blanc ou d'un faux succès

Scénario: Respecter le seuil de qualité PWA
  Étant donné que l'audit Lighthouse est exécuté sur la version du POC
  Quand le critère offline est évalué
  Alors le score PWA atteint au moins 90
```

---

## Epic — Rapport de visite exportable

**Étiquettes :** `epic`, `rapport-visite`

**Objectif :** générer un rapport simple exportable qui restitue l'identité de l'élevage, les actions de la grille et la date de visite.

### Story — Générer le rapport de visite

**Étiquettes :** `story`, `rapport-visite`

En tant que vétérinaire praticien, je veux générer un rapport de visite contenant les informations essentielles afin de restituer les constats de l'élevage.

**Critères d'acceptation**

```gherkin
Scénario: Générer un rapport avec les sections attendues
  Étant donné qu'une visite contient un élevage et des actions de grille enregistrées
  Quand je génère le rapport
  Alors le rapport contient l'identité de l'élevage, les actions de la grille et la date de visite

Scénario: Signaler l'absence de données de visite
  Étant donné qu'aucune visite exploitable n'est sélectionnée
  Quand je demande la génération d'un rapport
  Alors l'application m'indique qu'aucun rapport ne peut être généré pour cette visite
```

### Story — Exporter le rapport

**Étiquettes :** `story`, `rapport-visite`

En tant que vétérinaire praticien, je veux exporter le rapport sous forme de texte ou de PDF simple afin de le partager ou de l'archiver.

**Critères d'acceptation**

```gherkin
Scénario: Télécharger un rapport non vide
  Étant donné qu'un rapport a été généré pour une visite
  Quand je lance son export
  Alors un fichier non vide est téléchargé et contient les sections attendues

Scénario: Signaler l'échec de l'export
  Étant donné que le navigateur ne peut pas créer ou télécharger le fichier
  Quand je lance l'export du rapport
  Alors l'application m'indique explicitement que l'export a échoué
```

---

## Epic — Données locales et absence d'appels sortants

**Étiquettes :** `epic`, `donnees-locales`

**Objectif :** conserver les données de visite dans IndexedDB sur l'appareil et ne déclencher aucun appel réseau sortant pendant le parcours de visite.

### Story — Conserver les données dans IndexedDB

**Étiquettes :** `story`, `donnees-locales`

En tant que vétérinaire praticien, je veux que mes données de tournée et de visite soient stockées dans IndexedDB sur mon appareil afin de les retrouver sans compte ni serveur.

**Critères d'acceptation**

```gherkin
Scénario: Retrouver la tournée après fermeture de l'onglet
  Étant donné que trois élevages ont été ajoutés à la tournée et enregistrés dans IndexedDB
  Quand je ferme puis rouvre l'application en mode avion
  Alors les trois élevages sont toujours listés

Scénario: Signaler l'indisponibilité du stockage local
  Étant donné qu'IndexedDB est indisponible ou que son accès est refusé
  Quand l'application tente d'enregistrer des données de visite
  Alors elle m'indique explicitement que les données ne sont pas sauvegardées
```

### Story — Ne pas transmettre les données pendant la visite

**Étiquettes :** `story`, `donnees-locales`

En tant que vétérinaire praticien, je veux que le parcours de visite ne transmette aucune donnée vers un serveur afin de préserver la confidentialité des données d'élevage.

**Critères d'acceptation**

```gherkin
Scénario: Effectuer le parcours sans appel applicatif sortant
  Étant donné que les ressources statiques de l'application sont chargées
  Quand je parcours tournée, fiche, grille et rapport
  Alors aucune requête XHR ou fetch sortante n'est déclenchée

Scénario: Signaler l'impossibilité de satisfaire le parcours sans réseau
  Étant donné qu'une étape du parcours tente de joindre un service distant
  Quand l'appareil est hors ligne
  Alors l'étape ne prétend pas avoir réussi et l'application indique que l'opération distante est indisponible
```