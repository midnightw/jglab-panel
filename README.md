# JG LAB Panel

Firmware + interface web de flash pour le **Waveshare ESP32-S3-Touch-LCD-7** (800×480, tactile capacitif), utilisé en **portrait 480×800**.

## Matériel ciblé

- Waveshare ESP32-S3-Touch-LCD-7
- ESP32-S3 N16R8 : 16 MB Flash / 8 MB PSRAM
- LCD RGB 800×480 (modèle ESPHome natif `ESP32-S3-TOUCH-LCD-7-800X480`)
- tactile GT911
- expander CH422G

> Ce projet ne vise pas le modèle **7B 1024×600**.

## V0.2

- identité graphique JG LAB en portrait
- heure + date via SNTP (`Europe/Zurich`)
- Wi-Fi configurable au premier flash via Improv Serial / portail captif
- température + humidité avec SHT40/SHT41/SHT45 (optionnel)
- CO₂ avec SCD40/SCD41 (optionnel)
- qualité d’air dérivée du CO₂
- statut Wi-Fi réel
- bloc H2S prêt à être relié plus tard à la Bambu Lab H2S
- OTA ESPHome
- installateur ESP Web Tools via GitHub Pages

Sans capteur SHT4x/SCD4x, le panneau démarre quand même et affiche `--` pour les valeurs absentes.

## Flash web

Le workflow GitHub Actions compile automatiquement le firmware et prépare un site ESP Web Tools.

1. Ouvre la page GitHub Pages du dépôt dans **Chrome ou Edge sur ordinateur**.
2. Branche le port USB-C **UART** de la carte.
3. Clique sur **Installer JG LAB Panel**.
4. Sélectionne le port série et lance l’installation.
5. Configure ensuite le Wi-Fi via l’assistant USB ou le point d’accès `JG LAB Panel Setup`.

Si le port n’apparaît pas : maintiens **BOOT**, appuie brièvement sur **RESET**, puis relâche BOOT.

## Capteurs optionnels

Les capteurs partagent l’I²C de la carte (`SDA GPIO8`, `SCL GPIO9`) :

- SHT4x : `0x44`
- SCD40/SCD41 : `0x62`

## Fichiers

- `jglab-panel.yaml` : logique et interface LVGL
- `board_waveshare_7.yaml` : configuration matérielle
- `assets/jglab_background.png` : interface graphique 480×800
- `installer/index.html` : interface de flash web
- `.github/workflows/build-and-pages.yml` : compilation + publication
