# GestTravaux Pro

## Cahier des charges - Système de gestion de travaux immobiliers

### **Présentation générale du projet**

#### **Contexte métier**

La société IMMOSYNC est une société de syndic proposant des services de gérance de biens immobiliers. À ce titre, elle doit assurer le maintien en état des biens immobiliers en faisant réaliser des travaux dans les appartements et parties communes.

Lorsque des travaux sont nécessaires pour un bien, on établit un chantier. 

Une fois le chantier créé, on définit un modèle type de devis qui comprendra toutes les prestations (pose carrelage salle de bain, changer baignoire, pose parquet …) à réaliser.

Le chantier portera sur un bien qui appartient à un seul propriétaire.

On associe un inspecteur pour chaque chantier. Ce dernier devra établir des documents (diagnostic bruit, DPE ...) ainsi que des photos pour éventuellement expliquer les différents travaux à faire.

Le chantier sera proposé à 1 ou plusieurs entrepreneurs en fonction de la distance entre le bien et l’adresse de l’entrepreneur.

Chaque entrepreneur ayant reçu un chantier, pourra proposer son devis avec ses différentes prestations à partir du devis type.

L’application devra permettre de comparer tous les devis reçus pour un chantier afin de choisir l’entrepreneur qui réalisera les travaux. Ce choix se fera sur le prix du devis bien évidemment mais également sur celui qui commencera les travaux le plus rapidement possible.

Chaque entrepreneur est spécialisé dans une catégorie : plomberie, électricité, maçonnerie …

Chaque prestation appartient à une catégorie.

Cette mission est aujourd'hui assurée par une équipe de 3 personnes selon le processus suivant :

- Déterminer les travaux à réaliser par inspection sur site
- Identifier et contacter les entrepreneurs qualifiés
- Organiser la mise en concurrence via des appels d'offres
- Étudier les propositions et négocier les coûts avec validation des propriétaires
- Superviser l'avancement des chantiers
- Réceptionner les travaux et établir les procès-verbaux
- Gérer le suivi des règlements financiers

#### **Problématique**

Le processus actuel présente plusieurs défis :

- Gestion manuelle chronophage et source d'erreurs
- Communication dispersée entre les différents acteurs
- Suivi difficile de l'avancement des chantiers multiples
- Archivage papier peu pratique et non sécurisé
- Manque de traçabilité dans les échanges et décisions

#### **Objectifs du projet**

**Objectif principal :** Digitaliser et moderniser le processus de gestion des travaux immobiliers pour améliorer la productivité et la qualité de service.

#### **Objectifs spécifiques :**
- Réduire de 40% le temps de traitement des dossiers
- Améliorer la traçabilité des échanges et décisions
- Faciliter la communication entre tous les acteurs
- Centraliser l'information dans une base de données unique
- Optimiser la gestion des délais et budgets

### **Périmètre et acteurs du système**

#### **Acteurs et interfaces**

| Acteur | Interface | Justification |
| ----- | ----- | ----- |
| Gestionnaire IMMOSYNC | Application Java Desktop | Travail de bureau intensif, analyses complexes |
| Inspecteur | Application Web Mobile | Mobilité terrain, saisie sur tablette/smartphone |
| Entrepreneur | Application Web | Accès occasionnel, simplicité d'usage |
| Propriétaire | Application Web | Consultation/validation ponctuelle des chantiers |
| Administrateur système | Application Web | Administration distante |

#### **Architecture applicative**

##### **Application Web Symfony 7 :**

- Interface inspecteur mobile (PWA) pour évaluations terrain
- Espace entrepreneur pour soumission et suivi des devis
- Espace propriétaire pour consultations
- Interface d'administration système
- Accès direct à MySQL via Doctrine ORM

##### **Application Java Desktop :**

- Interface gestionnaire pour pilotage global des chantiers
- Comparateur de devis avancé avec analyses multi-critères
- Génération de rapports et tableaux de bord
- Accès direct à MySQL via Hibernate ORM

##### **Base de données MySQL unique :**

- Partagée entre les deux applications
- Gestion de la concurrence par les SGBD
- Sauvegarde centralisée
- Intégrité référentielle garantie

#### **Périmètre fonctionnel**

##### **Inclus dans le projet :**

- Gestion complète du cycle de vie des chantiers
- Interface web responsive avec PWA pour mobilité
- Application desktop Java pour gestion administrative
- Base de données MySQL partagée
- Système de notifications par email
- Génération de rapports PDF

