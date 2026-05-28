# CenterStage Ad — Generalized Ad Specification

## 1. Format Overview

The **CenterStage Ad** is a premium high-impact rich-media format that presents a brand message in a full-screen or near full-screen centered experience. It is designed for moments where the publisher allows a short, controlled interruption or high-visibility branded canvas, such as page entry, section transition, game/app break, article-to-article transition, or another publisher-defined natural break.

This format is best understood as a **custom takeover / interstitial-style rich-media display unit**, not a standard fixed IAB display unit. It should be implemented using IAB-compatible HTML5, display/video measurement, ad-serving, SafeFrame, OM SDK/OMID, and verification practices where applicable.

**Core purpose:**  
Deliver a visually dominant, center-focused brand experience while preserving user control through visible close/skip controls, time limits, and frequency caps.

**Best use cases:**

- Major campaign launches
- Entertainment trailers and premieres
- Retail sale announcements
- Auto launches and product reveals
- Travel destination inspiration
- BFSI product education
- High-value lead generation
- App install or product onboarding campaigns

**Brand value:**

- Maximum canvas and share of attention
- Strong storytelling potential
- Supports video, animation, product cards, forms, quizzes, or CTA-led journeys
- High memorability when frequency and close controls are handled responsibly

**Publisher value:**

- Premium high-impact monetization opportunity
- Works well for sponsorships, roadblocks, homepage takeovers, and guaranteed deals
- Can be packaged as a curated direct, PMP, or PG unit
- Requires publisher approval because the format affects the page experience

**User experience value:**

- Clear, focused message
- Easy close/skip path
- No content trapping
- Should appear at natural breaks rather than unexpectedly during task completion
- Should return the user to the original content state after close, skip, timeout, or completion

**Classification:**

| Classification | Applicability | Notes |
|---|---:|---|
| Display | Yes | Usually served through display/rich-media ad infrastructure. |
| Rich media | Yes | Uses HTML5, animation, video, interaction, tracking, and state logic. |
| Expandable | Sometimes | May expand from a banner/teaser into center-stage mode. |
| Interstitial-style | Yes | Full-screen or near full-screen, but must remain dismissible. |
| Page-level takeover | Sometimes | If it overlays the full page and dims/obscures content. |
| Sticky | No by default | It should not remain persistently attached during scrolling unless specifically approved. |
| Video-led | Optional | Video may be used, but is not required. |
| Gamified | Optional | Can include interaction, but the core format is not inherently gamified. |
| Standard IAB unit | No | Treat as a custom high-impact rich-media format using IAB-compatible practices. |

### CenterStage takeover vs standard interstitial

A **standard interstitial** often appears as a mandatory transitional ad between content screens or pages. A **CenterStage Ad** is a premium creative pattern that may behave like an interstitial but is usually more flexible: it can open from a teaser, appear at a natural break, run as a near full-screen overlay, contain rich media, and be trafficked as a custom direct or programmatic guaranteed format.

The important distinction is UX control. A CenterStage Ad must not behave like an abusive forced interstitial. It needs clear close/skip behavior, responsible timing, frequency caps, and publisher-defined entry points.

---

## 2. Standard Ad Dimensions & States

Because CenterStage is a high-impact responsive format, the declared serving size and the actual active canvas may differ. The declared size is usually used for ad-server eligibility, reservation, reporting, and trafficking. The active size is controlled by the creative overlay or expansion container.

| State / Variant | Recommended Collapsed Size | Recommended Expanded Size | Device | Common Placement | Notes |
|---|---:|---:|---|---|---|
| Teaser banner to CenterStage | 300×250 | 90–100% viewport width × 80–100% viewport height | Desktop / Mobile Web | In-content, sidebar, MPU slot | Good when publisher requires user-initiated opening. Collapsed creative must disclose expand action. |
| Mobile banner to takeover | 320×50 | Fullscreen mobile, respecting safe areas | Mobile Web / App | Top/bottom mobile display slot | Use only if expansion is approved. Close button must remain inside visible safe area. |
| Mobile full canvas | 320×480 | Fullscreen mobile or 9:16 responsive | Mobile Web / App | Interstitial or app natural break | Suitable for vertical video, app-style cards, and product storytelling. |
| Desktop MPU to overlay | 300×250 | Center modal 800×600 to 1200×800, or responsive 80vw × 80vh | Desktop | Standard display inventory | Safer than full browser takeover. Background dim may be used if allowed. |
| Half-page teaser | 300×600 | Center modal 900×700 to 1200×900, or responsive 80vw × 90vh | Desktop / Tablet | Sidebar / premium display | Strong for product reveal or video-led creative. |
| Leaderboard teaser | 728×90 | Center modal 900×600 to 1200×800 | Desktop / Tablet | Above/below article | May open on click or publisher-defined trigger. |
| Billboard takeover | 970×250 | Near full-screen desktop or 970×500+ centered canvas | Desktop | Homepage / section front | Premium sponsorship unit; often direct-sold. |
| Large desktop takeover | 970×500 | Fullscreen desktop, or centered 1200×675 / 1200×800 | Desktop | Homepage / premium content break | Good for cinematic video and brand storytelling. Must handle viewport resize. |
| Fullscreen mobile | N/A or 1×1 / fluid / 320×480 | 100vw × 100dvh, safe-area aware | Mobile Web / App | Interstitial / natural app break | Use dynamic viewport units and safe-area padding. Avoid hidden close button under browser chrome. |
| Fullscreen desktop | N/A or 1×1 / fluid / 970×250 | 100vw × 100vh or centered 80–90vw × 80–90vh | Desktop | Page-level takeover | Requires direct publisher approval and careful QA. |
| Responsive / fluid variant | Fluid / multi-size | CSS clamp-based responsive canvas | Desktop / Mobile / App | Custom rich-media placement | Recommended for a reusable ad-builder/editor. Declare eligible sizes in GAM and manage active dimensions in creative config. |

### Safe-area considerations

| Environment | Safe-area rule |
|---|---|
| Mobile web | Use `env(safe-area-inset-top/right/bottom/left)` where supported. Avoid placing close/CTA controls at the browser chrome edge. |
| iOS Safari / Chrome mobile | Use `100dvh` or a viewport-height fallback strategy. Do not assume `100vh` equals visible space. |
| Android Chrome | Test after address bar collapse/expand. Recalculate layout on resize and orientation change. |
| In-app webview | Respect SDK safe areas and host app chrome. Some webviews restrict overlay size or pointer events. |
| Desktop | Keep close control visible above all creative layers. Avoid placing critical text or CTA outside the centered content area on smaller screens. |
| Notched devices | Keep close, CTA, skip, and legal text outside notches and home indicator areas. |

---

## 3. User Experience & Behaviour Specification

### Initial state

The format can start in one of three modes:

1. **Direct open at natural break:** The CenterStage canvas opens when the publisher defines a valid break.
2. **Delayed page-load open:** The unit opens after a short delay, subject to policy, frequency cap, and publisher approval.
3. **User-initiated expansion:** A teaser banner, card, or CTA opens the CenterStage canvas on click/tap.

The creative should never surprise users with sound or trap users from continuing to content.

### Trigger condition

Allowed trigger patterns:

