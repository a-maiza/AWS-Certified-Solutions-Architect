# AWS Regions, Availability Zones, and Edge Locations

## Sujet du cours

Introduction à l'infrastructure mondiale d'AWS : compréhension des régions, des zones de disponibilité (AZ) et des emplacements périphériques (edge locations), dans le cadre de la préparation à la certification **AWS Certified Solutions Architect Associate**.

---

## Concepts clés

| Concept                        | Définition                                                                                                                                   |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| **Région AWS**                 | Zone géographique distincte hébergeant des data centers AWS. Offre tolérance aux pannes et stabilité maximales.                              |
| **Zone de disponibilité (AZ)** | Emplacement isolé et indépendant au sein d'une région, avec alimentation redondante, réseau propre et connectivité à faible latence.         |
| **Edge Location**              | Data center (ou point de présence) permettant de délivrer des services avec une latence très faible, au plus proche des utilisateurs finaux. |
| **AZ ID**                      | Identifiant physique permanent d'une AZ, indépendant du nom logique affiché dans un compte AWS.                                              |

---

## Explications essentielles

### Régions AWS
- Chaque région est une zone géographique **complètement séparée**.
- Elles permettent de déployer des charges de travail **à travers le monde**.
- AWS ajoute continuellement de nouvelles régions.
- Il existe aussi des **régions GovCloud**, réservées aux workloads gouvernementaux stricts (peu probable à l'examen).

### Zones de disponibilité (AZ)
- Chaque région contient **au minimum 3 AZ**, chacune composée de plusieurs data centers.
- Les AZ sont **physiquement séparées** pour limiter l'impact des catastrophes naturelles (ouragans, inondations, etc.).
- Si une AZ tombe en panne, les autres restent opérationnelles.
- Le terme **multi-AZ** désigne un déploiement sur deux AZ ou plus.

### Edge Locations
- Permettent de déployer des contenus **encore plus près des utilisateurs** que les régions.
- Utilisées principalement pour la **mise en cache** via des points de présence (*points of presence*) et des caches périphériques régionaux.

---

## Méthodes / Raisonnements

### Nommage des AZ vs AZ ID
- Le **nom logique** d'une AZ (ex. : `us-west-2b`) est propre à chaque compte AWS et peut pointer vers des data centers différents d'un compte à l'autre.
- L'**AZ ID** (ex. : `usw2-az1`) est un identifiant **physique fixe**, identique quel que soit le compte.
- L'AZ ID est essentiel pour les architectures **multi-comptes** afin de garantir que les workloads s'exécutent sur les mêmes infrastructures physiques.

---

## Exemples importants

- **US West 2** est actuellement composée de **4 AZ** (`us-west-2a`, `us-west-2b`, `us-west-2c`, `us-west-2d`).
- Dans un compte, `us-west-2b` peut correspondre à l'AZ ID `usw2-az1`, mais dans un autre compte, `us-west-2b` peut correspondre à `usw2-az3`. Le nom logique ne garantit pas les mêmes data centers.

---

## Points à retenir

- Une **région** = zone géographique distincte avec plusieurs data centers.
- Une **AZ** = emplacement isolé dans une région, conçu pour résister aux catastrophes locales.
- AWS recommande **au moins 3 AZ par région** pour assurer la haute disponibilité.
- Les **edge locations** servent à rapprocher les services des utilisateurs finaux (caching).
- Pour les architectures **multi-comptes**, toujours utiliser l'**AZ ID** (et non le nom logique) pour identifier les mêmes data centers physiques.
- Les régions **GovCloud** existent pour les workloads gouvernementaux mais sont rarement testées à l'examen.