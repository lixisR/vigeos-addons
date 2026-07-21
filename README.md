# Vigeos Add-ons

Dépôt d'add-ons [Home Assistant](https://www.home-assistant.io/) de **Vigeos** —
télésurveillance bienveillante pour les seniors : <https://vigeos.fr>

## Ajouter ce dépôt à Home Assistant

1. **Paramètres → Modules complémentaires → Boutique des modules complémentaires**
2. Menu **⋮** (en haut à droite) → **Dépôts**
3. Coller cette URL, puis **Ajouter** :

   ```
   https://github.com/lixisR/vigeos-addons
   ```

4. Fermer, rafraîchir la page : les add-ons Vigeos apparaissent dans la boutique.

[![Ajouter ce dépôt à votre instance Home Assistant.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2FlixisR%2Fvigeos-addons)

## Add-ons

| Add-on | Description |
|---|---|
| [**Vigeos Agent**](vigeos_agent) | Configuration automatique de la box Vigeos : activation par QR code depuis l'application, détection de chute sur la box, alertes à la famille, chiffrement de bout en bout des vidéos. |

## À propos de ce dépôt

Ce dépôt ne contient **que les métadonnées** nécessaires à Home Assistant
(manifestes et documentation). Les add-ons sont distribués sous forme d'images
déjà construites, publiées sur GitHub Container Registry : Home Assistant les
télécharge, rien n'est compilé sur votre box.

**Les sources des add-ons Vigeos sont propriétaires** et ne sont pas publiées.
Ce dépôt n'est pas un projet open source : voir [LICENSE](LICENSE).

## Support

- Site : <https://vigeos.fr>
- Contact : <equipe@vigeos.fr>