| Trigger | Recommendation | Notes |
|---|---|---|
| User click/tap | Preferred | Lowest intrusion risk and easiest to justify for rich media. |
| Publisher-defined natural break | Acceptable | Common for app and content transitions. |
| Time delay after load | Use cautiously | Requires frequency cap and visible close from start. |
| Scroll threshold | Optional | Should not cover content unexpectedly mid-scroll unless approved. |
| Auto-open on every page view | Not recommended | High fatigue and policy risk. |
| Forced countdown before close | Avoid | Close/skip expectations must be clear and user-controlled. |

### Animation / transition

- Fade, scale, slide, or center zoom transitions may be used.
- Recommended open transition: **200–450 ms**.
- Recommended close transition: **150–300 ms**.
- Avoid aggressive flashing, shaking, rapid zooms, or motion that causes disorientation.
- If using video, begin muted and preferably with a poster frame until playback is allowed.
- Respect `prefers-reduced-motion`.

### Interaction model

| Interaction | Expected behavior |
|---|---|
| Close button | Always visible or available from the start unless local publisher policy requires a short skip delay; if a delay is used, show countdown clearly. |
| Skip button | Optional for video-led executions; recommended when video duration exceeds 6 seconds. |
| CTA click | Opens click-through in approved target context and records click/CTA event. |
| Video play/pause | User should be able to pause video or stop motion where relevant. |
| Audio | Muted by default. Sound only after explicit user action. |
| Background click | Do not count background/dim-layer clicks as ad clicks unless clearly labelled. Prefer using it only to close if publisher approves. |
| Escape key | Desktop should support Escape to close. |
| Tab navigation | Focus should remain inside the overlay while open and return to previous page element after close. |

### Expanded / active state

The active state displays a full-screen or near full-screen container with:

- Center-focused content area
- Close button
- Optional skip/countdown state
- Optional CTA
- Optional video, animation, carousel, product cards, lead form, or interactive content
- Legal/disclaimer region where needed
- Tracking state machine for open, view, interaction, close, skip, timeout, and click

### Close / collapse behaviour

A CenterStage Ad must provide a reliable path back to content.

Close methods:

- Close icon/tap target
- Skip button
- Escape key on desktop
- Timeout close after configured max display seconds
- Natural completion close for short animation/video, only if publisher approved
- Back button handling in-app where supported

After close:

- Restore scroll position or app state.
- Remove focus trap.
- Stop/pause video and animation.
- Do not re-open during the same page view unless explicitly user-initiated.
- Do not create layout shift in the underlying page.

### Re-entry behaviour

| Scenario | Recommended behavior |
|---|---|
| User closes auto-open unit | Do not reopen in same page view. Respect session frequency cap. |
| User clicks teaser again | May reopen if user-initiated. |
| Timeout close occurs | Do not immediately reopen. |
| User navigates to new page | Apply campaign/publisher frequency cap before opening again. |
| App resumes from background | Do not auto-reopen unless it was already active and not closed. |

### Mobile behaviour

- Use mobile-first layout.
- Support portrait and landscape if approved.
- Close/skip must be easy to tap with a minimum target of roughly 44×44 CSS px.
- Avoid hidden close button beneath browser address bars, notches, or OS controls.
- Use `playsinline` for HTML5 video.
- Do not trigger sound until tap.
- Handle soft keyboard if forms are used.
- Prevent scroll bleed behind overlay only while active, then restore page scrolling.
- Use safe-area padding.

### Desktop behaviour

- Center the creative with max-width and max-height constraints.
- Support Escape key close.
- Preserve focus management.
- Avoid using excessive full-screen coverage when a modal-sized CenterStage canvas is sufficient.
- Recalculate on viewport resize.
- Ensure close button is above all z-index layers.

### App behaviour

- Confirm support for the host SDK, webview, MRAID where applicable, and OM SDK/OMID measurement.
- In-app display may require MRAID-style expand/close behavior depending on SDK.
- Test safe areas, device orientation, app background/resume, and back button.
- Do not assume all app environments allow full-screen overlay from display inventory.

### Accessibility expectations

- Close and skip controls must have accessible labels.
- Keyboard users must be able to close the unit.
- Motion should respect reduced-motion preferences.
- Focus should move into the active ad when opened and return to the prior element when closed.
- Avoid inaccessible image-only CTAs.
- All critical text should be present as HTML text or accessible labels, not only baked into images.

### Behaviour classification checklist

| Property | Recommended Setting |
|---|---|
| User-initiated | Preferred, but not mandatory if publisher-approved natural break is used |
| Scroll-triggered | Optional, not core behavior |
| Auto-started but muted | Allowed for video/animation only if muted and policy-compliant |
| Time-bound | Strongly recommended |
| Dismissible | Required |
| Frequency-capped | Required for auto-open or natural-break use |
| Non-blocking | Must not trap user; overlay may temporarily cover content only with close |
| Sticky / persistent | No by default |
| Full-screen / takeover | Yes, subject to publisher approval |

---

## 4. Creative Design Guidelines

### Layout hierarchy

Recommended hierarchy:

1. Brand/logo
2. Main message or visual hero
3. Supporting proof/product/offer detail
4. CTA
5. Legal/disclaimer
6. Close/skip controls

Keep the content center-focused. The user should understand the offer within 1–2 seconds.

### CTA placement

- Place CTA in a stable, predictable region, usually lower center or lower right inside the content area.
- Keep CTA away from the close button.
- Avoid placing CTA directly under the user’s likely close/skip path.
- For mobile, keep CTA above the home indicator and away from browser UI.
- Multiple CTAs are allowed only when the hierarchy remains clear.

### Logo placement

- Top-left or top-center inside the content frame is usually safest.
- Do not place logo behind close/skip controls.
- For video-led creative, logo can be persistent as a small overlay.

### Safe zones

| Element | Minimum safe-zone guidance |
|---|---|
| Close button | At least 8–16 px from viewport/content edge plus safe-area inset |
| Main headline | Keep within central 70–80% width on desktop and 85–90% width on mobile |
| CTA | Avoid bottom 24–48 px on mobile unless safe-area-aware |
| Legal text | Keep readable; do not place below visible viewport edge |
| Video controls | Must not overlap CTA or close button |

### Readability

- Avoid long paragraphs.
- Use high contrast.
- Keep mobile headline short.
- Use responsive type via `clamp()`.
- Avoid tiny legal text; use expandable legal copy if necessary.

### Motion intensity

- Motion should enhance the reveal, not punish the user.
- Avoid rapid flashing, repeated shake, or parallax overload.
- Provide reduced-motion alternative.
- Keep looping background animation subtle.

### Animation timing

| Animation | Recommended timing |
|---|---:|
| Overlay open | 200–450 ms |
| Content reveal | 300–800 ms |
| CTA pulse | Use sparingly; 1.5–3 sec cycle if needed |
| Video intro | 3–6 sec for non-skippable feel; longer video should be skippable |
| Auto-close | Usually 8–15 sec if used; must be publisher-approved |

### Touch targets

- Minimum target: approximately 44×44 CSS px for close, skip, CTA, and key interactions.
- Space close and CTA apart to avoid accidental clicks.
- Do not make the whole background clickable unless clearly disclosed.

