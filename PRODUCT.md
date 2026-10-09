# TournéeVéto — contexte produit

## 1. Problème

- Une visite d’élevage exige de retrouver et de recouper des données individuelles (santé, généalogie, reproduction) et des actions à planifier; l’ordre de grandeur du temps consacré à cette préparation est **à vérifier**.
- Dans les étables sans réseau fiable, les outils en ligne sont inaccessibles; les informations utiles doivent rester consultables et saisissables hors ligne.
- Le vétérinaire doit aussi garder une trace exploitable de la visite et repérer les pratiques de biosécurité prioritaires, sans multiplier les sources d’information.

## 2. Personas

### Médecin vétérinaire en production laitière
- **Objectif :** préparer et réaliser les visites, suivre les animaux et consigner les constats et actions à effectuer.
- **Frustration :** devoir retrouver des informations dispersées ou être privé d’un outil faute de réseau.
- **Contexte d’usage :** préparation au bureau, puis consultation et saisie sur le terrain, notamment dans les étables hors connexion.

### Producteur laitier
- **Objectif :** consulter les informations de son élevage et suivre les animaux, les actions de régie et les éléments documentés lors des visites.
- **Frustration :** devoir rassembler les informations du troupeau à partir de plusieurs supports et ne pas pouvoir y accéder dans les zones sans réseau.
- **Contexte d’usage :** consultation et suivi de l’élevage à la ferme, parfois hors connexion.

Le vétérinaire et le producteur sont les profils visés. Le POC ne prévoit ni comptes ni permissions différenciées; les données restent locales au navigateur utilisé.

## 3. Proposition de valeur et parcours clés

**Proposition de valeur :** TournéeVéto rassemble les informations utiles à la visite d’élevage laitier dans une application locale utilisable hors ligne.

1. **Préparer la tournée :** ouvrir la tournée du jour, choisir ou importer un élevage (CSV), consulter sa fiche et sa grille de régie, puis repérer les actions et examens à échéance.
2. **Réaliser la visite :** consulter les fiches individuelles (généalogie, santé, statuts reproducteurs et photos), ajouter les événements observés et examiner le bilan de biosécurité et ses pratiques prioritaires.
3. **Clore la visite :** produire un rapport imprimable avec les statuts reproducteurs et les événements consignés pendant la visite.

## 4. Hors périmètre du POC

- Backend, comptes utilisateurs, authentification, partage ou synchronisation distante des données.
- Fonctionnement nécessitant une connexion Internet; les données sont stockées localement dans le navigateur.
- Diagnostic ou décision médicale automatisés, prescriptions et intégrations à des équipements ou systèmes tiers.
- Règles métier exhaustives ou validation clinique : les données d’exemple sont **fictives** et les règles métier **simplifiées**.

Le POC est une application web progressive (PWA), publiée sur GitHub Pages. Les écrans doivent pouvoir être réutilisés dans les applications Windows (WPF) et mobile (MAUI); cela ne suppose ni backend ni synchronisation entre plateformes.

## 5. Glossaire

- **Régie :** organisation et suivi des interventions, soins et étapes de production d’un animal ou d’un troupeau.
- **Vêlage :** mise bas d’une vache.
- **Tarissement :** période précédant le vêlage pendant laquelle la traite est interrompue.
- **Insémination :** dépôt de semence dans l’appareil reproducteur de la femelle en vue d’une fécondation.
- **Diagnostic de gestation :** examen visant à déterminer si une femelle est gestante.
- **CCS :** comptage des cellules somatiques du lait, indicateur utilisé dans le suivi de la santé mammaire.
- **Biosécurité :** mesures visant à prévenir l’introduction et la propagation d’agents infectieux dans un élevage.
- **Élevage :** troupeau et exploitation agricole suivis dans l’application.
- **Visite :** intervention du vétérinaire dans un élevage, avec ses observations, événements et actions consignés.
