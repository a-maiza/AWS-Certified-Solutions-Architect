# Reviewing the Exam Guide and Domains

## Sujet du cours

Présentation de l'**examen AWS Certified Solutions Architect Associate** : structure, domaines, conseils pratiques et stratégies pour réussir.

---

## Concepts clés

| Élément | Détail |
|---|---|
| **Nombre de questions** | 65 (dont 15 non notées, indistinguables) |
| **Types de questions** | QCM (1 bonne réponse) / QRM (2+ bonnes réponses) |
| **Durée** | 130 min (+ 30 min si anglais langue étrangère) |
| **Score de passage** | 720 / 1000 (score pondéré) |
| **Expérience recommandée** | 1 an de pratique AWS |

---

## Explications essentielles

### Objectif de l'examen
Valider la capacité à **concevoir des architectures AWS** conformes au Well-Architected Framework : sécurisées, résilientes, performantes et optimisées en coûts, en réponse à des scénarios métier réels.

### Les 4 domaines de l'examen

| Domaine                                        | Poids |
|------------------------------------------------|-------|
| **1. Designing Secure Architectures**          | 30%   |
| **2. Designing Resilient Architectures**       | 26%   |
| **3. Designing High-Performing Architectures** | 24%   |
| **4. Designing Cost-Optimized Architectures**  | 20%   |

### Détail de chaque domaine

**1. Secure Architectures (30%)**
- Concevoir des accès sécurisés aux ressources AWS (IAM, contrôles d'accès).
- Sécuriser les workloads et applications (ports, protocoles, trafic réseau).
- Choisir les bonnes options de sécurité des données (chiffrement au repos et en transit).

**2. Resilient Architectures (26%)**
- Architectures scalables et faiblement couplées (microservices indépendants).
- Architectures hautement disponibles et/ou tolérantes aux pannes.

**3. High-Performing Architectures (24%)**
- Solutions de calcul scalables (bon type d'instance ou service managé).
- Stockage performant (serverless vs EBS).
- Réseau performant (load balancing, caching).
- Bases de données adaptées (SQL managé vs NoSQL).
- Pipelines d'ingestion et transformation de données (ETL, Data Lakes).

**4. Cost-Optimized Architectures (20%)**
- Stockage optimisé (stockage froid pour données peu accédées).
- Calcul et bases de données optimisés (bonne taille d'instance, auto-scaling).
- Architectures réseau économiques (VPC peering, accès externe).

---

## Méthodes / Raisonnements

### Stratégies pour l'examen
1. **Pratiquer en conditions réelles** : utiliser des labs et playgrounds pour apprendre par l'expérience.
2. **Repérer les mots-clés** dans chaque scénario pour identifier rapidement la bonne piste de réponse.
3. **Éliminer les distracteurs évidents** : ex. si la question demande du NoSQL, éliminer RDS immédiatement.
4. **Flaguer les questions difficiles** : répondre à tout, marquer les incertitudes, et revoir à la fin — ne jamais laisser de réponse vide.
5. **Planifier et s'y tenir** : fixer une date d'examen et organiser les révisions autour de cette échéance.

---

## Points à retenir

- Le **Well-Architected Framework est omniprésent** dans l'examen : chaque scénario y fait référence d'une façon ou d'une autre.
- Les **15 questions non notées** sont indétectables — traiter toutes les questions avec le même sérieux.
- **720/1000** est le score minimum pour être certifié.
- La **sécurité est le domaine le plus important** (30% des questions).
- Toujours lire l'**exam guide officiel** en complément du cours (disponible dans les assets du module).


# 2- Demo: Booking Your Exam

## Sujet du cours

Démonstration complète du processus de **réservation de l'examen AWS Certified Solutions Architect Associate** via le portail officiel AWS, avec recommandations pratiques sur le mode de passage.

---

## Méthodes / Raisonnements

### Étapes pour réserver l'examen

1. Aller sur **aws.training** → *Certification* → *Schedule an exam*.
2. Se connecter avec un **AWS Builder ID** (créer un compte si nécessaire ; activer le MFA recommandé).
3. Sélectionner l'examen **SAA-C03** et cliquer sur *Schedule*.
4. Choisir le **mode de passage** : en ligne (*OnVUE*) ou en **centre de test**.
5. Sélectionner la **langue** (anglais ou autre — Extended Time disponible si anglais langue étrangère).
6. Lire et accepter les **politiques d'examen** (conditions d'utilisation, règles d'espace de travail).
7. Choisir la **langue du proctor**, le **fuseau horaire**, la **date** et l'**heure**.
8. Valider le panier et procéder au **paiement** (~150 USD).

### Exigences techniques pour le passage en ligne (OnVUE)
- Caméra et microphone **obligatoires** (enregistrement vidéo, audio et écran).
- Bureau **entièrement dégagé** (rien sur le bureau, un seul écran, rien de branché).
- Environnement calme et isolé.

---

## Exemples importants

- **En ligne (OnVUE)** : pratique si pas de centre de test accessible, mais contraintes d'espace de travail strictes et risques de problèmes réseau.
- **Centre de test** : environnement standardisé, matériel dédié, proctor sur place — recommandé pour éviter les complications techniques.

---

## Points à retenir

- Utiliser **aws.training** pour toute inscription à un examen AWS.
- Activer le **MFA** sur son compte Builder ID pour la sécurité.
- Passage **en centre de test recommandé** : moins de contraintes techniques et environnement optimisé.
- Si l'anglais n'est pas la langue maternelle, demander le **temps supplémentaire (+30 min)** lors de l'inscription.
- **Lire les politiques d'examen** avant d'accepter — elles précisent les règles de surveillance et de traitement des données.
- Fixer une **date d'examen à l'avance** et planifier les révisions en conséquence.
- Commencer le parcours d'apprentissage par le cours **Core Services** avant de choisir la suite.