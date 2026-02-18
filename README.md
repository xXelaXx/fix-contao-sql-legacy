# fix-contao-sql-legacy

# Étude de Cas : Maintenance Critique & Résolution de Conflit SQL (CMS Legacy)

## 📝 Contexte du Projet
Le site vitrine d'un producteur local (Les Jardins d'Herbauges), basé sur une version obsolète du CMS **Contao**, s'est retrouvé totalement hors-ligne suite à une mise à jour d'infrastructure chez l'hébergeur (OVH).

**Statut initial :** Erreur fatale (`Fatal Error`) bloquant l'accès à l'intégralité du site et de l'administration.

## 🛠️ Problèmes Identifiés
Après analyse des logs et activation du mode débugging, deux causes principales ont été isolées :

1. **Évolution de l'environnement SQL** : Le serveur MySQL a été mis à jour vers une version où le terme `groups` est devenu un **mot réservé**. Le code source du CMS n'étant pas protégé, les requêtes SQL échouaient systématiquement.
2. **Dette Technique** : Environnement tournant sous PHP 5.5 (obsolète), rendant le site vulnérable et instable face aux évolutions de l'hébergeur.

## 🚀 Actions Réalisées

### 1. Diagnostic & Investigation
- Accès au serveur via FTP pour analyse de la structure.
- Modification du fichier `localconfig.php` pour forcer l'affichage des erreurs système (`displayErrors = true`).
- Identification précise des fichiers sources générant les exceptions SQL.

### 2. Hotfix & Patching de Code
- **Échappement des colonnes SQL** : Intervention manuelle sur les librairies et modules natifs (News, Search).
- Ajout de "backticks" (\` \`) autour de la colonne `groups` pour permettre au serveur SQL d'interpréter le terme comme un nom de colonne et non comme une commande.
- *Exemple de correction :*
  - **Avant** : `SELECT groups FROM tl_news_archive...`
  - **Après** : `SELECT `groups` FROM tl_news_archive...`

### 3. Stabilisation & Livraison
- Désactivation du mode débug pour la mise en production.
- Test de l'intégrité des données et de l'affichage (indexation de recherche, menus, galeries).
- Rédaction d'un compte-rendu technique pour le client expliquant l'origine de la panne.

## 📈 Résultats
- **Temps de résolution** : Moins d'une heure.
- **Impact** : Site 100% fonctionnel sans perte de données.
- **Opportunité** : Validation d'un projet de refonte complète sous une technologie moderne suite à la démonstration de l'obsolescence du système actuel.

## 🧠 Compétences Démontrées
- **Debug d'urgence** (Environnement de production)
- **PHP / SQL** (Écriture de requêtes et correction de syntaxe)
- **Gestion de la dette technique** (Legacy code)
- **Relation client** (Vulgarisation technique et conseil stratégique)
