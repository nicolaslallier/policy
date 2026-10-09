# PRD – Système d'assurance collective

Oct 9, 2026 · Nicolas Lallier

## 1. Contexte, vision et problème

Nous voulons une plateforme unique pour concevoir, vendre, administrer et indemniser des contrats d'assurance collective (vie, invalidité, maladie complémentaire, dentaire) pour des groupes d'employeurs.

**Problème :** l'administration de groupe repose sur des processus manuels (fichiers Excel, courriels, saisies multiples), ce qui allonge les délais de mise en vigueur, multiplie les erreurs d'adhésion et de facturation, et limite la visibilité des employeurs et des participants.

**Vision :** un système où l'employeur gère ses employés en libre-service, le participant soumet et suit ses réclamations en ligne, et l'assureur automatise la tarification, la facturation et l'adjudication des réclamations courantes.

## 2. Objectifs et indicateurs de succès

Le succès se mesure à 12 mois après la mise en production. Les cibles sont des hypothèses de départ à valider.

| Objectif | Indicateur | Cible (à valider) |
| --- | --- | --- |
| Accélérer la mise en vigueur d'un groupe | Délai soumission acceptée → contrat actif | ≤ 10 jours ouvrables |
| Automatiser les réclamations courantes | % de réclamations adjugées sans intervention | ≥ 70 % |
| Réduire les erreurs d'administration | Retouches de facturation par cycle | ≤ 2 % |
| Adoption du libre-service | % de changements d'adhésion faits par l'employeur en ligne | ≥ 80 % |
| Satisfaction | NPS participants et administrateurs de régime | ≥ +40 |

## 3. Parties prenantes et personas