### Close button placement

- Top-right is standard.
- Top-left may be acceptable in some app environments but should be consistent.
- Use a visible icon and/or “Close”.
- Ensure it is always above video, canvas, animation, and dim layers.
- It should be accessible from the start or after a clearly disclosed skip countdown if policy permits.

### Visual density

- CenterStage units can be cinematic, but density must remain low.
- Avoid too many interactive hotspots in a takeover.
- Use progressive disclosure for complex details.

### Responsive scaling

- Use one layout system with breakpoints:
  - Small mobile: 320–390 px width
  - Large mobile: 391–480 px width
  - Tablet: 768–1024 px width
  - Desktop: 1024+ px width
- Keep media aspect ratio stable.
- Use `object-fit: cover` carefully; do not crop legal copy, logo, product pack, or CTA.

### Brand safety

- Creative should not mimic OS alerts, browser dialogs, publisher navigation, or system warnings.
- Do not use deceptive close controls.
- Do not obscure publisher consent/privacy controls.
- Avoid false scarcity or misleading interaction cues.

### Do / Don’t

| Do | Don’t |
|---|---|
| Provide close/skip controls clearly. | Hide close controls or delay them without disclosure. |
| Use frequency caps for auto-open. | Show the takeover repeatedly on every page view. |
| Keep video muted until user action. | Start audio automatically. |
| Restore content state after close. | Trap scroll, focus, or navigation. |
| Use responsive safe areas. | Place controls under browser chrome or device notches. |
| QA on low-end mobile devices. | Assume desktop performance reflects mobile performance. |
| Use a backup image. | Serve a blank overlay if JS/video fails. |
| Get publisher approval. | Run as a normal banner without approval. |

---

## 5. Asset Specifications

### A. Image Assets

**Supported formats:**

- JPG/JPEG for photographic backgrounds
- PNG for transparent logos, UI elements, packshots
- WebP where supported
- AVIF where publisher/browser support is confirmed
- SVG for simple vector icons/logos where allowed by ad platform and security policy

**Recommended compression:**

| Asset Type | Recommendation |
|---|---|
| Hero image | Compressed JPG/WebP, target visually lossless |
| Logo | SVG or optimized PNG |
| Product cutout | Optimized transparent PNG/WebP |
| Background | Avoid enormous desktop-only images on mobile |
| Backup image | Match declared slot or responsive fallback size |

**Retina / high-density considerations:**

- Supply 2× assets for small UI/logo elements.
- Avoid shipping 2× full-screen backgrounds by default on mobile; lazy-load only if needed.
- Use responsive image selection where permitted.

**Background image rules:**

- Critical text should not be baked into background if it needs accessibility or localization.
- Use `object-position` rules to preserve product/face safe zones.
- Test portrait and landscape cropping.

**Transparent overlay rules:**

- Keep alpha overlays lightweight.
- Avoid stacking many large transparent PNGs.
- Use CSS gradients or HTML overlays where possible.

**Maximum recommended file sizes:**

| Load Phase | Guidance |
|---|---:|
| Initial creative shell | 150–250 KB preferred |
| Initial visual assets | 300–500 KB preferred |
| Polite/subload assets | 1–2 MB depending on publisher approval |
| Full rich-media execution | Keep as light as possible; avoid multi-MB first load |
| Backup image | 50–150 KB for standard display; larger only for full-screen fallback if approved |

### B. Video Assets

Video is optional but common for CenterStage.

**Supported video format guidance:**

- MP4 container
- H.264 video codec
- AAC audio codec
- WebM optional only as supplementary source
- Poster frame required
- Fallback image required

**Autoplay/audio rules:**

- Autoplay video must be muted.
- Audio must require explicit user tap/click.
- Use `playsinline` for mobile.
- Do not show fake sound controls.
- Pause or stop video on close/skip.

**Duration guidance:**

| Use Case | Recommended Duration |
|---|---:|
| Animated intro / bumper | 3–6 sec |
| Product reveal | 6–10 sec |
| Trailer / entertainment | 10–15 sec before skip, longer only if user-initiated |
| Optional expanded video | 15–30 sec if user chooses to watch |

**Looping guidance:**

- Looping background video should be subtle, muted, and short.
- Do not loop loud or visually intense content.
- Stop loop after close.
- Provide reduced-motion fallback.

**Poster frame:**

- Must communicate core brand/message even if video does not play.
- Should include logo and CTA or clear visual hook.
- Should not be a black frame.

**Fallback image:**

- Required for no-JS, blocked autoplay, unsupported video, low-bandwidth mode, or SDK restrictions.
- Should include click-through and tracking fallback where possible.

**File-size guidance:**

| Video Load Phase | Guidance |
|---|---:|
| Initial load | Avoid loading full video before ad is active |
| Polite load after open | 1–3 MB preferred for short mobile video |
| Desktop high-quality polite load | 3–5 MB only if approved |
| Long-form video | Use streaming/player/VAST approach rather than bundling large video |
| Poster | 50–200 KB |

### C. HTML5 / JS / CSS Assets

**Single creative bundle expectations:**

- One HTML entry file
- Minified CSS/JS
- Configurable JSON object or GAM template variables
- Assets referenced through approved CDN URLs or bundled where allowed
- Backup image path
- Tracking endpoints/macros

**CDN-hosted assets:**

- Use HTTPS only.
- Avoid third-party libraries unless necessary.
- Use cache control correctly.
- Do not load unapproved external scripts.
- Keep vendor dependencies minimal.

**Avoiding heavy JS:**

- Avoid large frameworks for simple overlays.
- Avoid forced synchronous layout.
- Avoid long main-thread tasks.
- Use CSS transitions where possible.
- Use `requestAnimationFrame` for custom animation.

**Animation performance:**

- Prefer `transform` and `opacity`.
- Avoid animating `top`, `left`, `width`, `height`, `box-shadow`, and filters at high frequency.
- Use `will-change` sparingly and remove it after transitions.
- Avoid heavy canvas/WebGL unless the concept requires it.

**Request count discipline:**

- Keep initial request count low.
- Batch tracking where appropriate, but never lose required events.
- Defer non-critical assets.
- Avoid multiple font files.

**Fallback behaviour:**

- If JS fails, show a static backup image with a click-through.
- If video fails, show poster frame.
- If expansion is blocked, remain in collapsed teaser or static state.
- If SafeFrame restrictions prevent overlay, use a same-slot or publisher-provided expansion container.

### D. Optional Interactive Assets

CenterStage may include:

- Product tiles
- Feature cards
- Mini carousel
- Lead form
- Store locator prompt
- App install CTA
- Video chapter selector
- Quiz/poll
- Scratch/reveal mechanic
- Multiple CTAs
- Hotspots over product or scene

Recommended interaction limit: one primary interaction pattern per execution. Do not combine video, carousel, quiz, lead form, hotspots, and product tiles unless the creative is explicitly designed as a multi-step experience and QA-tested.

---

## 6. IAB / UX Compliance Considerations

This is a high-intrusion format, so the burden of UX responsibility is higher than for standard display.

### Alignment principles

