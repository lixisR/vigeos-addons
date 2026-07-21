# Vigeos Agent

Add-on Home Assistant de la box Vigeos. Il transforme une box Home Assistant OS
en box Vigeos : vous branchez la box, vous scannez le QR code du kit dans
l'application Vigeos, et l'agent applique tout seul la configuration
(alertes, détection de chute, chiffrement des vidéos).

> Cet add-on est destiné aux **kits Vigeos**. Il n'a aucune utilité sans un kit
> et un compte Vigeos.

## Installation

1. Dans Home Assistant : **Paramètres → Modules complémentaires → Boutique des
   modules complémentaires**.
2. Menu **⋮** (en haut à droite) → **Dépôts**.
3. Coller l'URL suivante puis **Ajouter** :

   ```
   https://github.com/lixisR/vigeos-addons
   ```

4. Fermer la fenêtre, rafraîchir la page, puis ouvrir **Vigeos Agent** dans la
   liste et cliquer sur **Installer**.
5. Activer **Démarrage au lancement** et **Watchdog**, puis **Démarrer**.

L'add-on est distribué sous forme d'image déjà construite : l'installation se
résume à un téléchargement, il n'y a pas de compilation sur la box.

## Activation du kit

Rien à saisir à la main dans le cas courant : l'agent démarre sans identité et
attend. Le journal affiche alors :

```
Kit non activé — en attente du scan du QR code dans l'app…
```

Ouvrez l'application Vigeos, scannez le QR code collé sur la box, et suivez
l'assistant d'installation. L'agent reçoit son identité et se configure seul.

Si votre kit vous a été livré avec un code et un secret à saisir, renseignez-les
dans l'onglet **Configuration** de l'add-on (`kit_code` et `kit_secret`), puis
redémarrez l'add-on.

## Options

| Option | Défaut | Rôle |
|---|---|---|
| `kit_code` | *(vide)* | Code du kit (`VK-XXXXXX`). Laissé vide, il est renseigné à l'activation depuis l'application. |
| `kit_secret` | *(vide)* | Secret associé au kit. Idem : normalement rempli automatiquement. |
| `api_base` | `https://api.vigeos.fr` | Service Vigeos contacté par la box. À ne pas modifier. |
| `fall_detection` | `true` | Interrupteur maître de la détection de chute. `false` : l'agent continue de tourner, seule la détection est arrêtée. |
| `mqtt_host` | `core-mosquitto` | Broker MQTT utilisé si aucun service MQTT n'est déclaré à Home Assistant. |
| `frigate_slug` | `ccab4aaf_frigate` | Identifiant de l'add-on Frigate installé sur la box. À changer seulement si vous avez installé Frigate depuis un autre dépôt. |

## Ce que fait l'agent une fois le kit activé

- Écrit la configuration Home Assistant nécessaire aux alertes
  (une sauvegarde du fichier modifié est créée avant toute écriture) et
  recharge Home Assistant.
- Envoie un signe de vie régulier au service Vigeos : si la box est débranchée
  ou perd Internet, la famille est prévenue.
- Relaie chaque chute détectée en alerte vers l'application de la famille.
- Fait tourner la **détection de chute** sur la box elle-même : les images sont
  analysées en local, elles ne quittent jamais le domicile.
- **Configure et surveille les caméras du kit** : elles sont déclarées par
  l'application au moment de l'installation, l'agent les découvre ensuite sur
  votre réseau, change leurs mots de passe d'usine et vérifie en continu
  qu'elles répondent.
- **Chiffre les vidéos de bout en bout** avant envoi : seules les personnes de
  votre foyer peuvent les déchiffrer. Le serveur Vigeos ne voit jamais les
  images en clair.

## Mises à jour

L'add-on se met à jour tout seul lorsqu'une nouvelle version est publiée : rien
à faire. Vous pouvez aussi la déclencher manuellement depuis la page de l'add-on
dans Home Assistant lorsque le bouton **Mettre à jour** apparaît.

## Vie privée

- L'analyse vidéo (détection de chute) s'exécute **sur la box**, chez vous.
- Les enregistrements envoyés à l'application sont **chiffrés de bout en bout**.
- La détection de chute peut être coupée à tout moment (`fall_detection: false`)
  sans désinstaller l'add-on.

## Dépannage

| Symptôme | Cause probable | Que faire |
|---|---|---|
| `401` dans le journal | Code ou secret du kit incorrect, ou kit supprimé côté Vigeos | Contacter le support Vigeos |
| « Ce kit est déjà activé » au scan | Le kit est rattaché à un autre compte | Contacter le support Vigeos pour le libérer |
| La caméra reste « hors ligne » dans l'app | Caméra non alimentée, ou mauvais mot de passe WiFi saisi lors de l'installation | Vérifier l'alimentation, puis relancer l'appairage de la caméra depuis l'application |
| L'add-on ne démarre pas | Voir le journal de l'add-on | Copier le journal et contacter le support |

Le journal se consulte dans **Paramètres → Modules complémentaires → Vigeos
Agent → Journal**.

## Support

- Site : <https://vigeos.fr>
- Contact : <equipe@vigeos.fr>

---

Les sources de cet add-on sont **propriétaires** (SASU Vigeos). Ce dépôt ne
contient que les métadonnées nécessaires à Home Assistant.
