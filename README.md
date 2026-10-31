# SiteVue.AR Home: a visionOS-style menu for Meta Ray-Ban Display

This Meta Ray-Ban Display Web App recreates the Apple Vision Pro Home View on the 600×600 full-color display in the right lens. You control it with the Meta Neural Band. It is a single `index.html` file (about 65 KB) with no build step, plus two PNG icons.

## What carries over from Vision Pro, and how

| Vision Pro | On the lens |
|---|---|
| Home View with round, layered app icons in a honeycomb | The same 3-4-3 honeycomb of circular icons. Each icon has a gradient backplate, a specular highlight and a separate glyph layer. |
| Look at something and it highlights | A **thumb swipe** moves the highlight. The icon lifts 12%, its glyph layer moves further than its backplate (parallax), and a colored halo appears. On a laptop, hovering the mouse acts as gaze. |
| Pinch to tap | **Index pinch** (Enter) |
| Tab bar on the left: Apps / People / Environments | Same. The label expands out of the bar when a tab is highlighted. |
| Chevron at the top opens Control Center | Swipe up to the chevron and pinch. Control Center has Brightness, Immersion, Do Not Disturb, Reduce Motion, Recenter, Environments, Settings and Tips. |
| Windows on glass, with a close button and window bar below | Each app opens in a glass window that springs out of its icon. Below the window are **×** and the window bar. Pinch the bar, then swipe or pinch-and-drag to move the window, and pinch again to drop it. |
| Environments plus the Digital Crown for immersion | Choose None, The Moon, Haleakalā, Yosemite, Mount Hood, Joshua Tree or Jupiter. Set the strength with the **Immersion** slider. |
| People tab | The people you add, with their local time |

**Why the glass looks different:** the display adds light to what you see. Black pixels are see-through, so a frosted backdrop blur would blur nothing. Instead, "glass" is a dim lit fill with a bright top edge. Environments are drawn as faint light (stars, horizons, rain, snow, Jupiter's bands) over the real world, much like visionOS's mixed immersion.

## Apps

Clock (world clocks) · Weather (location from your phone + Open-Meteo, °F/°C) · Timer (it keeps running in the status pill and announces "Timer done" aloud) · Stopwatch with laps · Mindfulness (breathing flower: 4 s in, 6 s out) · Compass (the glasses' own motion sensors, so it points where your head points) · Notes (pinch the text box to dictate or type, then **Read** to hear it aloud) · Calculator · Tips · Settings (accent color, text size, brightness, reduce motion, Do Not Disturb, reset).

Settings, people, notes, the timer and the stopwatch are saved in the glasses' local storage.

## Controls

| Neural Band | Key the glasses send | Does |
|---|---|---|
| Thumb swipe up/down/left/right | Arrow keys | Moves the highlight. On a slider or a ◀ ▶ control, left/right changes the value. In move mode it moves the window. |
| Index pinch | Enter | Selects |
| Middle pinch (Back) | `history.back()` | Closes the window or panel and returns to Home |
| Pinch and drag | Pointer events | Fine control on sliders and while moving a window. A drag elsewhere moves the highlight. |

Meta documents only that the band arrives as arrow keys, Enter and Back. Which finger gesture maps to which key is from Meta's product documentation, so check it on your glasses.

On a laptop, use the arrow keys, Enter and Esc. Mouse hover acts as gaze, and clicking selects.

## Put it on your glasses

1. **Host it over HTTPS.** Meta accepts only `https://` URLs. Any static host works, for example:
   ```bash
   npx netlify-cli deploy --dir vision-home --prod
   ```
2. **Turn on Developer Mode.** In the Meta AI app, go to Settings → App Info, tap the version number 5 times, then tap Enable.
3. **Add the app.** In the Meta AI app, go to Apps → Web Apps → Connect Web App, paste the URL and save. "SiteVue.AR Home" then appears in the glasses' app list.
4. Weather and Compass ask for location and motion permission the first time you use them. To change a permission later, open the system menu → Permissions.

## Platform limits it respects

- The page is a fixed 600×600 with no page scrolling. Long lists scroll inside the window as the highlight moves.
- At most 3 history entries are used (Home → app → sub-screen). The host caps history at 5.
- Text is at least 16 px. Primary content is 20–28 px, and buttons are at least 58 px tall.
- Camera, microphone and notifications aren't available to Display Web Apps yet, so no app relies on them.
- Spoken alerts use `speechSynthesis`, which Meta supports with one voice. Do Not Disturb mutes them.