- Keep initial load lightweight.
- Use polite/subload for heavy video and rich media.
- Avoid unexpected audio.
- Provide obvious close/skip controls.
- Do not block content without a clear dismissal path.
- Avoid layout shift when opening and closing.
- Respect mobile viewport, safe areas, browser chrome, and app UI.
- Do not mislead users with fake system UI or deceptive close buttons.
- Use frequency caps.
- Prefer natural breaks or user-initiated entry.
- Ensure the user returns to content immediately after dismissal.

### Format-specific compliance risks

| Risk | Why it matters | Mitigation |
|---|---|---|
| High intrusion | Full-screen ads interrupt content. | Use frequency caps, natural breaks, and clear close controls. |
| Hidden close button | Creates user frustration and policy risk. | Keep close visible, high z-index, safe-area-aware. |
| Forced countdown | Can feel coercive. | Prefer close from start; if skip delay is used, make it short and transparent. |
| Unexpected audio | Violates user expectations and browser policies. | Muted autoplay only; user-initiated sound. |
| Content trap | User cannot return to page/app. | Provide multiple close paths and restore state. |
| Layout shift | Underlying page jumps after close. | Use fixed overlay; do not inject height into content flow unless designed. |
| Excessive frequency | User sees takeover too often. | Campaign/session/day frequency caps. |
| Misleading UI | User thinks it is system or publisher UI. | Clearly brand the creative and label controls. |

---

## 7. GAM Implementation Specification

### Recommended GAM creative type

Recommended options:

1. **Custom creative template**  
   Best for reusable production trafficking, QA, and ad-builder automation.

2. **Custom HTML creative**  
   Acceptable for one-off prototypes or controlled direct campaigns.

3. **Third-party rich-media tag**  
   Acceptable if using an approved rich-media vendor, but requires publisher QA.

4. **Out-of-page creative / interstitial-like implementation**  
   May be required depending on publisher setup and Google Ad Manager configuration. Use only with explicit publisher approval.

### SafeFrame guidance

SafeFrame should be **enabled and tested carefully**, not blindly disabled.

| Scenario | Guidance |
|---|---|
| Same-slot modal only | SafeFrame may work if creative stays inside iframe. |
| Full-page overlay from iframe | SafeFrame may restrict expansion, viewport access, or overlay behavior. |
| Publisher-hosted wrapper | Often required for true page-level takeover. |
| App SDK | Requires SDK-specific support; SafeFrame is not always the relevant control layer. |

If SafeFrame blocks expansion, use a publisher-approved wrapper, rich-media vendor integration, or template with explicit expansion APIs.

### Required creative sizes

For GAM line items, declare all eligible sizes the publisher will allow. Common sizes:

- 300×250
- 320×50
- 320×480
- 300×600
- 728×90
- 970×90
- 970×250
- 970×500
- Fluid/responsive where publisher supports it
- Out-of-page / interstitial placement where publisher supports it

### Multi-size mapping

Use responsive size mapping for web placements:

| Viewport | Eligible serving sizes |
|---|---|
| Small mobile | 320×50, 320×480, fluid |
| Large mobile | 320×50, 320×480, fluid |
| Tablet | 300×250, 728×90, fluid |
| Desktop | 300×250, 300×600, 728×90, 970×90, 970×250, 970×500, fluid |

The active CenterStage canvas should be controlled by creative configuration and CSS, not by pretending a standard banner size is full-screen.

### Key-values / custom fields

Recommended targeting keys:

| Key | Example Values | Purpose |
|---|---|---|
| `format` | `centerstage` | Identifies format for reporting and template routing. |
| `trigger_type` | `user_click`, `natural_break`, `delayed_open` | Controls opening behavior. |
| `device_class` | `desktop`, `mobile_web`, `app`, `tablet` | Allows device-specific creative. |
| `experience_level` | `modal`, `near_fullscreen`, `fullscreen` | Publisher approval / packaging. |
| `video_enabled` | `true`, `false` | Routes video-capable executions. |
| `frequency_bucket` | `campaign_daily`, `session_once` | Supports capping logic. |
| `creative_variant_id` | `cs_auto_launch_v1` | Reporting and QA. |

### Click-through URL setup

- Use GAM click macros correctly in the creative/template.
- Do not hardcode final URLs without click tracking support.
- Multiple CTAs should use distinct click variables or append CTA identifiers.
- Avoid making the entire overlay clickable unless clearly intended and approved.
- Close, skip, mute, pause, and background close actions must not trigger click-through.

### Impression tracking

Track:

- GAM-served impression
- Creative loaded
- CenterStage opened
- Viewable impression / Active View eligibility
- Third-party verification if approved

### Third-party tracking pixels

- Use HTTPS.
- Fire only at intended event.
- Cachebust when required.
- Avoid firing click trackers on non-click interactions.
- Validate all trackers in preview and live QA.

### Cachebuster handling

Use cachebuster macros/placeholders where supported for:

- Impression pixels
- Interaction pixels
- Third-party tracking
- Video tracking
- Survey/lead submit pixels where applicable

### Preview and QA process

1. Preview custom template with all required variables.
2. Test in GAM creative preview.
3. Test on a publisher staging page.
4. Test with SafeFrame on/off where allowed.
5. Test in all declared sizes.
6. Test desktop, mobile web, and app SDK environments separately.
7. Validate tracking in network logs.
8. Confirm return-to-content behavior.
9. Confirm frequency-cap behavior.
10. Obtain publisher approval before live trafficking.

### GAM configurable variables

