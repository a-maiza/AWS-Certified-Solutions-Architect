# Amazon VPC Overview

## Sujet du cours

Introduction aux **Amazon Virtual Private Clouds (VPC)** : définition, composants clés, types de VPC, planification des plages d'adresses IP et calcul des CIDR.

---

## Concepts clés

| Composant           | Description                                                                     |
|---------------------|---------------------------------------------------------------------------------|
| **VPC**             | Réseau virtuel isolé dans AWS — votre propre data center virtuel dans le cloud. |
| **CIDR block**      | Plage d'adresses IP attribuée au VPC.                                           |
| **Subnet**          | Sous-réseau pour héberger les ressources compute.                               |
| **Route table**     | Contrôle le routage du trafic réseau.                                           |
| **Security Group**  | Pare-feu virtuel au niveau du compute.                                          |
| **NACL**            | Pare-feu virtuel au niveau du subnet.                                           |
| **Network Gateway** | Passerelle réseau (VPN, Internet Gateway, NAT Gateway).                         |

---

## Explications essentielles

### Types de VPC
- **Default VPC** : créé automatiquement par AWS à la création du compte. CIDR fixe. À utiliser uniquement pour les tests.
- **Custom VPC** : créé par l'utilisateur, CIDR personnalisé, contrôle total. **À utiliser pour toute architecture de production.**

### Caractéristiques importantes
- Un VPC est une **ressource régionale** — il ne s'étend pas sur plusieurs régions.
- **Limite** : 5 VPCs par région par compte (soft limit, extensible sur demande).
- Si plus de 5 VPCs sont nécessaires dans une région, revoir l'architecture du compte.

### Plages IP privées (RFC 1918)
Les CIDR d'un VPC doivent obligatoirement appartenir à l'une de ces plages privées :

| Plage            | Usage courant              |
|------------------|----------------------------|
| `10.0.0.0/8`     | Entreprises (très courant) |
| `172.16.0.0/12`  | Usage mixte                |
| `192.168.0.0/16` | Réseaux domestiques        |

> Ces adresses sont **non résolvables sur Internet** — elles ne sont pas publiques.

### Règles de création d'un VPC
- **IPv4 CIDR** : obligatoire, plage de `/16` à `/28`.
- **IPv6 CIDR** : optionnel, plage de `/44` à `/60`.

---

## Méthodes / Raisonnements

### Calcul du nombre d'IPs utilisables dans un CIDR

Formule : **2^(32 - préfixe)**

**Exemple avec `10.0.0.0/16` :**
- 32 bits total − 16 bits réseau = **16 bits restants**
- 2^16 = **65 536 adresses IP** disponibles

| CIDR  | Bits restants | IPs disponibles |
|-------|---------------|-----------------|
| `/16` | 16            | 65 536          |
| `/24` | 8             | 256             |
| `/28` | 4             | 16              |

> Le préfixe `/16` correspond au masque `255.255.0.0` — les 2 premiers octets sont réservés au réseau.

---

## Points à retenir

- **Ne jamais utiliser le VPC par défaut** en production — toujours créer un VPC custom.
- Les VPCs sont **régionaux** — un VPC par région, pas de portée globale.
- Les CIDR doivent appartenir aux **plages RFC 1918** (adresses privées).
- **Planifier soigneusement** les plages IP avant déploiement — difficile à modifier après coup.
- Savoir **calculer le nombre d'IPs** d'un CIDR est potentiellement testé à l'examen.
- Limite soft : **5 VPCs par région** — à ne pas dépasser sans revoir l'architecture.

# 2- Demo: Exploring the Default VPC

## Sujet du cours

Exploration du **VPC par défaut** créé automatiquement par AWS dans chaque région active : ses composants, ses paramètres par défaut et pourquoi il ne doit pas être utilisé en production.

---

## Composants du VPC par défaut

| Composant           | Configuration par défaut                                                      |
|---------------------|-------------------------------------------------------------------------------|
| **CIDR**            | `172.31.0.0/16`                                                               |
| **Route table**     | Route locale + route vers Internet Gateway                                    |
| **NACL**            | Tout le trafic entrant et sortant autorisé                                    |
| **DHCP option set** | Nom de domaine interne, serveurs DNS, NTP, NetBIOS configurés automatiquement |
| **Subnets**         | Plages `/20` créées automatiquement (4 091 IPs disponibles par subnet)        |

---

## Explications essentielles

### Accès Internet automatique
- Le VPC par défaut est connecté à un **Internet Gateway** via sa route table.
- Tout compute déployé dans ce VPC reçoit automatiquement une **adresse IP publique**.
- Il est donc **publiquement accessible sur Internet** sans configuration supplémentaire.

