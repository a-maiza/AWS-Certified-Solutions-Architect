# 1- What Is AWS CloudShell?

## Sujet du cours

Présentation d'**AWS CloudShell** : un shell intégré à la console AWS permettant d'interagir avec les ressources AWS sans configuration locale.

---

## Concepts clés

- **AWS CloudShell** : shell navigateur pré-authentifié, intégré directement à la console AWS.
- **Session pré-authentifiée** : utilise automatiquement les credentials de l'identité connectée (utilisateur IAM ou rôle assumé).
- **Logiciels pré-installés** : nombreux outils et programmes courants disponibles dès l'ouverture, sans installation manuelle.

---

## Explications essentielles

### Comment ça fonctionne
- Accessible via le **bouton CloudShell** dans la barre de navigation de la console AWS.
- Ouvre un terminal directement dans le navigateur, dans la région sélectionnée.
- Authentification automatique basée sur les credentials de la session console en cours.

### Avantages
- Pas de configuration locale du CLI requise.
- Idéal pour les **tâches rapides et simples** via CLI sans quitter la console.
- Environnement préconfiguré avec les outils les plus courants déjà disponibles.

---

## Points à retenir

- CloudShell hérite des **credentials de l'identité active** dans la console (IAM user ou rôle assumé).
- La commande `aws sts get-caller-identity` permet de vérifier sous quelle identité on est authentifié.
- Recommandé comme **alternative rapide** à la configuration d'un CLI local pour des opérations ponctuelles.

# 2- Demo: Using AWS CloudShell

## Sujet du cours

Démonstration pratique d'**AWS CloudShell** : vérification de l'authentification, exécution de commandes de lecture et d'écriture via CLI directement dans le navigateur.

---

## Méthodes / Raisonnements

### 1. Ouvrir CloudShell
- Cliquer sur le **bouton CloudShell** dans la barre de navigation de la console AWS.
- Une session terminal s'ouvre dans le navigateur, authentifiée avec les credentials de l'utilisateur connecté.

### 2. Vérifier l'identité active
```bash
aws sts get-caller-identity
```
Confirme que CloudShell utilise bien les credentials de l'identité connectée (ici : `cloud_user`).

### 3. Tester les actions de lecture
```bash
# Lister les utilisateurs IAM
aws iam list-users

# Décrire les instances EC2
aws ec2 describe-instances
```
Les ressources créées préalablement (3 utilisateurs IAM, 2 instances EC2) sont bien visibles — les permissions de lecture fonctionnent.

### 4. Tester les actions d'écriture
- Exécution d'un script shell créant 3 nouveaux utilisateurs IAM via le CLI.
- Les utilisateurs apparaissent immédiatement dans la console IAM → les permissions d'écriture fonctionnent également.

---
### 5. Créer et exécuter des scripts Bash dans CloudShell

#### Script de création d'utilisateurs IAM (`02-demo-create-iam-users-script.sh`)

```bash
#!/bin/bash
 
# Function to generate a random username
generate_random_username() {
    echo "user-$(openssl rand -hex 3)"
}
 
# Loop to create 3 users
for i in {1..3}; do
    # Generate a random username
    USERNAME=$(generate_random_username)
 
    # Create the IAM user
    aws iam create-user --user-name "$USERNAME"
    echo "Created IAM user: $USERNAME"
 
    # Attach the AmazonS3FullAccess managed policy
    aws iam attach-user-policy --user-name "$USERNAME" --policy-arn "arn:aws:iam::aws:policy/AmazonS3FullAccess"
    echo "Attached AmazonS3FullAccess policy to user: $USERNAME"
done
 
echo "All users created and policies attached."
```

**Ce script :**
1. Génère un nom d'utilisateur aléatoire via `openssl rand -hex 3` (ex. `user-a3f9c1`).
2. Crée l'utilisateur IAM avec `aws iam create-user`.
3. Attache la policy managée `AmazonS3FullAccess` à chaque utilisateur.
4. Répète l'opération 3 fois.

#### Script de démo générique (`demo.sh`)

**Créer le script :**
```bash
nano demo.sh
```

**Contenu du script :**
```bash
#!/bin/bash
 
echo "Hello depuis CloudShell"
aws sts get-caller-identity
```

**Sauvegarder dans nano :**
- `CTRL + O` → Entrée (enregistrer)
- `CTRL + X` (quitter)

**Rendre le script exécutable :**
```bash
chmod +x demo.sh
```

**Exécuter le script :**
```bash
./demo.sh
# ou
bash demo.sh
```

## Points à retenir

- CloudShell **hérite des permissions** de l'identité connectée : lecture ET écriture selon les policies en place.
- Tout ce qui est réalisable dans la console peut être fait dans CloudShell via CLI — **même périmètre de permissions**.
- Un **script shell** peut être exécuté directement dans CloudShell pour automatiser des actions répétitives.
- CloudShell est un outil puissant pour **accélérer les interactions CLI** sans configuration locale.
- Les ressources du module (scripts) sont disponibles dans les assets pour suivre la démonstration.

# 3- Module Summary and Exam Tips — AWS CloudShell

## Sujet du cours

Récapitulatif du module AWS CloudShell et conseils clés pour l'examen.

---

## Points à retenir

- **CloudShell** = shell navigateur intégré à la console AWS.
- **Pré-authentifié** automatiquement avec les credentials de la session active (IAM user ou rôle assumé).
- **AWS CLI pré-installée** et prête à l'emploi — aucune configuration requise.
- Nombreux outils et logiciels courants disponibles dès l'ouverture.

---

## Conseil examen

> Si un scénario demande une solution **rapide, pré-installée et pré-authentifiée** pour interagir avec AWS via CLI → réponse = **AWS CloudShell**.

Workflow typique : se connecter à la console → ouvrir CloudShell → exécuter des commandes CLI → vérifier les résultats dans la console. Tout cela sans quitter le navigateur.