| Variable name | Type | Example | Required / Optional | Purpose |
|---|---|---|---|---|
| `click_url` | URL | `%%CLICK_URL_UNESC%%https://brand.example/landing` | Required | Primary click-through with GAM click tracking. |
| `cta_url` | URL | `https://brand.example/offer` | Required if CTA exists | Landing destination for CTA. |
| `cta_text` | String | `Explore Now` | Optional | CTA label. |
| `impression_url` | URL | `https://tracker.example/imp?[CACHEBUSTER]` | Optional | Third-party impression pixel. |
| `backup_image_url` | URL | `https://cdn.example/backup.jpg` | Required | Fallback static creative. |
| `auto_open` | Boolean | `false` | Required | Whether the unit opens automatically. |
| `trigger_type` | Enum | `user_click`, `natural_break`, `delayed_open` | Required | Determines opening behavior. |
| `trigger_delay` | Number | `3000` | Optional | Delay in ms before auto-open. |
| `max_display_seconds` | Number | `12` | Required for auto-open | Maximum active display duration. |
| `close_enabled` | Boolean | `true` | Required | Enables close control. |
| `skip_enabled` | Boolean | `true` | Optional | Enables skip state. |
| `skip_after_seconds` | Number | `0` or `5` | Optional | Seconds before skip appears or activates. Prefer 0 where possible. |
| `countdown_enabled` | Boolean | `false` | Optional | Shows countdown to skip/auto-close. |
| `countdown_text` | String | `You can close this ad in {n}` | Optional | Countdown label if used. |
| `video_url` | URL | `https://cdn.example/video.mp4` | Optional | Main video asset. |
| `video_poster_url` | URL | `https://cdn.example/poster.jpg` | Optional | Video poster. |
| `autoplay` | Boolean | `true` | Optional | Controls video autoplay. Must remain muted. |
| `muted` | Boolean | `true` | Required for autoplay video | Ensures compliant autoplay. |
| `video_loop` | Boolean | `false` | Optional | Controls video loop. |
| `background_image_url` | URL | `https://cdn.example/bg.jpg` | Optional | Main background. |
| `logo_image_url` | URL | `https://cdn.example/logo.png` | Optional | Brand logo. |
| `headline_text` | String | `The launch starts now` | Optional | Dynamic headline. |
| `body_text` | String | `Experience the new collection.` | Optional | Dynamic body copy. |
| `legal_text` | String | `T&Cs apply.` | Optional | Disclaimer. |
| `custom_tracking_pixel_1` | URL | `https://tracker.example/p1` | Optional | Additional tracker. |
| `custom_tracking_pixel_2` | URL | `https://tracker.example/p2` | Optional | Additional tracker. |
| `custom_tracking_pixel_3` | URL | `https://tracker.example/p3` | Optional | Additional tracker. |
| `custom_tracking_pixel_4` | URL | `https://tracker.example/p4` | Optional | Additional tracker. |
| `custom_tracking_pixel_5` | URL | `https://tracker.example/p5` | Optional | Additional tracker. |
| `interaction_tracking_url` | URL | `https://tracker.example/interaction` | Optional | Fires on approved engagement event. |
| `open_tracking_url` | URL | `https://tracker.example/open` | Optional | Fires when CenterStage opens. |
| `close_tracking_url` | URL | `https://tracker.example/close` | Optional | Fires on close. |
| `skip_tracking_url` | URL | `https://tracker.example/skip` | Optional | Fires on skip. |
| `timeout_tracking_url` | URL | `https://tracker.example/timeout` | Optional | Fires on auto timeout close. |
| `video_start_tracking_url` | URL | `https://tracker.example/vstart` | Optional | Fires on video start. |
| `video_complete_tracking_url` | URL | `https://tracker.example/vcomplete` | Optional | Fires on video complete. |
| `frequency_cap_key` | String | `centerstage_campaign_123` | Required for auto-open | Local/session cap coordination. |
| `creative_variant_id` | String | `cs_launch_v3_mobile` | Required | Reporting, QA, and template versioning. |

---

## 8. Tracking & Analytics Event Taxonomy

| Event name | Trigger | Required / Optional | Tracking method | Notes |
|---|---|---|---|---|
| `creative_loaded` | Creative JS/CSS/config initialized | Required | JS event + optional pixel | Confirms creative shell loaded. |
| `impression_rendered` | First render or GAM impression state | Required | GAM + optional pixel | Do not duplicate ad-server impression improperly. |
| `viewable_impression` | Meets viewability threshold through GAM/verification | Required where measurable | Active View / vendor / OMID | Use official measurement where possible. |
| `centerstage_open` | Overlay/takeover becomes active | Required | JS event + pixel | Core format event. |
| `open` | Alias or mapped event for platform | Optional | JS event | Use consistent naming in analytics. |
| `time_in_view_start` | Active unit visible | Required | Timer | Start only when overlay is visible. |
| `time_in_view` | On close/skip/timeout/completion | Required | Analytics beacon | Send duration bucket and exact ms where allowed. |
| `close` | User clicks close | Required | JS event + pixel | Must not count as click-through. |
| `skip` | User clicks skip | Required if skip exists | JS event + pixel | Distinguish from close. |
| `timeout_close` | Max display time expires | Required if auto-close exists | JS event + pixel | Useful for UX reporting. |
| `cta_click` | User clicks primary CTA | Required | GAM click macro + event | Must route through ad-server click tracking. |
| `click` | Any approved click-through | Required | GAM click macro | Avoid counting close/skip/background actions. |
| `background_close` | User taps dim layer to close | Optional | JS event | Only if this behavior is enabled. |
| `video_start` | Video playback starts | Required if video | JS video event + optional pixel | Differentiate autoplay/user-initiated if possible. |
| `video_25` | 25% video progress | Optional / recommended | JS video event | Align with video reporting. |
| `video_50` | 50% video progress | Optional / recommended | JS video event | Align with video reporting. |
| `video_75` | 75% video progress | Optional / recommended | JS video event | Align with video reporting. |
| `video_complete` | Video reaches completion | Required if video | JS video event + pixel | Use once per view. |
| `video_mute` | User mutes video | Optional | JS event | Autoplay should already begin muted. |
| `video_unmute` | User explicitly unmutes | Required if audio control exists | JS event | Important compliance/engagement signal. |
| `video_pause` | User pauses or ad closes | Optional | JS event | Separate user pause from close. |
| `video_replay` | User restarts video | Optional | JS event | Engagement signal. |
| `interaction_start` | First non-click interaction inside overlay | Optional | JS event | For carousel, quiz, form, etc. |
| `interaction_complete` | User completes designed interaction | Optional | JS event + pixel | Define per creative. |
| `lead_form_start` | User focuses first lead field | Optional | JS event | Only if form exists. |
| `lead_form_submit` | User submits lead form | Optional | Secure endpoint + event | Must follow privacy/legal rules. |
| `error` | Creative/video/tracking error | Optional / recommended | JS event | Include error code and environment. |

---

## 9. GAM Macros & Click Tracking

### Click macro usage

Use GAM click macros through the custom template or creative tag. Generic examples:

```text
click_url = %%CLICK_URL_UNESC%%https://advertiser.example/landing-page
```

or, for escaped redirect patterns:

```text
click_url = %%CLICK_URL_ESC%%https%3A%2F%2Fadvertiser.example%2Flanding-page
```

Actual macro syntax and escaping should match the publisher’s GAM implementation, creative type, and destination URL handling.

### Impression/view macro usage

- Use GAM’s native impression counting as the primary ad-server impression.
- Use third-party impression URLs only when approved.
- Fire third-party impression pixels once, not on every overlay state.
- Distinguish `impression_rendered` from `centerstage_open` if a teaser is served before the takeover opens.

### Cachebuster macro usage

Generic placeholder example:

```text
https://tracker.example/pixel?cb=%%CACHEBUSTER%%
```

If the third-party tracker expects a different cachebuster token, map it in the template.

### Third-party tracker usage

- Use HTTPS.
- Avoid piggybacking unapproved scripts.
- Use image pixels or beacon requests for simple events.
- Use cachebusting for impression and event pixels.
- Ensure trackers do not block rendering.

### Multiple CTA tracking

For multiple CTAs, use separate variables and event labels:

```text
cta_1_url = %%CLICK_URL_UNESC%%https://advertiser.example/product
cta_2_url = %%CLICK_URL_UNESC%%https://advertiser.example/store-locator
cta_3_url = %%CLICK_URL_UNESC%%https://advertiser.example/signup
```

Attach a CTA identifier to analytics events:

```json
{
  "event": "cta_click",
  "cta_id": "store_locator",
  "creative_variant_id": "cs_launch_v3"
}
```

### Deep link / landing page handling

- Mobile app deep links must include fallback web URLs.
- Test iOS and Android separately.
- Avoid opening app stores unexpectedly unless the CTA clearly says so.
- For app environments, confirm whether click opens in in-app browser, external browser, or app store.

### Avoiding invalid click inflation

