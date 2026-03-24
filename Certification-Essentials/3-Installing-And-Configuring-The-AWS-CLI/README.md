# 1- Demo: Installing the AWS CLI

## Sujet du cours

Démonstration pratique de l'**installation de l'AWS CLI (version 2)** sur macOS, avec un aperçu des autres systèmes d'exploitation supportés et des conseils pour configurer son environnement de travail.

---

## Concepts clés

- **AWS CLI v2** : outil en ligne de commande officiel pour interagir avec les services AWS.
- **Systèmes supportés** : Linux, macOS, Windows.
- **Documentation officielle** : source de référence pour l'installation (lien fourni dans les assets du module). https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

---

## Méthodes / Raisonnements

### Étapes d'installation sur macOS (ligne de commande)

1. **Copier et exécuter la commande de téléchargement** depuis la documentation officielle AWS.
2. *(Si erreur SSL de vérification de certificat)* : ajouter le flag de désactivation de vérification — non recommandé en production, utilisé ici uniquement pour la démonstration.
3. **Exécuter la commande d'installation** avec `sudo`.
4. **Vérifier l'installation** :
    - Taper `aws` → affiche le prompt CLI.
    - Taper `aws --version` → confirme l'installation de la version 2.
    - Taper `which aws` → indique le chemin d'installation.

### Recommandation importante
> Même sur macOS ou Windows, il est **fortement conseillé d'apprendre Linux** pour les installations CLI. Linux est le système dominant dans le cloud, et sa maîtrise est un atout majeur en environnement réel et pour l'examen.

---

## Points à retenir

- Toujours utiliser **AWS CLI version 2** pour suivre les démonstrations du cours.
- La procédure varie légèrement selon l'OS, mais la logique reste la même.
- Il est possible d'utiliser le CLI via un **environnement playground** (abordé dans la démonstration suivante), sans installation locale.
- Le lien vers la documentation officielle est fourni dans les **assets du module**.

# 2- Demo: Using the Hands-on Playground and AWS CLI

## Sujet du cours

Démonstration pratique de l'utilisation du **Hands-on Playground Pluralsight** combiné à l'**AWS CLI** : création d'un compte sandbox AWS, configuration des credentials CLI, et vérification de l'authentification.

---

## Concepts clés

- **Hands-on Playground** : environnement sandbox AWS fourni par Pluralsight (nécessite un abonnement).
- **Access Key ID / Secret Access Key** : paire de credentials utilisée pour s'authentifier dans AWS via le CLI.
- **`aws configure`** : commande pour configurer les credentials et les paramètres par défaut du CLI.
- **Profils CLI** : mécanisme permettant de gérer plusieurs ensembles de credentials dans le même environnement.

---

## Méthodes / Raisonnements

### 1. Lancer un sandbox Pluralsight
1. Aller dans **Hands-on > Cloud Sandboxes > AWS**.
2. Choisir **Default Sandbox** et cliquer sur *Start Sandbox*.
3. Ouvrir la sandbox en **fenêtre incognito** (le compte AWS s'ouvre avec l'ID pré-rempli).
4. Se connecter avec l'identifiant `cloud_user` et le mot de passe fourni.

### 2. Configurer le CLI avec `aws configure`
```bash
aws configure
```
Renseigner dans l'ordre :
- **AWS Access Key ID** : copier depuis le sandbox.
- **AWS Secret Access Key** : copier depuis le sandbox.
- **Default region** : `us-east-1` *(recommandé pour le playground, moins de restrictions)*.
- **Default output format** : `json`.

### 3. Vérifier l'authentification
```bash
aws sts get-caller-identity --no-verify-ssl
```
Retourne l'identité de l'utilisateur connecté (UserID, Account, ARN) — permet de confirmer que le CLI est bien authentifié.

### 4. Gérer plusieurs profils
```bash
aws configure --profile <nom_du_profil>
```
- Permet de stocker plusieurs ensembles de credentials sous des noms distincts.
- Les profils sont stockés dans `~/.aws/credentials` et `~/.aws/config`.
- Pour utiliser un profil spécifique dans une commande : ajouter `--profile <nom_du_profil>`.

---

## Points à retenir

- Le Hands-on Playground nécessite un **abonnement Pluralsight actif**.
- Toujours utiliser la région **`us-east-1`** dans la sandbox (les autres peuvent être restreintes).
- `aws configure` configure le **profil par défaut** ; utiliser `--profile` pour des profils supplémentaires.
- `aws sts get-caller-identity` est la commande de référence pour **vérifier l'authentification CLI**.
- Les credentials sont visibles et modifiables directement dans **`~/.aws/credentials`**.