# Pastel Button Card

Card Lovelace personalizzabile con griglia di bottoni pastello per Home
Assistant, coerente con le altre card Pastel della stessa dashboard.

## Funzionalità

- **Griglia automatica 2 colonne**: 1 bottone → pieno; 2 → fianco a fianco;
  3 → 2 sopra + 1 grande sotto; 4 → 2×2; 5 → 2+2+1 grande; e così via.
- **Ogni bottone è completamente indipendente**: colore pastello, icona,
  etichetta e azione tutti configurabili per singolo bottone.
- **Palette 9 colori**: amber, blue, green, pink, purple, red, teal, orange,
  gray — stessa palette delle altre card Pastel.
- **Tutte le azioni HA supportate**: toggle, turn_on, turn_off, script,
  scene, call_service (con dati JSON), more_info, navigate, URL.
- **Drag & drop nell'editor** per riordinare i bottoni trascinandoli.
- Feedback visivo al tap (leggero scale down).
- Titolo card opzionale.

## Installazione

### Tramite HACS
1. HACS → Frontend → menu (⋮) → **Repository personalizzati**
2. Aggiungi l'URL del repository GitHub, categoria "Lovelace"
3. Cerca "Pastel Button Card" e installala

### Manuale
1. Copia `pastel-button-card.js` in `config/www/`
2. **Impostazioni → Dashboard → Risorse** → aggiungi:
   - URL: `/local/pastel-button-card.js`
   - Tipo: **JavaScript Module**

## Configurazione (YAML)

```yaml
type: custom:pastel-button-card
title: Dove siamo       # opzionale
buttons:
  - label: Cancello
    icon: mdi:gate
    color: green
    action:
      type: toggle
      entity_id: cover.cancello

  - label: Luci salotto
    icon: mdi:lightbulb
    color: amber
    action:
      type: turn_on
      entity_id: light.salotto

  - label: Scena film
    icon: mdi:movie
    color: purple
    action:
      type: scene
      entity_id: scene.film

  - label: Attiva Allarme
    icon: mdi:alarm-light
    color: red
    action:
      type: script
      entity_id: script.attiva_allarme

  - label: Vai alla dashboard
    icon: mdi:home
    color: blue
    action:
      type: navigate
      navigation_path: /lovelace/0

  - label: Servizio custom
    icon: mdi:cog
    color: gray
    action:
      type: call_service
      service: notify.mobile_app_iphone
      data:
        message: "Ciao!"
```

## Tipi di azione disponibili

| Tipo | Descrizione | Parametri |
|---|---|---|
| `toggle` | Alterna on/off | `entity_id` |
| `turn_on` | Accende | `entity_id` |
| `turn_off` | Spegne | `entity_id` |
| `script` | Lancia script | `entity_id` (es. `script.nome`) |
| `scene` | Attiva scena | `entity_id` (es. `scene.nome`) |
| `call_service` | Servizio generico | `service`, `data` (JSON opzionale) |
| `more_info` | Apre popup dettagli | `entity_id` |
| `navigate` | Naviga a pagina | `navigation_path` |
| `url` | Apre URL | `url_path`, `new_tab` (default true) |

## Note tecniche

- Carica `lit-element` da CDN (stesso approccio delle altre card Pastel).
- Il drag & drop usa l'API nativa HTML5 `draggable` — funziona su desktop
  e tablet; su mobile potrebbe essere meno fluido (il touch drag non è
  supportato nativamente da tutti i browser senza librerie aggiuntive: in
  quel caso usa semplicemente rimuovi/aggiungi per riordinare).