Do not count the following as ad clicks:

- Close button
- Skip button
- Mute/unmute
- Pause/play unless it is intentionally a click-to-video action, not click-through
- Background dim-layer close
- Accidental swipe/touch interactions
- Countdown click
- Legal expansion click unless it opens landing page intentionally

---

## 10. VAST / Video Handling

Video is optional in CenterStage.

### When VAST is relevant

VAST is relevant if the video is served into a video player or outstream/player-based environment where VAST ad tags are expected. In that case, use the publisher/player’s supported VAST workflow and align playback/event tracking to the player.

### When VAST may not be required

If the creative contains a simple HTML5 `<video>` element inside a display/rich-media creative, VAST may not be required. However, video events should still be tracked consistently:

- `video_start`
- `video_25`
- `video_50`
- `video_75`
- `video_complete`
- `video_pause`
- `video_mute`
- `video_unmute`
- `video_replay`

### Autoplay and sound

- Muted autoplay only.
- Sound requires explicit user action.
- Use `playsinline` on mobile.
- Provide visible sound control if audio is available.
- Pause/stop video on close, skip, timeout, or overlay removal.

### Video fallback

If video fails or autoplay is blocked:

1. Show poster frame.
2. Provide a user-initiated play button if appropriate.
3. If playback remains unsupported, show backup image and CTA.
4. Still allow close/skip.

---

## 11. OpenRTB / Programmatic Compatibility

### Likely inventory classification

Exact mapping depends on the SSP, DSP, exchange, and publisher implementation. Do not invent unsupported OpenRTB fields. In most systems, CenterStage may be represented as one of the following:

| Classification | When used | Notes |
|---|---|---|
| Banner/display rich media | When delivered through display slot with HTML5 creative | Common for direct/PMP rich-media delivery. |
| Interstitial | When inventory is explicitly sold as interstitial/full-screen | Requires clear declaration and buyer approval. |
| Video | Only when the primary asset is player-served video | Use VAST when appropriate. |
| Native | Generally not recommended | Unless sold as native placement with custom rendering. |
| Rich media / expandable attribute | When platform supports declaring rich-media/expandable behavior | Field support varies by SSP/DSP. |

### Standard programmatic vs curated deals

CenterStage is usually **not ideal for open exchange delivery** unless the supply path supports high-impact creative controls and approvals. Recommended packaging:

- Direct-sold sponsorship
- Programmatic guaranteed
- Private marketplace deal
- Curated high-impact package
- Publisher-approved custom template

### Required buyer metadata

Provide buyers/adops with:

- Format name: `CenterStage Ad`
- Trigger type: user click / natural break / delayed open
- Full-screen or near full-screen behavior
- Declared ad sizes
- Active canvas dimensions
- Device support
- Video support and duration
- Audio behavior: muted by default, user-initiated sound
- Close/skip behavior
- Max display seconds
- Frequency cap
- Measurement vendors supported
- Backup creative availability
- Publisher approval status
- SafeFrame / SDK limitations

### Size declaration

Declare the serving slot size accurately. Do not misrepresent a takeover as a normal banner without metadata. If the active unit expands beyond the slot, document this in the deal, creative notes, and publisher approval workflow.

### Creative attributes

Where the platform supports creative attribute declaration, disclose:

- Rich media
- Expandable / overlay / interstitial behavior
- Auto-open if enabled
- Video if used
- Audio user-initiated only
- Full-screen or overlay behavior
- JavaScript required
- MRAID if in-app
- OMID measurement if applicable

### API / MRAID / OMID considerations

| Environment | Consideration |
|---|---|
| Mobile web | SafeFrame, GPT, viewability, browser autoplay policy |
| Mobile app | MRAID/SDK support, OM SDK/OMID measurement, safe areas |
| Desktop web | SafeFrame, iframe expansion, focus management, viewport resize |
| Video player | VAST/VPAID restrictions where applicable, OMID/video verification |

### Publisher approval requirements

Publisher approval is strongly recommended or required for:

- Auto-open takeover
- Full-screen overlay
- Delayed page-load open
- Any countdown/skip delay
- Video autoplay
- Large asset loads
- Page background dimming
- Scroll locking
- Form collection
- Use in app/webview environments

### Why direct integration may be required

CenterStage may require custom publisher integration because standard iframed display inventory may not have permission to cover the viewport, lock scrolling, read viewport dimensions, manage safe areas, or coordinate close behavior with the page/app shell.

---

## 12. Measurement, Viewability & Verification

### Active View / viewability

- Standard display impression viewability may measure the declared slot, not always the expanded overlay.
- If the takeover opens from a teaser, distinguish teaser viewability from CenterStage active view.
- For direct deals, define whether billing/reporting is based on served impression, opened takeover, viewable takeover, or completed view.

### OM SDK / OMID

- Use OM SDK/OMID-compatible measurement for mobile app and supported web video environments.
- Confirm the host SDK supports measurement vendors.
- Ensure overlay state does not break measurement access.
- For video, use OMID video measurement where supported.

### Scroll/visibility rules

Although CenterStage is not primarily scroll-triggered, visibility can be affected by viewport changes and app/browser UI. Track:

- Time overlay is visible
- Whether the creative was fully or partially obstructed
- Close before minimum attention threshold
- Video audible/inaudible state where relevant

### Core KPIs

| Metric | Definition |
|---|---|
| Open rate | Opens / rendered impressions. |
| Viewable open rate | Viewable active opens / rendered impressions. |
| Engagement rate | Meaningful interactions / opens. |
| CTR | Click-throughs / impressions or opens, depending reporting standard. |
| CTA click rate | CTA clicks / opens. |
| Close rate | User closes / opens. |
| Skip rate | Skips / opens or video starts. |
| Timeout close rate | Auto timeouts / opens. |
| Time in view | Duration from active open to close/skip/timeout. |
| Video start rate | Video starts / opens. |
| Video completion rate | Video completes / video starts. |
| Unmute rate | User unmutes / video starts. |
| Interaction depth | Number of panels/cards/actions completed. |

### Brand lift and attention suitability

CenterStage is suitable for:

- Brand lift studies
- Attention measurement
- Viewability/verification studies
- Controlled A/B creative testing
- Sequential messaging
- High-impact sponsorship reporting

Use caution when comparing CTR against standard banners because the format has a fundamentally different attention profile and user flow.

---

## 13. Accessibility & User Control

### Keyboard accessibility

- Close button must be reachable by keyboard.
- Escape key should close the overlay on desktop.
- Tab order should be logical.
- Focus should be trapped within the overlay while active, then returned to the previous page element after close.

### ARIA labels

Recommended labels:

```html
<button aria-label="Close advertisement">×</button>
<button aria-label="Skip advertisement">Skip</button>
<button aria-label="Pause video advertisement">Pause</button>
<button aria-label="Mute advertisement video">Mute</button>
<a aria-label="Learn more about [brand/product]">Learn More</a>
```

### Visible close button

- Must be visible against the creative background.
- Use a contrast-safe container if the background changes.
- Minimum tap target around 44×44 CSS px.
- Should not be hidden until animation completes unless a clear skip/countdown state is permitted by policy.

### Reduced motion

