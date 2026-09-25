# Crow Button Card

Crow Button Card is an entity button for Home Assistant with a **liquid-glass** look and feel. Tap the icon to switch the entity, and tap anywhere else for its details and history. While the entity is on, the button lights up in your chosen colour with a gently flashing glow.

> ✨ **AI features are optional and off by default.** To unlock them, turn on **Enable AI features** in the editor's AI Features section. They need a Google Gemini conversation agent. With AI off, everything else in the card works as normal.

## Key Features

- **Three Layouts**: Live Activity, Tile and Square
- **Smart Switching**: each kind of entity is switched the right way, from locks and covers to scenes and scripts
- **Custom Actions**: `tap_action` and `hold_action` with `perform_action` in YAML
- **Flash While On**: a pulsing glow with an adjustable speed
- **Spin While On**: the icon can spin for as long as the entity is on
- **Read State from Another Entity**: for example, a script button that shows the vacuum's state
- **Custom "On" States**: choose which states light the button up
- **Your Own Icon**: any Home Assistant icon, the entity's own icon, or no icon at all
- **Details Sheet**: a history graph or on/off timeline from 1 to 24 hours, with a tap-or-drag readout
- **Glass Style**: Auto, Light or Dark theme with a Clear-to-Frosted slider
- **Compact or Regular Size**: Compact matches standard widget sizing
- **Colour Presets**: Ruby, Amber, Mint, Ocean, Berry and Graphite, plus optional off, text and icon colours

## AI Features

These are all optional, and each one can be switched off individually. Long-press the button to open them:

- **Insight**: what the current state means, with a practical tip
- **Ask AI**: plain-English questions about the entity
- **What happened?**: the latest activity as a timeline, with a short summary
- **This week**: seven days of history as a few key numbers, with a short summary

To set up Google Gemini, enable the **Generative Language API** in Google Cloud Console and add the **Google Generative AI** integration with your API key. Then select **Google AI Conversation** as the card's Conversation agent. Full step-by-step setup is in the README.

## Installation

1. Add `https://github.com/jamesmcginnis/crow-button-card` as a **Dashboard** custom repository in HACS
2. Search for **Crow Button Card** and click **Download**
3. Hard-refresh your browser, or close and reopen the HA app on your phone
4. Add the **Crow Button Card** to a dashboard

To install manually instead, copy `crow-button-card.js` from the [Releases](../../releases/latest) page into `/config/www/`. Then add `/local/crow-button-card.js` as a **JavaScript module** resource.

## Quick Start

```yaml
type: custom:crow-button-card
entity: switch.coffee_machine
layout: pill
appearance: auto
glass: 50
ai_features_enabled: true
ai_conversation_agent: conversation.google_generative_ai
```

> **Note:** Everything above can be set from the visual editor. AI features are **off by default**. The example above enables them; leave `ai_features_enabled` out (or set it to `false`) for a card with no AI.