##### **Exclu du projet :**

- Interface avec logiciels comptables tiers
- Gestion des stocks de matériaux
- Planning détaillé des équipes d'intervention
- Facturation automatisée

#### **Spécifications fonctionnelles détaillées**

##### **Fonctionnalité 1**

**Description :** Permettre la gestion globale de l’application. Vous devrez prévoir les opérations usuelles de gestion (création, modification, consultation) des entités suivantes :

* Entrepreneurs \+ catégorie entrepreneur

* Propriétaires

* Biens

* Prestations \+ catégorie prestation

**Acteurs concernés :** Gestionnaire (Java)

##### **Fonctionnalité 2 : Création d’un chantier**

**Description :** Permettre la création d'un nouveau chantier et l'établissement d'un devis type suite à une inspection sur site.

**Acteurs concernés :** Gestionnaire (Java), Inspecteur (Web Mobile)

**Processus détaillé :**

***Côté Gestionnaire (Application Java) :***

 - Création du dossier chantier avec informations du bien
 - Création du devis type avec les prestations nécessaires aux différents travaux
 - Assignation de l'inspecteur
 - Consultation des rapports d'inspection : documents \+ photos
 - Validation du devis préliminaire

***Côté Inspecteur (Interface Web Mobile) :***

- Consultation des chantiers assignées
- Prévoir une Map afin de localiser le bien immobilier
- Saisie des observations avec formulaires adaptatifs
- Prise de photos
- Ajout des documents (Diagnostic de performance énergétique : DPE, diagnostic bruit …)

##### **Fonctionnalité 3 : Sollicitation des entrepreneurs**

**Description :** Une fois le chantier complété et validé par le propriétaire, On doit pouvoir sélectionner et contacter automatiquement les entrepreneurs qualifiés dans un rayon géographique déterminé.

Acteurs concernés : Gestionnaire (Java)

**Processus détaillé (Application Java) :**

- Proposer le chantier avec le devis type aux entrepreneurs sélectionnés

**Fonctionnalités techniques Java :**

- Algorithmes géographiques pour calcul de distances
- Moteur de templates pour génération de documents
- Client SMTP intégré pour envoi automatique

##### **Fonctionnalité 4 : Espace entrepreneur dédié**

**Description :** Interface web Symfony permettant aux entrepreneurs de consulter les demandes de chantiers et soumettre leurs propositions.

Un entrepreneur pourra décider de valider ou pas une proposition de chantier.

Acteurs concernés : Entrepreneur (Web)

**Fonctionnalités Web Symfony :**

- Dashboard personnalisé avec liste des demandes
- Consultation détaillée du devis type
- Formulaires de soumission avec validation Symfony
- Upload de devis PDF avec VichUploaderBundle
- Suivi du statut des propositions soumises
- Messagerie simple avec notifications email

##### **Fonctionnalité 5 : Comparateur de devis**

**Description :** Outil d'aide à la décision pour analyser et comparer les propositions des devis reçues par les entrepreneurs.

Acteurs concernés : Gestionnaire (Java)

**Fonctionnalités Java avancées :**

- Interface graphique riche : jeu de couleurs
- Algorithmes de comparaison multi-critères pondérés : la comparaison entre les différents devis devra se faire sur les critères suivants :
- La date de début des travaux la plus récente
- Le prix le moins onéreux

##### **Fonctionnalité 6 : Suivi d'avancement des chantiers**

**Description :** Monitoring en temps réel de l'avancement des travaux avec système d'alertes.

**Répartition des fonctionnalités :**

Interface Web (Entrepreneur \+ Inspecteur) :

- Mise à jour mobile de l'avancement par l'entrepreneur
- Formulaires étapes selon corps de métier
- Upload photos d'avancement avec géolocalisation
- Validation inspecteur sur site via interface mobile

### **Application Java (Gestionnaire) :**

- Planning Gantt interactif avec bibliothèque JFreeGantt
- Tableau de bord temps réel avec indicateurs colorés
- Système d'alertes automatique avec notifications desktop
- Rapports d'avancement automatiques et personnalisables

##### **Fonctionnalité 7 : Réception des travaux**

**Description :** Processus dématérialisé de réception avec gestion des réserves et validation finale.

**Interface Web Mobile (Inspecteur) :**