- Respect `prefers-reduced-motion`.
- Replace zoom/slide animation with a simple fade.
- Pause or simplify looping background motion.
- Avoid parallax-heavy or flashing animation.

### Pause/stop controls

Provide controls when:

- Video is longer than a short bumper.
- Animation loops continuously.
- Interactive content changes automatically.
- Motion may distract from content or accessibility needs.

### No forced sound

- Audio off by default.
- Sound only after explicit tap/click.
- State must be visible.
- Do not auto-unmute after replay.

### Clear CTA labeling

CTA should accurately describe the destination:

- “Learn More”
- “Shop the Sale”
- “Watch Trailer”
- “Book a Test Drive”
- “Explore Plans”
- “Find a Store”

Avoid vague or deceptive CTAs.

---

## 14. Performance & Loading Strategy

### Initial load strategy

- Load only shell, basic CSS, config, logo, teaser/backup image initially.
- Avoid loading heavy video before user initiation or active open.
- Keep first render lightweight.
- Use async/defer script loading.
- Avoid blocking publisher page render.

### Subload / lazy-load strategy

- Preload full-screen hero/video only after:
  - Ad slot is near viewport,
  - User hovers/clicks teaser,
  - Natural break is imminent,
  - Or publisher-approved delay has passed.
- Use `preload="metadata"` for video unless immediate playback is required.
- Use `loading="lazy"` where useful, but test inside iframes.

### Image optimization

- Use responsive assets.
- Compress backgrounds.
- Avoid oversized mobile images.
- Use poster/backup images.
- Consider WebP/AVIF only if fallback exists.

### Video lazy loading

- Do not block overlay open while downloading large video.
- Show poster frame instantly.
- Start muted playback only when allowed.
- Provide fallback if playback stalls.

### Font loading

- Prefer system fonts.
- If brand fonts are needed, use limited weights.
- Use `font-display: swap`.
- Avoid multiple heavy font files.

### Animation performance

- Use `transform` and `opacity`.
- Avoid layout-triggering animation.
- Avoid heavy filters and giant shadows.
- Use `requestAnimationFrame` for custom loops.
- Stop animation when hidden or closed.
- Use IntersectionObserver for teaser state where applicable.

### GPU-friendly transforms

Recommended:

```css
.centerstage-panel {
  transform: translate3d(0, 0, 0) scale(1);
  opacity: 1;
  transition: transform 280ms ease, opacity 220ms ease;
}
```

Avoid animating:

```css
top, left, width, height, margin, padding
```

at high frequency.

### Avoiding layout shift

- Use fixed overlay container.
- Do not insert full-screen content into page flow unless explicitly designed.
- Reserve teaser slot space.
- Do not change publisher page dimensions after load.
- Remove overlay cleanly on close.

### Low bandwidth fallback

- Detect slow connection where possible.
- Serve static backup or poster-first experience.
- Avoid auto-loading video.
- Reduce animation and image weight.

### Unsupported browser/app fallback

Fallback order:

1. Full rich-media CenterStage
2. Static/animated center modal
3. Same-slot expandable or static rich-media
4. Static backup image with CTA
5. No-ad/fail-safe state if required by publisher

---

## 15. QA Checklist

### Creative rendering QA

- [ ] Creative renders in all declared sizes.
- [ ] CenterStage opens at correct dimensions.
- [ ] Content remains centered.
- [ ] Background dim/overlay appears only when intended.
- [ ] Logo, headline, CTA, and legal text are visible.
- [ ] Backup image displays if JS/video fails.
- [ ] No unintended scrollbars inside iframe or overlay.
- [ ] Z-index hierarchy is correct.

### Interaction QA

- [ ] Close button visible from start or approved skip state.
- [ ] Close button works with mouse, tap, and keyboard.
- [ ] Escape key closes on desktop.
- [ ] Skip works if enabled.
- [ ] CTA click works and does not conflict with close.
- [ ] Background clicks do not create invalid click-throughs.
- [ ] Focus returns to page after close.
- [ ] Re-entry behavior follows configuration.
- [ ] Auto-open does not repeat in same page view after close.

### Tracking QA

- [ ] `creative_loaded` fires once.
- [ ] `impression_rendered` is not duplicated.
- [ ] `centerstage_open` fires on active open.
- [ ] `close`, `skip`, and `timeout_close` fire correctly.
- [ ] CTA click routes through GAM click tracking.
- [ ] Video events fire only once per quartile.
- [ ] Time-in-view is accurate.
- [ ] Third-party pixels cachebust correctly.
- [ ] Network logs confirm no blocked critical trackers.
- [ ] Error events are captured.

### GAM trafficking QA

- [ ] Correct creative type/template selected.
- [ ] All required variables populated.
- [ ] Declared sizes match line item sizes.
- [ ] Multi-size mapping tested.
- [ ] Click macros correctly escaped.
- [ ] Cachebuster macros correctly placed.
- [ ] SafeFrame tested.
- [ ] Preview works in GAM and staging page.
- [ ] Frequency cap key configured.
- [ ] Creative variant ID matches reporting.

### Mobile QA

- [ ] Close button visible above browser chrome.
- [ ] Safe areas respected on notched devices.
- [ ] `100vh`/`100dvh` behavior tested.
- [ ] Portrait and landscape tested if supported.
- [ ] CTA not hidden by home indicator.
- [ ] Tap targets are large enough.
- [ ] No accidental taps.
- [ ] Video uses `playsinline`.
- [ ] Audio remains muted until user action.
- [ ] Soft keyboard does not break layout if forms exist.

### Desktop QA

- [ ] Centered canvas scales across viewport sizes.
- [ ] Resize behavior works.
- [ ] Keyboard navigation works.
- [ ] Escape key close works.
- [ ] Overlay does not block browser controls.
- [ ] Scroll lock releases after close.
- [ ] Multi-monitor and high-DPI rendering acceptable.

### App QA

- [ ] SDK supports required overlay/expand behavior.
- [ ] MRAID/SDK methods tested if used.
- [ ] App safe areas respected.
- [ ] Back button behavior tested on Android.
- [ ] App background/resume tested.
- [ ] OMID measurement works where required.
- [ ] Click opens in expected app/browser context.
- [ ] Orientation behavior tested.

### Performance QA

- [ ] Initial load stays within target weight.
- [ ] Heavy assets politely loaded.
- [ ] No long main-thread blocks.
- [ ] Animation remains smooth.
- [ ] Low-end Android tested.
- [ ] Video startup does not freeze UI.
- [ ] Memory usage acceptable.
- [ ] Assets compressed.
- [ ] No unnecessary third-party libraries.

### Accessibility QA

- [ ] Close/skip controls have ARIA labels.
- [ ] Keyboard access works.
- [ ] Focus management works.
- [ ] Reduced-motion mode tested.
- [ ] Text contrast acceptable.
- [ ] CTA labels are descriptive.
- [ ] Motion/video can be paused or stopped where needed.

### Publisher safety QA

- [ ] Publisher approved trigger type.
- [ ] Publisher approved full-screen/near-full-screen behavior.
- [ ] Frequency cap configured.
- [ ] No content trap.
- [ ] Return-to-content behavior verified.
- [ ] No interference with consent/privacy UI.
- [ ] No misleading system UI.
- [ ] No unauthorized data collection.
- [ ] No policy-restricted auto audio.