| Persona | Besoin principal | Canal |
| --- | --- | --- |
| Participant (employé) | Voir sa couverture, soumettre et suivre une réclamation, télécharger sa carte | Portail et application mobile |
| Administrateur de régime (RH de l'employeur) | Inscrire, modifier et retirer des employés; payer la prime; consulter les rapports | Portail employeur, téléversement de fichiers, API |
| Courtier / conseiller (hors portée) | Soumettre un appel d'offres, suivre le renouvellement, voir sa commission | Portail courtier |
| Souscripteur (underwriter) | Évaluer le risque, tarifer, approuver les exceptions | Poste de travail interne |
| Gestionnaire de réclamations | Adjuger, enquêter, approuver les cas complexes | Poste de travail interne |
| Finance / comptabilité | Facturation, encaissement, réserves, grand livre | Poste de travail interne |
| Conformité et audit | Traçabilité, protection des renseignements personnels | Rapports et journaux d'audit |

## 4. Portée

La phase 1 couvre le cœur administratif pour l'assurance maladie complémentaire, dans toutes les provinces et tous les territoires du Canada, pour environ 32 000 membres et 52 types de polices. Le système est construit sur mesure, sans système existant à remplacer.

**Inclus (MVP)**

- Produit : maladie complémentaire, dentaire inclus dans la même police, avec un moteur de polices générique (52 types de polices au départ)
- Soumission, tarification, souscription et mise en vigueur d'un groupe
- Gestion des adhésions (employés, personnes à charge, événements de vie)
- Facturation de groupe et encaissement
- Réclamations : soumission, adjudication, paiement
- Portails participant et employeur; gestion des réclamations à l'interne

**Exclu de la phase 1**

- Application mobile native (le portail web adaptatif suffit)
- Vie, invalidité, rentes collectives, retraite, portail courtier et coordination des prestations
- Lecteur de fraude par apprentissage automatique
- Renouvellement entièrement automatisé (phase 2)

## 5. Exigences fonctionnelles

Priorités : **P0** = indispensable au MVP, **P1** = phase 2, **P2** = souhaitable.

### 5.1 Produits et tarification

| ID | Exigence | Priorité |
| --- | --- | --- |
| PRD-01 | Le système doit permettre de configurer n'importe quelle police (garanties, montants, délais de carence, exclusions) sans développement, sans se limiter aux 52 types actuels. | P0 |
| PRD-02 | Le système doit tarifer par groupe selon l'âge, le sexe, la région, l'industrie, la taille et le niveau de couverture. | P0 |
| PRD-03 | Le système doit versionner les grilles de taux avec une date d'entrée en vigueur. | P0 |
| PRD-04 | Le système doit gérer les rabais, plafonds de renouvellement et ententes spéciales par groupe. | P1 |

### 5.2 Soumission et souscription

| ID | Exigence | Priorité |
| --- | --- | --- |
| SOU-01 | Un utilisateur interne doit pouvoir saisir une soumission avec le recensement des employés (pas de portail courtier). | P0 |
| SOU-02 | Le système doit produire une proposition tarifée et la comparer au contrat final. | P0 |
| SOU-03 | Le souscripteur doit pouvoir approuver, refuser ou contre-proposer, avec journal des décisions. | P0 |
| SOU-04 | Le système doit gérer la preuve d'assurabilité individuelle lorsque la police l'exige. | P1 |
| SOU-05 | Le système doit générer le contrat et le certificat d'assurance. | P0 |

### 5.3 Administration des adhésions

| ID | Exigence | Priorité |
| --- | --- | --- |
| ADH-01 | L'employeur doit pouvoir ajouter, modifier et retirer un employé et ses personnes à charge en ligne. | P0 |
| ADH-02 | Le système doit accepter un téléversement de fichier (CSV/Excel) avec validation et rapport d'erreurs. | P0 |
| ADH-03 | Le système doit gérer les événements de vie (mariage, naissance, changement d'emploi, départ) avec délais d'admissibilité. | P0 |
| ADH-04 | Le système doit appliquer automatiquement les délais de carence et les règles d'admissibilité (heures travaillées, catégorie d'employé). | P0 |
| ADH-05 | Le système doit conserver l'historique complet des changements, consultable par date. | P0 |

### 5.4 Facturation et encaissement

| ID | Exigence | Priorité |
| --- | --- | --- |
| FAC-01 | Le système doit générer une facture mensuelle par groupe, avec détail par employé et par garantie. | P0 |
| FAC-02 | Le système doit calculer les ajustements rétroactifs (ajouts et retraits tardifs). | P0 |
| FAC-03 | Le système doit gérer le paiement (virement, préautorisé) et le rapprochement bancaire. | P0 |
| FAC-04 | Le système doit gérer le défaut de paiement : avis, période de grâce, suspension, résiliation. | P1 |
| FAC-05 | Hors portée : commissions de courtage (pas de portail courtier). | P1 |

### 5.5 Réclamations

| ID | Exigence | Priorité |
| --- | --- | --- |
| REC-01 | Le participant doit pouvoir soumettre une réclamation en ligne avec pièces jointes. | P0 |
| REC-02 | Le système doit vérifier l'admissibilité, la couverture, les maximums annuels et les franchises. | P0 |
| REC-03 | Le système doit adjuger automatiquement les réclamations courantes selon des règles configurables. | P0 |
| REC-04 | Le système doit router les cas complexes vers un gestionnaire, avec niveaux d'approbation selon le montant. | P0 |
| REC-05 | Hors portée : dossiers d'invalidité (produit non retenu). | P1 |
| REC-06 | Le système doit gérer le paiement direct aux fournisseurs et le remboursement au participant. | P0 |
| REC-07 | Le système doit générer les relevés de prestations et lettres de décision. | P0 |

### 5.6 Portails et communications

| ID | Exigence | Priorité |
| --- | --- | --- |
| POR-01 | Le participant doit voir sa couverture, ses soldes de maximums, son historique et sa carte d'assuré numérique. | P0 |
| POR-02 | L'employeur doit voir ses factures, ses employés et ses rapports d'utilisation. | P0 |
| POR-03 | Hors portée : portail courtier. | P1 |
| POR-04 | Le système doit envoyer des notifications (courriel/texto) sur les événements clés. | P0 |
| POR-05 | Le système doit être disponible en français et en anglais. | P0 |

## 6. Exigences non fonctionnelles et conformité

Les seuils sont des hypothèses de départ; la conformité dépend de votre territoire (voir questions ouvertes).

| Catégorie | Exigence |
| --- | --- |
| Performance | Pages de portail en moins de 2 secondes (95e centile); lot de facturation de 32 000 membres en moins de 1 heure, avec une marge de croissance de ×3 |
| Disponibilité | 99,9 % pour les portails; fenêtre de maintenance hors heures ouvrables |
| Reprise après sinistre | RPO ≤ 15 minutes, RTO ≤ 4 heures |
| Sécurité | Authentification multifacteur, contrôle d'accès par rôle, chiffrement au repos et en transit, séparation des données par groupe |
| Protection des renseignements | Conformité aux lois applicables sur les renseignements personnels et de santé (ex. Loi 25 au Québec, LPRPDE); consentement, droit d'accès, minimisation, hébergement des données au Canada (exigé) |
| Réglementaire | Règles de l'organisme de réglementation applicable (toutes les provinces et les trois territoires: AMF au Québec, régulateurs provinciaux ailleurs, ACCAP), délais de réponse aux réclamations, taxes provinciales sur les primes, déclaration fiscale (feuillets) |
| Audit | Journal immuable de toute action (qui, quoi, quand), conservation selon les délais légaux |
| Accessibilité | WCAG 2.1 AA pour les portails |
| Bilinguisme | Interface, documents et correspondance en français et en anglais |
| Évolutivité | Ajout d'un produit ou d'une règle par configuration, sans redéploiement |

## 7. Intégrations, données et rapports

| Système | Objet | Mode |
| --- | --- | --- |
| Grand livre / ERP | Écritures comptables, comptes clients | API ou fichier planifié |
| Banque / paiement | Préautorisés, virements, rapprochement | Fichier ou API bancaire |
| Fournisseurs de soins | Paiement direct, éligibilité en temps réel | API / réseau de réclamation |
| Systèmes RH / paie des employeurs | Synchronisation des employés | API ou téléversement |
| Réassureur | Déclarations et cessions | Fichier planifié |
| Identité | Authentification des 3 types d'utilisateurs | SSO (OIDC) |
| Communications | Courriel, texto, impression de documents | API |

**Rapports minimaux :** ratio sinistres/primes par groupe, utilisation par garantie, tableau de bord des réclamations en attente, délais de traitement, rapports réglementaires et financiers, historique des primes par groupe.

## 8. Hypothèses, risques, dépendances

| Risque | Impact | Atténuation |
| --- | --- | --- |
| Chargement initial des 32 000 membres et de leurs polices | Élevé | Chargement par groupe avec validation et rapprochement |
| Complexité des règles de produits par groupe | Élevé | Moteur de polices générique, validé sur les 52 types existants |
| Qualité des données des employeurs | Moyen | Validation à l'import et rapport d'erreurs |
| Changements réglementaires en cours de projet | Moyen | Revue de conformité à chaque jalon |
| Absence de budget et d'échéance | Moyen | Fixer un budget et une cible avant la phase MVP |

**Hypothèses :** toutes les provinces et territoires dès le départ; réclamations gérées à l'interne; aucun système d'administration existant; construction sur mesure; ni budget ni échéance fixés.

## 9. Jalons et livraison par phases

Feuille de route : 4 phases, 3 portes de décision.

1. **Cadrage** : exigences validées, bâtir ou acheter, architecture cible. *Porte : budget approuvé.*
2. **MVP** : maladie complémentaire, adhésions, facturation, réclamations (base). *Porte : pilote réussi.*
3. **Extension** : 52 types de polices, rapports de gestion, défaut de paiement, cas complexes et audit. *Porte : groupes migrés.*
4. **Optimisation** : renouvellement automatique, rapports avancés, détection de fraude.

Chaque phase est franchie par une porte de décision. Les durées restent à fixer une fois le budget et l'équipe connus.

## 10. Questions ouvertes à valider

**Décidé**

- [x] Territoire : toutes les provinces et tous les territoires du Canada
- [x] Produit : maladie complémentaire, dentaire inclus dans la même police
- [x] Moteur : générique, capable de configurer n'importe quelle police
- [x] Volume : 32 000 membres, 52 types de polices au départ
- [x] Approche : construction sur mesure, sans système existant
- [x] Réclamations : gérées à l'interne
- [x] Budget et échéance : aucun fixé pour l'instant
- [x] Portail courtier : non
- [x] Coordination des prestations : non
- [x] Hébergement des données : au Canada
- [x] Validation du produit et de la réglementation : équipe de conformité