- Grilles de contrôle dynamiques selon type de travaux
- Saisie de réserves avec photos et descriptions détaillées
- Signature électronique sur tablette avec Canvas HTML5
- Génération PV automatique au format PDF

**Application Java (Gestionnaire) :**

- Workflow de validation avec règles métier configurable
- Génération documentaire complète (PV, courriers, avenants)

## **Livrables techniques**

## **Attendus spécifiques par technologie**

**Symfony 7 :**

- Configuration Doctrine avec entités mappées
- Système d'authentification multi-rôles fonctionnel
- Formulaires avec validation et upload de fichiers 
- Templates Twig responsive avec héritage
- Controllers avec injection de dépendances
- Tests PHPUnit avec au moins 60% de couverture

**Java Desktop :**

- Interface JavaFX avec architecture MVC
- Persistance Hibernate avec configuration XML/annotations 
- Services métier avec gestion des transactions
- Génération de rapports PDF
- Tests JUnit avec mocks et intégration
- Package JAR exécutable avec dépendances

**Base de données MySQL :**

- Schéma normalisé en 3FN minimum
- Index optimisés pour les requêtes fréquentes
- Contraintes d'intégrité référentielle
- Jeu de données de test réaliste
- Scripts de sauvegarde/restauration

## **Les versions \+ planning**

Chaque équipe devra rendre un seul projet opérationnel aux dates ci-dessous en respectant les fonctionnalités demandées.

Chaque « release » suivante devra prendre en compte les correctifs de la release précédente.

| DEADLINE | APP | ROADMAP |
| :---: | :---: | :---- |
| 24/10/2025 | Java | Template \+ configuration du projet Base de données opérationnelle \+ jeu d’essais Fonctionnalité 1 et fonctionnalité 2 |
| 24/10/2025 | Symfony | Template \+ configuration du projet Base de données opérationnelle \+ jeu d’essais Fonctionnalité 2 |
| 19/12/2025 | Java | Fonctionnalité 3 |
| 19/12/2025 | Symfony | Fonctionnalité 4 |
| 27/03/2026 | Java | Fonctionnalité 5 |
| 27/03/2026 | Symfony | Projet final opérationnel \+ documentation technique et utilisatrice. |

## **Les equipes**

**Groupe 1**

|        NOM        | OPTION | GR  |
|:-----------------:| :---: |:----|
|  ABERKANE	Anaïs   | SLAM | GR1 |
|  BENBRIKHO Amine  | SLAM | GR1 |
| DEVINEAU	Thibault | SLAM | GR1 |
|  GARNIER	Julien   | SISR | GR1 |

**Groupe 2**

| NOM | OPTION | GR |
| :---: | :---: | :---- |
| BEHAR	Sammy | SLAM | GR2 |
| OUGHLIS	Mohamed | SLAM | GR2 |
| THIRUVARUCHELVAN	Kirdigan | SISR | GR2 |

**Groupe 3**

| NOM | OPTION | GR  |
| :---: | :---: |:----|
| EMILE-GUILLOT	Anthony | SLAM | GR3 |
| AMBROISE	Ihlane | SLAM | GR3 |
| QIU	Jing Hui Terry | SLAM | GR3 |
| CHIROUX	Victor | SISR | GR3 |

**Groupe 4**

| NOM | OPTION | GR |
| :---: | :---: | :---- |
| ANDOH	Claude | SLAM | GR5 |
| BOUTIBA	Sami | SLAM | GR5 |
| GLEIZES	Alexandre | SLAM | GR5 |
| FUENTES	Ethan | SISR | GR5 |

**Groupe 5**

| NOM | OPTION | GR |
| :---: | :---: | :---- |
| BILL	Ruben | SLAM | GR6 |
| BOUIBCHA	Ziyad | SLAM | GR6 |
| BAYA BAHA	Sara-Christel | SLAM | GR6 |
| AZIZ	Saem | SISR | GR6 |

**Groupe 6**

| NOM | OPTION | GR |
| :---: | :---: | :---- |
| ERDEM	Roni | SLAM | GR7 |
| MASSE-REYES	Pablo | SLAM | GR7 |
| DOAMENYO	Ismael | SISR | GR7 |

**Groupe 7**

| NOM | OPTION | GR |
| :---: | :---: | :---- |
| MINEIRO	Florent | SLAM | GR8 |
| OURAGA	Yann | SLAM | GR8 |
| SILLION	Thomas | SISR | GR8 |