---

## 16. Common Failure Cases

| Failure case | Likely cause | Practical fix |
|---|---|---|
| Creative clipped inside iframe | Standard display iframe restricts overlay. | Use SafeFrame expansion API, publisher wrapper, out-of-page placement, or same-slot modal fallback. |
| Expansion blocked by SafeFrame | SafeFrame config disallows viewport overlay. | Test SafeFrame settings; use approved rich-media template or publisher-side integration. |
| Close button hidden | Z-index conflict, video overlay, safe-area issue, or responsive bug. | Give close highest controlled z-index; safe-area padding; test over all backgrounds. |
| Close button too small on mobile | Desktop UI reused on mobile. | Use minimum 44×44 CSS px target and mobile-specific positioning. |
| Forced countdown causes complaints | User cannot dismiss quickly. | Prefer close from start; if countdown is required, keep short and clearly label skip/close state. |
| Autoplay blocked | Video not muted or browser policy blocks playback. | Start muted with `playsinline`; show poster and user play control. |
| Audio starts unexpectedly | Video/audio state not initialized as muted. | Set `muted`, `defaultMuted`, and no audio until user gesture. |
| Mobile viewport overflow | `100vh` mismatch, address bar changes, notches. | Use `100dvh` with fallback; recalc on resize/orientation; safe-area CSS. |
| Browser address bar covers CTA | CTA too low in viewport. | Add bottom safe padding and mobile breakpoint layout. |
| Scroll remains locked after close | Body scroll lock cleanup fails. | Store previous overflow/position state and restore on every close path. |
| User returns to wrong content position | Overlay code modifies page scroll. | Use fixed overlay; preserve scroll position before open and restore after close. |
| Video too heavy | Full video loaded on initial page load. | Lazy-load video after open or intent; use poster-first approach. |
| Page jank on open | Heavy JS/layout work during transition. | Precompute layout, use CSS transforms, defer non-critical work. |
| Third-party pixels cached | Missing cachebuster. | Add approved cachebuster macro to event URLs. |
| Click tracking not firing | Incorrect macro escaping or CTA bypasses click URL. | Validate macro expansion in GAM preview and live network logs. |
| Invalid click inflation | Close/skip/background counted as clicks. | Separate interaction events from click-through events. |
| Wrong size declared in GAM | Creative served into incompatible slot. | Align line item sizes, creative sizes, and GPT size mapping. |
| Frequency cap not respected | Cap stored only in volatile state or wrong key. | Use GAM frequency cap plus creative/session cap where appropriate. |
| In-app SDK not supporting overlay | SDK/webview blocks expansion or full-screen. | Use MRAID-compatible approach or app-native interstitial placement. |
| OMID measurement missing | Host app/webview not OM SDK integrated. | Confirm SDK support and measurement vendor certification. |
| Backup image missing | JS/video failure leaves blank overlay. | Require `backup_image_url` and test no-JS/video-fail conditions. |

---

## 17. Recommended Use Cases

| Industry | Campaign goal | Why this format fits | Example creative concept |
|---|---|---|---|
| Auto | New model launch / test drive | Large canvas supports cinematic reveal and feature highlights. | Full-screen car reveal with muted intro video, 3 feature cards, and “Book a Test Drive” CTA. |
| BFSI | Product education / lead generation | Centered layout can simplify complex offerings with controlled steps. | Credit card benefit reveal with calculator teaser and “Check Eligibility” CTA. |
| FMCG | Awareness / seasonal launch | High-impact visual burst works well for packshot and offer recall. | Festival product launch with animated packshot and coupon CTA. |
| Retail | Sale announcement / traffic | Full-screen urgency and clear CTA drive high visibility. | Mega sale takeover with countdown, category tiles, and “Shop Now”. |
| Entertainment | Trailer / premiere | Video-led takeover is suitable for cinematic storytelling. | Muted trailer teaser with skip, watch trailer CTA, and release date. |
| Real Estate | Project walkthrough | Large visual area supports floor plans, amenities, and lead form. | Hero render with amenity carousel and “Schedule Site Visit” CTA. |
| Travel | Destination inspiration | Immersive imagery/video supports aspiration and discovery. | Destination film card with package highlights and “Explore Packages”. |
| Tech | Product launch / app install | Helps explain features with animation and screenshots. | New smartphone reveal with feature sequence and “Pre-order Now”. |
| QSR | Offer / store visit | Strong full-screen offer visibility with location CTA. | New meal combo reveal with “Find Nearest Store” CTA. |
| Consumer Durables | Product demo / comparison | Center canvas can show feature benefits and usage scenarios. | Appliance feature animation with “Compare Models” CTA. |

---

## 18. Final Trafficker / Developer Handoff Summary

| Handoff Item | Requirement |
|---|---|
| Required assets | Backup image, logo, headline/body copy, CTA text/URL, background/hero image, optional video MP4, poster frame, legal text, tracking URLs. |
| Required dimensions | At minimum declare one approved serving size; recommended support for 300×250, 320×50, 320×480, 300×600, 728×90, 970×250, 970×500, and responsive/fullscreen variants where publisher supports them. |
| Required GAM variables | `click_url`, `cta_url`, `backup_image_url`, `auto_open`, `trigger_type`, `trigger_delay`, `max_display_seconds`, `close_enabled`, `skip_after_seconds`, `video_url`, `video_poster_url`, `muted`, `frequency_cap_key`, `creative_variant_id`, optional custom trackers. |
| Required tracking events | `creative_loaded`, `impression_rendered`, `viewable_impression`, `centerstage_open`, `time_in_view`, `close`, `skip`, `timeout_close`, `cta_click`, `click`, and video events if video is used. |
| Required QA checks | Close/skip visibility, return-to-content, viewport resize, mobile safe areas, browser chrome, video autoplay/mute, SafeFrame behavior, click tracking, frequency cap, performance, accessibility. |
| Publisher-side requirements | Approval for takeover behavior, trigger type, frequency cap, overlay permissions, SafeFrame/iframe expansion, scroll locking, video autoplay, and any data collection. |
| Known limitations | Full-screen behavior may be blocked in standard iframes or SafeFrame; app support depends on SDK/MRAID/OMID; auto-open is high-risk without frequency caps; video can hurt performance if not lazy-loaded; open exchange programmatic support may require custom deal setup. |
| Recommended implementation model | GAM custom creative template with configurable variables, publisher-approved wrapper for true full-screen overlay, static backup image, modular state machine, and shared tracking taxonomy for future ad-builder support. |

---

## Assumptions & Implementation Notes

- CenterStage Ad is a **custom high-impact rich-media execution**, not an official fixed-size IAB standard unit.
- The format should follow modern lightweight, non-disruptive ad principles.
- Full-screen or near full-screen behavior requires publisher approval.
- Auto-open behavior should be frequency-capped and used only at approved natural breaks or controlled delays.
- Video is optional; VAST is required only when a video player/ad tag workflow is used.
- Exact OpenRTB representation depends on SSP/DSP support and should be confirmed per supply path.
- Mobile app behavior depends on SDK, MRAID, OM SDK/OMID, and webview capabilities.
