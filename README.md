# Crow Button Card

Crow Button Card is an entity button for Home Assistant with a **liquid-glass** look and feel. Tap the icon to switch the entity, and tap anywhere else on the card for its details and history. While the entity is on, the button lights up in your chosen colour with a gently flashing glow. You can choose from three layouts: a slim **Live Activity** row, a compact **Tile** or a **Square**.

> 🎨 **Built to stay readable.** The "on" colour is adjusted automatically so the button stays legible in both light and dark themes.

> ✨ **AI features are optional and off by default.** To unlock them, turn on **Enable AI features** in the AI Features section of the card editor. They need a Google Gemini conversation agent (see [AI Features Setup](#-ai-features-setup-optional) below). With AI off, everything else in the card works as normal.

**Add the repository to HACS:**

[![Open your Home Assistant instance and add this repository to HACS.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=jamesmcginnis&repository=crow-button-card&category=plugin)

---

## 🛠️ Installation

### Via HACS (Recommended)

1. Click the **Add to HACS** button above. Alternatively, in Home Assistant open **HACS** → **⋮ menu** (top right) → **Custom repositories**
2. Add `https://github.com/jamesmcginnis/crow-button-card` as a **Dashboard** repository, then close
3. Search for **Crow Button Card** and click **Download**
4. Hard-refresh your browser (Cmd+Shift+R on Mac), or close and reopen the Home Assistant app on your phone
5. Edit a dashboard, click **+ Add Card** and search for **Crow Button Card**

> 💡 HACS adds the dashboard resource for you, so there's nothing else to set up.

### Manual

1. Download `crow-button-card.js` from [Releases](../../releases/latest)
2. Copy it into `/config/www/` on your Home Assistant instance
3. Go to **Settings → Dashboards → ⋮ menu → Resources → + Add Resource**
4. Enter `/local/crow-button-card.js`, choose **JavaScript module** and click **Create**
5. Hard-refresh your browser and add the **Crow Button Card** to a dashboard

---

## 🤖 AI Features Setup (Optional)

AI features are **off by default**, and the card works fully without them. To unlock them (Insight, Ask AI, What happened? and This week), turn on **Enable AI features** in the card editor's **AI Features** section, then set up Google Gemini as your conversation agent:

### Step 1 — Enable the Generative Language API

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and sign in
2. Create a new project (or select an existing one)
3. Go to **APIs & Services → Library**
4. Search for **Generative Language API** and click **Enable**

> ⚠️ This step is essential. An API key without the Generative Language API enabled will return errors immediately.

### Step 2 — Create an API Key

1. In Google Cloud Console go to **APIs & Services → Credentials**
2. Click **+ Create Credentials → API key** and copy the key

### Step 3 — Add Google Generative AI to Home Assistant

1. In Home Assistant go to **Settings → Devices & Services → + Add Integration**
2. Search for **Google Generative AI** and select it
3. Paste your API key and click Submit
4. Click the **gear icon ⚙️** next to **Google AI Conversation**
5. Uncheck **Recommended model settings**, select a current **Flash** model and save

### Step 4 — Configure the Card

1. In the card's visual editor, open the **AI Features** section and turn on **Enable AI features**
2. Select **Google AI Conversation** from the **Conversation agent** dropdown
3. Optionally, switch off any individual AI tool you don't want

AI stays off until an agent is chosen. Nothing is sent to Gemini until you open one of the AI sheets, and nothing runs in the background.

### Free Tier

Gemini's free tier is generous for a single button card. Answers are cached, so opening the same sheet again shortly afterwards doesn't use extra requests. Insight and Ask AI answers are kept for 10 minutes and What happened? summaries for 30 minutes. If you see a rate-limit error, your daily quota has run out and will reset the next day.

---

## ✨ Features

### Layouts

- 💊 **Live Activity**: one slim row with the icon, name and state, with an adjustable height
- 🟧 **Tile**: a compact tile with the icon and name
- ⬛ **Square**: the icon on top with the name below

### Button

- 👆 **Tap the icon to switch**: each kind of entity is switched the right way. Locks lock and unlock, covers open and close, vacuums start and stop, and scenes, scripts and buttons run.
- ⚙️ **Custom actions**: set a `tap_action` or `hold_action` with `perform_action` in YAML to call any action instead
- ✨ **Flash while on**: the glow pulses while the entity is on, with an adjustable flash speed. Turned off, it just stays lit.
- 🌀 **Spin while on**: optionally, the icon spins for as long as the entity is on
- 🔀 **Read state from another entity**: for example, a script that starts the vacuum can show the vacuum's state
- ✅ **Custom "on" states**: choose which states count as on, such as `cleaning, returning, paused`
- 🖼️ **Your own icon**: pick any Home Assistant (Material Design Icons) icon, or use the entity's own state-aware icon. With the icon hidden, the whole button switches the entity.
- 🔤 **Text options**: show or hide the state, align left, centre or right, and set a font size from 10 to 28px
- ✋ **Long-press**: opens the AI actions sheet when AI features are on, or runs your `hold_action`

### Details Sheet

Tap anywhere on the card except the icon to open it:

- 📈 **History graph**: a line graph for numeric states, or an on/off timeline, with **1h, 3h, 6h, 12h or 24h** ranges
- 👉 **Tap-or-drag readout**: a glass pill shows the value or state and time anywhere along the graph
- 📊 **On-time summary**: how long it was on and what percentage of the period that was
- 🕒 **Current state and last changed**
- 🔘 **Action button** that matches the entity: Turn on / off, Lock / Unlock, Start / Stop, Open / close or Run

### Appearance

- **Theme**: Auto (follows your Home Assistant theme), Light or Dark
- **Glass slider**: from Clear to Frosted. It looks best over a wallpaper or coloured view.
- **Size**: Compact, which matches standard widget sizing, or Regular, which is about 20% larger
- **Animations**: Subtle, Full (the icon also glows while on), Off (which also stops the flash), or System (Subtle, but stays still when your device's Reduce Motion setting is on)
- **Colour presets**: Ruby, Amber, Mint, Ocean, Berry and Graphite
- **Optional colours**: an Off tint for the button while it's off, plus Text and Icon colours that are used exactly as picked

### AI Features

These are all optional, and each one can be switched off individually in the editor. Long-press the button to open them:

- **Insight**: what the current state means, with a practical tip
- **Ask AI**: type a question about the entity, or tap a suggested one
- **What happened?**: the latest activity as a timeline, with a short summary
- **This week**: seven days of history as a few key numbers, with a short summary

> 🔒 **The AI only works with facts from Home Assistant.** Each request includes the entity's actual state and history, and the AI is told not to add anything that isn't in that data.

---

## 📋 Quick Start

```yaml
type: custom:crow-button-card
entity: switch.coffee_machine
layout: pill
appearance: auto
glass: 50
size: compact
animation: subtle
show_icon: true
show_state: true
flash_enabled: true
flash_speed: 600
active_color: '#FF3B30'
ai_features_enabled: true
ai_conversation_agent: conversation.google_generative_ai
ai_enable_insight: true
ai_enable_ask: true
ai_enable_recap: true
ai_enable_week: true
```

> **Note:** Everything above can be set from the visual editor. AI features are **off by default**. The example above enables them; leave `ai_features_enabled` out (or set it to `false`) for a card with no AI. Your Gemini agent's entity ID may differ, so pick it from the editor's dropdown.

### Showing another entity's state

```yaml
type: custom:crow-button-card
entity: script.start_vacuum
state_entity: vacuum.roborock
active_state:
  - cleaning
  - returning
  - paused
spin_icon: true
```

### Custom actions

```yaml
type: custom:crow-button-card
entity: light.porch
tap_action:
  action: perform-action
  perform_action: light.turn_on
  data:
    brightness_pct: 100
hold_action:
  action: perform-action
  perform_action: light.turn_off
```

### Configuration Options

| Option | Default | Description |
|--------|---------|-------------|
| `entity` | *(required)* | What the button controls |
| `state_entity` | — | Read the state from a different entity |
| `active_state` | *(usual on states)* | List of states that count as "on" |
| `layout` | `pill` | `pill` (Live Activity), `tile` or `square` |
| `name` | *(entity name)* | Custom name for the button |
| `show_icon` | `true` | Show the icon. Turned off, the whole button switches the entity |
| `icon` | *(entity icon)* | Any `mdi:` icon |
| `use_dynamic_icon` | `false` | Use the entity's own state-aware icon, even if an icon is set |
| `spin_icon` | `false` | Spin the icon while the entity is on |
| `show_state` | `true` | Show the state under the name |
| `text_align` | `left` | `left`, `center` or `right` |
| `font_size` | `14px` | Size of the name, from `10px` to `28px` |
| `card_height` | `56px` | Height of the Live Activity layout, from `40px` to `110px` |
| `tap_action` | `toggle` | `toggle`, `none`, or `perform-action` with `perform_action`, `data` and `target` |
| `hold_action` | — | Action for a long-press when AI features are off |
| `flash_enabled` | `true` | Pulse the glow while the entity is on |
| `flash_speed` | `600` | Flash speed in milliseconds, from `150` to `1500` (lower is faster) |
| `graph_hours` | `3` | History range opened first: `1`, `3`, `6`, `12` or `24` |
| `appearance` | `auto` | `auto`, `light` or `dark` |
| `glass` | `50` | Glass transparency, `0` (clear) to `100` (frosted) |
| `size` | `compact` | `compact` or `regular` |
| `animation` | `subtle` | `subtle`, `full`, `off` or `system` |
| `active_color` | `#FF3B30` | The button colour while it is on |
| `inactive_color` | — | Optional tint while the button is off |
| `name_color` | *(automatic)* | Optional text colour |
| `icon_color` | *(automatic)* | Optional icon colour |
| `ai_features_enabled` | `false` | Master switch for all AI features |
| `ai_conversation_agent` | — | Your Google Gemini conversation agent |
| `ai_enable_insight` | `true` | Insight |
| `ai_enable_ask` | `true` | Ask AI |
| `ai_enable_recap` | `true` | What happened? |
| `ai_enable_week` | `true` | This week |

---

## 🔧 Troubleshooting

**The card doesn't appear in the card picker**
- Hard-refresh your browser, or close and reopen the Home Assistant app on your phone.
- For manual installs, check `/local/crow-button-card.js` is listed under **Settings → Dashboards → Resources** as a **JavaScript module**.

**Tapping the card doesn't switch the entity**
- Tap the **icon** to switch. Tapping anywhere else opens the details sheet. If you'd rather tap the whole button, turn off **Show icon**.
- Check **When the icon is tapped** isn't set to **Nothing**.

**The button doesn't light up when the entity is on**
- Some entities use states other than `on`. Add them under **Counts as "on" when the state is**, for example `cleaning, returning`.
- If the state lives on a different entity, set **Read its state from another entity**.

**The glow doesn't flash**
- Check **Flash while on** is turned on, and that **Animations** isn't set to **Off**. With **System**, the flash also stops when your device's Reduce Motion setting is on.

**The glass looks solid**
- Glass needs something behind it to show through. Use a dashboard wallpaper or a coloured view, and move the **Glass** slider towards Clear.

**AI features are missing, or long-press does nothing**
- Check **Enable AI features** is turned on in the editor's **AI Features** section. AI is off by default.
- Confirm **Google AI Conversation** is selected as the **Conversation agent**. AI stays off until one is chosen.
- Ensure the **Generative Language API** is enabled in Google Cloud Console. This is the most common setup mistake.

---

## 🙏 Credits & Acknowledgements

- The [Home Assistant](https://www.home-assistant.io) team
- The HA community for inspiration and feedback
- All users who test, report issues and suggest improvements
- My Loving Wife for her endless support ❤️

---

## 📄 License

MIT License: free to use, modify and distribute.

---

## ⭐ Support

If this is useful to you, please **star the repository** and share it with the community!

For bugs or feature requests, use the [GitHub Issues](../../issues) page.