### NACL par défaut
- Autorise **tout le trafic entrant et sortant** sans restriction.
- Appliqué à **tous les subnets** du VPC par défaut.

### Subnets par défaut
- Plages `/20` → **4 091 IPs disponibles** (et non 4 096 — les 5 adresses réservées par AWS seront expliquées dans un module ultérieur).

---

## Points à retenir

- Chaque région active dispose d'**un VPC par défaut** créé automatiquement.
- Le VPC par défaut est **ouvert sur Internet par défaut** → risque de sécurité majeur.
- **Ne jamais utiliser le VPC par défaut en production** — réservé aux tests rapides uniquement.
- Pour toute architecture sérieuse, créer un **VPC custom** avec des paramètres de sécurité contrôlés.

# 3- Demo: Creating a Custom VPC

## Sujet du cours

Démonstration de la **création d'un VPC custom** dans la console AWS : paramètres essentiels, ressources créées automatiquement et bonnes pratiques de référencement.

---

## Méthodes / Raisonnements

### Créer un VPC custom (console)
1. VPC dashboard → *Create VPC*.
2. Sélectionner **VPC only** (et non "VPC and more") — bonne pratique pour comprendre chaque composant individuellement.
3. Donner un **nom** au VPC.
4. Saisir manuellement un **IPv4 CIDR** valide (ex. `10.0.0.0/24`).
5. **IPv6** : optionnel — Amazon-provided ou BYOIP. Laisser désactivé si non nécessaire.
6. **Tenancy** :
    - `Default` : ressources partagées avec d'autres clients AWS sur le même matériel (recommandé).
    - `Dedicated` : matériel dédié à un seul client — pour exigences de conformité strictes, mais plus coûteux.
7. Cliquer sur *Create VPC*.

### Ressources créées automatiquement
| Ressource              | Description                                  |
|------------------------|----------------------------------------------|
| **DHCP option set**    | Spécifique au VPC custom créé.               |
| **Route table (main)** | Table de routage principale par défaut.      |
| **NACL (main)**        | Liste de contrôle d'accès réseau par défaut. |

---

## Points à retenir

- Toujours créer les composants VPC **séparément** (subnets, route tables, gateways) pour bien comprendre leur fonctionnement et leurs interactions.
- Référencer les VPCs par leur **VPC ID** (et non leur nom) dans tout script ou infrastructure as code.
- La **tenancy dédiée** a un coût supplémentaire — à utiliser uniquement pour des besoins de conformité spécifiques.
- Un VPC custom ne dispose **pas d'accès Internet par défaut** — contrairement au VPC par défaut.
- Les subnets, gateways et autres ressources seront ajoutés dans les modules suivants.

# 4- Module Summary and Exam Tips — Amazon VPC

## Sujet du cours

Récapitulatif des concepts essentiels sur les VPCs Amazon et conseils clés pour l'examen.

---

## Points à retenir

### VPC — Fondamentaux
- Réseau **logiquement isolé** dans le cloud AWS — configuration entièrement contrôlée par l'utilisateur.
- **IPv4 CIDR** : obligatoire, plage de `/16` à `/28`.
- **IPv6 CIDR** : optionnel.
- Les VPCs sont des **ressources régionales** — un VPC ne s'étend pas sur plusieurs régions.
- **Limite** : 5 VPCs par région (soft limit) — si cette limite est atteinte, revoir l'architecture.

### Plages IP privées valides (RFC 1918)
| Plage            | Note                     |
|------------------|--------------------------|
| `10.0.0.0/8`     | Usage entreprise courant |
| `172.16.0.0/12`  | Usage mixte              |
| `192.168.0.0/16` | Réseaux domestiques      |

> Ces adresses sont **privées et non résolvables sur Internet**.

### Calcul CIDR — À maîtriser pour l'examen
**Formule : 2^(32 - préfixe)**

| CIDR  | IPs disponibles |
|-------|-----------------|
| `/16` | 65 536          |
| `/24` | 256             |
| `/28` | 16              |

### Ressources créées automatiquement dans un VPC custom

| Ressource                  | Comportement par défaut                                             |
|----------------------------|---------------------------------------------------------------------|
| **DHCP option set**        | Configure domaine, DNS, NTP — personnalisable.                      |
| **Route table principale** | Contient une route locale pour le trafic interne au VPC uniquement. |
| **NACL principale**        | Autorise tout le trafic entrant et sortant par défaut.              |

---

## Conseils examen

- Savoir **lire et calculer** une notation CIDR est directement testé.
- Les plages RFC 1918 sont **non publiques** — à retenir si un scénario parle de résolution internet.
- Un VPC custom crée automatiquement **3 ressources** : DHCP option set, route table, NACL.
- Si un scénario mentionne plus de 5 VPCs dans une région → signal d'une mauvaise architecture.