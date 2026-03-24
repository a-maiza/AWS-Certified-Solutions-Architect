# 1- What Is IAM?

## Sujet du cours

Introduction à **AWS IAM (Identity and Access Management)** : le service de gestion des identités et des accès dans AWS, et les bonnes pratiques de sécurisation du compte root.

---

## Concepts clés

| Concept             | Définition                                                                                |
|---------------------|-------------------------------------------------------------------------------------------|
| **IAM**             | Service AWS de gestion des identités et des accès, isolé logiquement par compte AWS.      |
| **Utilisateur IAM** | Identité individuelle avec des permissions définies dans un compte AWS.                   |
| **Groupe IAM**      | Ensemble d'utilisateurs partageant les mêmes permissions.                                 |
| **Rôle IAM**        | Identité temporaire assignable à des services ou utilisateurs pour des accès spécifiques. |
| **Compte root**     | Utilisateur créé avec l'adresse email d'inscription — accès administratif total.          |

---

## Explications essentielles

### Rôle d'IAM
- IAM permet de **créer des utilisateurs, groupes et rôles** et de leur attribuer des permissions précises.
- Il contrôle **ce que chaque identité peut ou ne peut pas faire** avec les ressources et services AWS.
- C'est **le service le plus important d'AWS** — à maîtriser absolument pour l'examen et en production.

### Le compte root
- Créé automatiquement lors de l'ouverture du compte AWS (via l'adresse email d'inscription).
- Dispose d'un **accès administratif total** — extrêmement puissant, donc extrêmement risqué.
- Si compromis, un attaquant peut causer des dégâts financiers considérables.

---

## Méthodes / Raisonnements

### Sécuriser le compte root — Actions immédiates

1. **Activer le MFA** (Multi-Factor Authentication) : logiciel (ex. Google Authenticator) ou matériel (ex. YubiKey) — peu importe le choix, l'activer immédiatement.
2. **Ne pas utiliser le root pour les tâches courantes** : créer un utilisateur IAM dédié et l'utiliser à la place.
3. **Ne jamais créer de clés d'accès (*access keys*) pour le root** : des clés compromises donnent un accès programmatique complet au compte, aussi dangereux qu'un mot de passe volé.

### Cas d'usage légitimes du compte root (rares)
- Modifier les informations de facturation.
- Fermer le compte AWS.

---

## Points à retenir

- **IAM = gestion des utilisateurs et contrôle de leurs accès** dans un compte AWS.
- Le compte root est **à sécuriser en priorité absolue** dès la création du compte.
- **MFA obligatoire** sur le root ; utilisation du root à éviter au maximum.
- **Jamais de clés d'accès sur le root** — risque de compromission programmatique totale.
- Les notions de groupes, rôles et clés d'accès seront détaillées dans les modules suivants.

# 2- Demo: Securing the AWS Root Account

## Sujet du cours

Démonstration pratique de la **création d'un compte AWS** et de la **sécurisation immédiate du compte root** via l'activation du MFA (Multi-Factor Authentication).

---

## Méthodes / Raisonnements

### Étapes de création d'un compte AWS
1. Fournir une **adresse email root** et un **nom de compte**.
2. **Vérifier l'adresse email** via le code envoyé par AWS.
3. Définir un **mot de passe complexe** (utiliser un gestionnaire de mots de passe recommandé).
4. Compléter les informations de contact et de facturation.

### Activer le MFA sur le compte root

1. Une fois connecté, aller dans le menu compte (haut droite) → **Security credentials**.
    - Alternative : rechercher le service **IAM** dans la console.
2. Dans la section **Multi-Factor Authentication**, cliquer sur **Assign MFA device**.
3. Donner un **nom au dispositif** (ex. `google-auth`) pour l'identifier facilement.
4. Choisir le **type de dispositif** :
    - **Authenticator app** (ex. Google Authenticator) — utilisé dans la démo.
    - **Passkey / Security key** (ex. YubiKey).
    - **Hardware token**.
5. Scanner le **QR code** avec l'application d'authentification.
    - Si le QR code ne fonctionne pas : utiliser le bouton **Show secret key** pour saisir la clé manuellement.
6. Entrer **deux codes MFA consécutifs** générés par l'application, puis cliquer sur **Add MFA**.

### Vérification
- Se déconnecter et se reconnecter : AWS demande désormais le code MFA après le mot de passe → le compte root est sécurisé.

---

## Points à retenir

- **Activer le MFA immédiatement** après la création du compte — c'est la première action de sécurité.
- Le choix du dispositif MFA dépend des exigences de sécurité ; une **application d'authentification** est la solution la plus accessible.
- Si le QR code est inaccessible, la **clé secrète manuelle** permet tout de même de configurer l'app.
- Après activation du MFA, **toute connexion root nécessite le code MFA** en plus du mot de passe.
- Ne pas utiliser le compte root pour les tâches courantes — créer un utilisateur IAM dédié à la place.


# 3- Module Summary and Exam Tips — IAM & Root User

## Sujet du cours

Récapitulatif des points essentiels du module IAM et conseils clés pour l'examen, centrés sur les caractéristiques d'IAM et la sécurisation du compte root.

---

## Points à retenir

### IAM — Rappels fondamentaux
- IAM est un **service global** : il offre une base d'authentification **unique et isolée** par compte AWS.
- Aucun autre compte AWS n'a accès à votre base IAM.

### Compte root — Ce qu'il faut absolument savoir
- Le root dispose d'un accès **total et non fédéré** à tout le compte : ressources, facturation, fermeture du compte.
- **Activer le MFA immédiatement** après la création du compte.
- **Définir un mot de passe fort** pour le root (et appliquer une politique de mot de passe robuste à IAM en général).
- **Ne jamais utiliser le root pour les tâches courantes** — créer un utilisateur IAM dédié à la place.
- L'adresse email root doit être **unique par compte AWS** — elle ne peut pas être réutilisée entre comptes.

---

## Conseils pratiques (Exam Tips)

- **MFA + mot de passe fort** = première ligne de défense indispensable pour le root.
- Utiliser des **alias d'adresse email** pour les comptes root de plusieurs comptes AWS : pratique courante permettant de centraliser la gestion dans une seule boîte mail.
- Sur l'examen : si un scénario mentionne une action nécessitant le compte root (modifier la facturation, fermer le compte), c'est un indicateur clé — **seul le root peut faire ces actions**.
- Retenir la règle d'or : **le root ne doit être utilisé que si absolument nécessaire**.