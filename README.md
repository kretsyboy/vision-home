# SiteVue.AR Home: a visionOS-style menu for Meta Ray-Ban Display

This Meta Ray-Ban Display Web App recreates the Apple Vision Pro Home View on the 600×600 full-color display in the right lens. You control it with the Meta Neural Band. It is a single `index.html` file (about 69 KB) with no build step, plus two PNG icons and a seamlessly looping wallpaper video (`wallpaper.mp4`, 600×600, 18 s, 4.1 MB, with `wallpaper.jpg` shown while it loads).

## What carries over from Vision Pro, and how

| Vision Pro | On the lens |
|---|---|
| Home View with round, layered app icons | Round icons in SiteVue brand colors (navy, electric indigo, violet-blue and periwinkle) with white icon art, arranged in a circle: **Notes** in the center, with Clock, Weather, Compass, Calculator, Tips and Settings around it. Each icon has a gradient backplate, a specular highlight and a separate glyph layer. |
| Look at something and it highlights | A **thumb swipe** moves the highlight. The icon lifts 12%, its glyph layer moves further than its backplate (parallax), and a colored halo appears. On a laptop, hovering the mouse acts as gaze. |
| Pinch to tap | **Index pinch** (Enter) |
| Tab bar on the left | Apps and People. The label expands out of the bar when a tab is highlighted. |
| Chevron at the top opens Control Center | Swipe up to the chevron and pinch. Control Center has Brightness, Do Not Disturb, Reduce Motion, Recenter, Settings and Tips. |
| Windows on glass, with a close button and window bar below | Each app opens in a glass window that springs out of its icon. Below the window are **×** and the window bar. Pinch the bar, then swipe or pinch-and-drag to move the window, and pinch again to drop it. |
| People tab | The people you add, with their local time |
| Startup | When the app opens, the 13 pieces of the SiteVue AI logo (each letter plus the mark's shapes) float and tumble in 3D over the wallpaper as thick, extruded blocks (12 stacked layers, about 2× size), then snap together into the logo, flattening as they lock in. A light sweeps slowly across it (1.5 s) while the logo grows about 8%, stopping when the light reaches the end. As the light moves onto each next letter, the letter behind it turns solid white, so the whole logo ends up white. The finished white logo stays on screen for 3 s before Home appears. Then Home pops in. It takes about 7.3 s, and a pinch or swipe skips it at any point. Pinch or swipe to skip. **Reduce Motion** shows the logo with a simple fade instead. The letter shapes come from the SiteVue logo artwork (`cms/static/sitevue-logo.svg`). |
| Bluetooth Devices | **Settings → Bluetooth Devices** shows live status for the Meta Ray-Ban Display (whether this app is running on them) and the Meta Neural Band (whether swipe and pinch input is arriving, and how recently). **Pair ›** shows the steps for each device. Display Web Apps get no Bluetooth access, so pairing itself happens in the Meta AI app on your phone: the glasses pair with the phone, and the band pairs with the glasses. The band's input reaches this app automatically once paired. |
| Transparency | **Settings → Transparency** (also in Control Center) fades the whole app, wallpaper included, so you see more of the real world through the lens. 0% is normal and it goes up to 85%, so the app never disappears completely and you can always turn it back down. |
| Wallpaper | A slow plasma video in the SiteVue palette (navy-black, electric indigo, periwinkle and white, sampled from the SiteVue AI artwork) loops behind Home at 60% speed, so it drifts slowly. Its last 2 s crossfade into its opening frames, so the loop has no visible restart. It fades back when a window or Control Center is open. Set its strength in **Settings → Wallpaper** (default 70%, 0% turns it off). **Reduce Motion** freezes it. |

**Why the glass looks different:** the display adds light to what you see. Black pixels are see-through, so a frosted backdrop blur would blur nothing. Instead, "glass" is a dim lit fill with a bright top edge. For the same reason, the wallpaper's lit areas tint your view indigo and use more battery than black, so lower it in Settings if the world looks too tinted. Its dark navy areas stay nearly see-through.

## Apps

Clock, with World / Timer / Stopwatch tabs like visionOS's Clock (the timer and stopwatch keep running in the status pill, and the timer announces "Timer done" aloud) · Weather (location from your phone + Open-Meteo, °F/°C) · Compass (the glasses' own motion sensors, so it points where your head points) · Notes (pinch the text box to dictate or type, then **Read** to hear it aloud) · Calculator · Tips · Settings (Bluetooth Devices, Transparency, accent color, including White, text size, brightness, wallpaper strength, reduce motion, Do Not Disturb, reset).

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

1. **Host it over HTTPS.** Meta accepts only `https://` URLs. It's live on GitHub Pages at https://kretsyboy.github.io/vision-home/ (repo `kretsyboy/vision-home`). Pushing to `main` republishes it in about a minute.
2. **Turn on Developer Mode.** In the Meta AI app, go to Settings → App Info, tap the version number 5 times, then tap Enable.
3. **Add the app.** In the Meta AI app, go to Apps → Web Apps → Connect Web App, paste the URL and save. "SiteVue.AR Home" then appears in the glasses' app list.
4. Weather and Compass ask for location and motion permission the first time you use them. To change a permission later, open the system menu → Permissions.

## Platform limits it respects

- The page is a fixed 600×600 with no page scrolling. Long lists scroll inside the window as the highlight moves.
- At most 3 history entries are used (Home → app → sub-screen). The host caps history at 5.
- Text is at least 16 px. Primary content is 20–28 px, and buttons are at least 58 px tall.
- Camera, microphone and notifications aren't available to Display Web Apps yet, so no app relies on them.
- Spoken alerts use `speechSynthesis`, which Meta supports with one voice. Do Not Disturb mutes them.
