# Scroll Activated Ad — Generalized Ad Specification

**Format name:** Scroll Activated Ad  
**Placement:** In-content / full-width interscroller placement  
**Compatibility:** Desktop web, mobile web, in-app webview / in-app rich media where supported  
**Primary behavior:** Scroll-triggered immersive rich-media unit that activates as the user scrolls into the placement and completes naturally as the user scrolls past it  
**Reference behavior:** Comparable to an interscroller-style rich-media display unit; not a forced interstitial and not a page-blocking takeover  
**Document purpose:** Production-ready technical, creative, trafficking, measurement, QA, and handoff specification for AcunX Showcase and future ad-builder automation

---

## Implementation Assumptions

1. This is a **custom rich-media display format**, not an official fixed IAB standard ad unit by itself.
2. It should be implemented using **IAB-compatible HTML5, lightweight ad-loading, SafeFrame-aware, OMID-ready, GAM-traffickable, and programmatic-friendly practices**.
3. The ad should be treated as an **in-content immersive unit** that is activated by scroll visibility, not by forcing the user into a full-screen modal experience.
4. The scroll behavior must be **non-blocking**. The user must be able to continue scrolling the page normally.
5. If video is used, it is optional and must follow muted autoplay and user-initiated audio rules.
6. For app inventory, MRAID / OM SDK support depends on the host SDK. Scroll progress and expansion behaviors must be tested in the exact app environment.
7. Publisher approval is recommended before live trafficking because this format affects page layout, scroll behavior, viewability, and measurement.

---

## Standards & Platform References

Use these as implementation guardrails, not as claims that the Scroll Activated Ad is itself an official standard format.

- IAB Tech Lab New Ad Portfolio / lightweight non-disruptive ad principles
- IAB Tech Lab HTML5 display creative guidance
- IAB Tech Lab SafeFrame implementation guidance
- IAB Tech Lab Open Measurement SDK / OMID guidance
- IAB Tech Lab MRAID guidance for in-app rich media
- IAB Tech Lab VAST guidance where video is served through a video player
- OpenRTB 2.x / AdCOM concepts for banner, video, native, rich media, creative attributes, and buyer metadata
- Google Ad Manager custom creatives, creative templates, macros, SafeFrame, GPT size mapping, and Active View measurement

---

## 1. Format Overview

A **Scroll Activated Ad** is an immersive in-content rich-media ad unit that becomes active when the placement scrolls into the user's viewport. It typically occupies a full-width section within the article, feed, or page body and uses scroll position to reveal brand content, animate layers, move products, trigger parallax effects, reveal copy, or tell a short visual story.

Unlike an interstitial, the format does **not** interrupt navigation, block the page, trap the user, or require an explicit close action before content can continue. It should behave like a premium content module embedded in the page flow. The user controls progression by scrolling.

### Core purpose

The format is designed to convert ordinary in-content display inventory into a high-attention, visually immersive storytelling unit while preserving user control and page continuity.

### Best use cases

- Product reveal or feature storytelling
- Automotive exterior/interior reveal
- Travel destination reveal
- Retail seasonal campaign storytelling
- Entertainment trailer teaser or release countdown
- BFSI product education flow
- FMCG sensory or pack-shot reveal
- Real estate walkthrough teaser
- Tech feature sequence
- QSR menu or offer discovery

### Brand value

- Higher visual attention than static banners
- More room for narrative than 300x250 or 728x90 units
- Better fit for premium storytelling and launch campaigns
- Supports controlled motion, product sequencing, optional video, and interactive hotspots
- Can be used as a bridge between standard display and high-impact sponsorship units

### Publisher value

- Premium in-content placement without a forced takeover
- Preserves page flow and reduces risk of intrusive ad complaints
- Can be packaged as high-impact rich media, sponsorship, or PMP/PG inventory
- Better suited to editorial environments than forced interstitials
- Allows reserved layout space, reducing layout shift when implemented correctly

### User experience value

- User remains in control through natural scrolling
- No forced full-screen interruption
- No required interaction to continue reading
- Can feel native to the page when motion intensity and layout are controlled
- Can be skipped simply by scrolling past the placement

### Classification

| Classification dimension | Recommended classification |
|---|---|
| Primary media category | Display / rich media |
| Placement type | In-content / full-width interscroller |
| Interaction driver | Scroll-triggered |
| Expansion behavior | In-content active expansion or reveal, not page-blocking expansion |
| Takeover status | Not a forced takeover |
| Sticky status | Not sticky by default; avoid persistent sticky behavior unless separately approved |
| Video-led status | Optional video support; not inherently a video format |
| Gamified status | Optional interactive/storytelling support; not inherently gamified |
| Programmatic packaging | Custom rich media, high-impact display, PMP / PG preferred |

---

## 2. Standard Ad Dimensions & States

The Scroll Activated Ad can be trafficked using fixed slot sizes, multi-size responsive mappings, or a fluid/responsive custom template depending on publisher setup. The key is to distinguish between the **declared serving size** and the **active creative canvas**.

- **Declared serving size:** Size sent to GAM / ad server / bid request.
- **Reserved layout size:** Space held in page to avoid layout shift.
- **Active canvas size:** Visual area used by the creative while the scroll activation is in progress.
- **Safe area:** Area where key copy, CTA, logo, close/minimize controls, and legal text must remain visible and tappable.

### Recommended states and variants

| State / Variant | Recommended collapsed size | Recommended expanded / active size | Device | Common placement | Notes |
|---|---:|---:|---|---|---|
| Mobile teaser banner | 320x50 | 100vw x 320-480, max 80vh | Mobile web / app | Article body, feed break | Use when only a small initial slot is available. Do not immediately push into full-screen. Reserve enough height before activation if possible. |
| Mobile medium rectangle | 300x250 | 320x480 or 100vw x 70-85vh | Mobile web / app | In-article / mid-feed | Good balance between traffickability and immersive reveal. Safe area should avoid browser UI, notch, and bottom nav. |
| Mobile portrait interscroller | 320x480 | 100vw x 80-90vh or fullscreen mobile safe area | Mobile web / app | Interscroller / feed module | Best mobile variant for visual storytelling. Must not trap scroll. Audio must remain off unless user taps. |
| Mobile fullscreen-style canvas | 320x480 or responsive | 100vw x 100svh, with safe-area padding | Mobile web / app | Premium mobile interscroller | Use only when page flow remains scrollable. This should not behave like a forced interstitial. Account for `env(safe-area-inset-*)`. |
| Desktop leaderboard teaser | 728x90 | 728x400, 970x500, or 100% container x 450-600 | Desktop | Article body, content break | Useful for editorial sites where leaderboard sizes are already approved. Needs clear reserved height to avoid layout shift. |
| Desktop billboard teaser | 970x90 | 970x250, 970x500, or 100% container x 450-600 | Desktop | Premium content break | Good for high-impact scroll reveal. Use when publisher has a wide content well. |
| Desktop billboard | 970x250 | 970x500 or 100% container x 500-650 | Desktop | Full-width interscroller | Strong recommended desktop implementation. Can support parallax/product reveal without feeling like a takeover. |
| Desktop immersive canvas | 970x250 or responsive | 100vw x 500-700, max 85vh | Desktop | Wide article break / homepage module | Requires publisher approval because it affects layout and page experience. Keep CTA/logo inside central safe area. |
| Large vertical fallback | 300x600 | 300x600 or 100% column x 600 | Desktop / tablet | Sidebar-like or narrow content well | Not ideal for full-width interscroller, but useful where publisher inventory is vertical. Avoid scroll hijacking. |
| Medium rectangle fallback | 300x250 | 300x250 or 300x400 | Desktop / mobile | Standard display slot | Use as fallback when scroll activation is unsupported. Can show static or lightly animated state. |
| Responsive full-width | Fluid / responsive | Container width x 40-85vh | Desktop / mobile | In-content section | Preferred for custom publisher integration. Requires GPT size mapping or custom template logic. |
| App MRAID-supported interscroller | 320x50, 300x250, 320x480, or SDK-supported | SDK viewport / container-dependent | In-app | Feed / article card | Must verify MRAID resize/expand, OMID, scroll visibility, and SDK autoplay policies. |

### Size-specific guidance

| Size | Recommended use | Safe-area considerations |
|---:|---|---|
| 300x250 | Default fallback and mobile/desktop mid-content entry point | Keep core message visible even without activation. CTA minimum 44x44 CSS px on touch devices. |
| 320x50 | Lightweight teaser only | Avoid dense text. Use as a pre-activation prompt, not as the full creative experience. |
| 320x480 | Strong mobile portrait active canvas | Keep logo and CTA away from top notch, browser bottom bars, and app nav. Use 16-24 px internal padding minimum. |
| 300x600 | Narrow vertical fallback or tablet/sidebar variant | Avoid pretending it is full-width. Use vertical storytelling, not forced expand. |
| 728x90 | Desktop/tablet teaser or fallback | Do not put legal text or detailed messages here. Use as entry state into a larger in-content canvas. |
| 970x90 | Premium desktop teaser | Good for publisher approval because it maps to known billboard inventory. Expand/reveal into a reserved section. |
| 970x250 | Preferred desktop high-impact declared size | Enough room for a meaningful static fallback and smooth active state. |
| 970x500 | Preferred desktop active canvas | Keep important content inside central 970x420 region; allow edges for decorative parallax. |
| Fullscreen mobile | Only for non-blocking scroll-controlled interscroller | Must not cover content outside the reserved scroll section. Use safe-area CSS and no forced close requirement. |
| Fullscreen desktop | Use with caution; better as viewport-height in-content section | Avoid modal overlay behavior. Keep page scroll available and provide fallback when iframe expansion is constrained. |
| Responsive / viewport-based | Best for future ad-builder support | Define min/max heights, aspect ratio limits, breakpoint rules, and fallback fixed sizes. |

### Recommended responsive breakpoints

| Breakpoint | Declared / fallback size | Active height recommendation | Notes |
|---|---:|---:|---|
| `< 360px` mobile | 320x50 or 300x250 | 360-480 px, max 85vh | Avoid horizontal overflow. |
| `360-767px` mobile | 320x480 or responsive | 70-90vh | Best mobile storytelling range. |
| `768-1023px` tablet | 728x90 or responsive | 400-550 px | Avoid tiny typography. |
| `1024-1279px` desktop | 970x250 or responsive | 450-600 px | Standard premium desktop. |
| `>= 1280px` wide desktop | 970x250 / 970x500 / responsive | 500-700 px, max 85vh | Decorative background may extend; content should remain centered. |

---

## 3. User Experience & Behaviour Specification

### Behaviour summary

| Behaviour item | Specification |
|---|---|
| Primary trigger | Scroll-triggered when placement enters viewport |
| User initiation | User initiates progression by scrolling; clicks/taps are optional secondary interactions |
| Auto-started behavior | Motion may begin on view; audio must not auto-start |
| Time-bound | Recommended animation should complete within the scroll distance or 3-8 seconds of active viewing |
| Dismissible | Optional close/minimize control if the unit overlays or pins content; not required if purely in-flow and non-blocking |
| Frequency-capped | Recommended for premium variants and heavy animation/video variants |
| Non-blocking | Required |
| Sticky / persistent | Not default; only allowed if separately approved |
| Full-screen / takeover | Not a forced takeover; fullscreen-style canvas must remain scroll-controlled and escapable |

### Initial state

The unit appears as a reserved in-content placement, teaser, or static fallback. Before activation, it should:

- Reserve height to avoid cumulative layout shift.
- Show a lightweight first frame, poster, or branded teaser.
- Avoid heavy scripts and large video downloads before the unit approaches the viewport.
- Be meaningful if animation never starts.
- Be clearly recognizable as advertising when required by publisher policy.

### Trigger condition

The recommended activation trigger is viewport visibility using `IntersectionObserver` or host SDK visibility callbacks.

Recommended thresholds:

| Trigger | Recommendation |
|---|---|
| Preload trigger | Unit within 1-2 viewport heights before entering view |
| Activation trigger | 30-50% of placement visible, or publisher-defined viewability threshold |
| Scroll progress mapping | Use element position relative to viewport, not global page scroll only |
| Re-trigger | Once per impression by default; optional replay after full exit and re-entry |
| Measurement trigger | Separate `creative_in_view`, `viewable_impression`, and `scroll_activation_start` events |

### Animation / transition

The unit may use:

- Parallax background movement
- Layered product reveal
- Frame sequence reveal
- Static image reveal with copy transitions
- Scroll-synced story panels
- Optional lightweight video start when in view
- Hotspot fade-in after scroll progress reaches a defined point

Animation principles:

- Use `transform` and `opacity` where possible.
- Avoid animating layout-heavy properties such as `top`, `left`, `height`, and `width` continuously.
- Avoid scroll hijacking.
- Avoid forcing the user's scroll velocity.
- Do not lock body scroll.
- Keep animation reversible only if useful; otherwise allow natural completion.

### Interaction model

Primary interaction is scroll. Secondary interactions may include:

- CTA click/tap
- Hotspot click/tap
- Swipe between panels on mobile
- Product tile selection
- Video play/pause/mute/unmute
- Replay button after completion
- Optional expand/read-more interaction

The unit should remain useful for users who do not interact beyond scrolling.

### Expanded / active state

The active state is the immersive visual state shown while the user is inside the placement. It should:

- Occupy the reserved in-content section or approved active canvas.
- Keep page scroll functional.
- Reveal content based on scroll progress or visible time.
- Avoid covering unrelated page content unless explicitly approved.
- Keep CTA and controls visible inside safe areas.
- Prevent accidental clicks from scroll gestures.

### Close / collapse behavior

Because this is an in-content unit, close behavior differs from overlay formats.

| Scenario | Expected behavior |
|---|---|
| Pure in-flow interscroller | No close required; user scrolls past naturally. |
| Unit uses fixed/pinned internal layer | Provide close/minimize button. |
| Unit contains video/audio controls | Provide pause/mute controls. |
| Unit expands beyond reserved placement | Provide visible close/collapse and test with SafeFrame. |
| User closes manually | Collapse to fallback height or hide interactive layer; do not remove page content unexpectedly. |

### Re-entry behavior

Recommended default:

- On first entry: activate animation.
- On scroll past completion: mark `interaction_complete` if the user reached the final section.
- On re-entry during same page view: preserve completed state or allow replay only with explicit replay control.
- Do not repeatedly auto-start heavy video or re-fire primary engagement events.

### Mobile behavior

- Use portrait-first layout.
- Keep visual hierarchy simple.
- Do not use hover-only interactions.
- Touch targets should be at least 44x44 CSS px.
- Use `playsinline` for video.
- Avoid body scroll lock.
- Avoid horizontal overflow.
- Account for browser UI, notches, app bottom navigation, and safe-area insets.
- Use passive scroll listeners when needed.
- Avoid scroll jank from frame sequences or large images.

### Desktop behavior

- Use wider composition with central safe area.
- Support mouse click/tap-equivalent interactions.
- Avoid forcing full-screen unless publisher has approved the experience.
- Ensure the creative works inside an iframe.
- If using parallax, keep motion subtle and non-nauseating.
- Test in common viewport widths: 1024, 1280, 1366, 1440, 1920.

### App behavior

- Use MRAID only when available and required by SDK.
- Use OMID / OM SDK for measurement where supported.
- Verify whether the host SDK supports scroll visibility, resize, expand, video autoplay, and external click handling.
- Avoid assuming browser APIs are available in all in-app webviews.
- Test Android and iOS separately.
- Respect app safe areas and publisher app navigation.

### Accessibility expectations

- Do not rely only on motion to communicate core information.
- Provide clear CTA labels.
- Provide keyboard focus styles for interactive controls where keyboard access applies.
- Respect `prefers-reduced-motion`.
- Provide pause/stop controls for long or looping motion.
- Keep text contrast readable.
- Avoid flashing or rapid strobe effects.

---

## 4. Creative Design Guidelines

### Layout hierarchy

Recommended hierarchy:

1. Brand/logo identifier
2. Main visual/product/destination/story frame
3. Short headline
4. Supporting copy or feature callout
5. CTA
6. Legal/disclaimer text if required
7. Optional interactive hints such as “Scroll to explore” or “Tap to view details”

### CTA placement

- Mobile: bottom-center or lower-right within safe area; avoid browser bottom UI.
- Desktop: lower-right or right-center, depending on layout.
- CTA should remain visible during key active moments.
- Avoid placing CTA where users naturally swipe/scroll to prevent accidental clicks.
- For multi-stage stories, CTA can appear persistently after 40-60% scroll progress or at the completion state.

### Logo placement

- Keep logo visible but not dominant.
- Recommended placement: top-left or top-right safe area.
- Maintain enough padding from viewport edges and notches.
- Avoid placing logo over highly textured backgrounds unless backed by a gradient or surface.

### Safe zones

| Device | Minimum internal safe padding | Recommended content-safe area |
|---|---:|---|
| Mobile web | 16 px + safe-area insets | Center 90% width, excluding top/bottom browser UI |
| In-app | 16-24 px + SDK/app safe areas | Avoid app nav, close controls, and OS gesture areas |
| Desktop | 24-48 px | Central 970 px or publisher content width |
| Wide desktop | 48-96 px | Decorative edges allowed; key content centered |

### Readability

- Use short headlines, ideally 3-8 words.
- Avoid body copy smaller than 12 px mobile / 14 px desktop.
- Legal text should not be hidden or unreadable.
- Use overlays or scrims behind text over image/video.
- Avoid text-heavy storytelling; use progressive reveal.

### Motion intensity

- Keep scroll-linked movement smooth and subtle.
- Avoid rapid direction changes.
- Avoid continuous spinning, flashing, or aggressive zooming.
- Avoid parallax depth that creates nausea.
- Use reduced-motion fallback.

### Animation timing

| Animation type | Recommended duration |
|---|---:|
| Entrance fade / reveal | 250-500 ms |
| Layer transition | 300-700 ms |
| Product reveal | 500-1200 ms |
| Scroll-progress animation | Bound to scroll progress; avoid time-only forced playback |
| CTA reveal | After first key message or 40-60% scroll progress |
| Looping ambient motion | 3-8 seconds per loop; pause or reduce after completion |

### Touch targets

- Minimum target: 44x44 CSS px.
- Preferred mobile CTA height: 44-56 px.
- Keep controls separated by at least 8 px.
- Avoid tiny mute/close icons.

### Close button placement

Close is optional for pure in-flow units. If used:

- Place in top-right safe area.
- Minimum 44x44 CSS px on touch devices.
- Use clear icon and accessible label.
- Do not hide it behind animation layers.
- Do not make close click open the advertiser landing page.

### Visual density

- One primary message per scroll stage.
- Avoid more than 3-4 active foreground layers on mobile.
- Avoid cluttered product grids unless using deliberate carousel/tile interaction.
- Prioritize fast comprehension over cinematic complexity.

### Responsive scaling

- Use CSS clamp values for font sizes.
- Define breakpoints for mobile, tablet, desktop, and wide desktop.
- Do not scale a desktop composition directly into mobile.
- Provide separate focal points for mobile crops.

### Brand safety

- Avoid misleading UI, fake system controls, fake notifications, or deceptive close buttons.
- Avoid animation that could be mistaken for publisher navigation.
- Ensure brand content is clearly distinguishable from editorial content where required.
- Respect publisher category exclusions and sensitive-content restrictions.

### Avoiding intrusive UX

This format should never:

- Lock page scroll.
- Force a close before reading continues.
- Auto-play sound.
- Take over the full page as a modal unless explicitly trafficked as a different approved format.
- Cover publisher navigation or content unexpectedly.
- Trigger on every re-entry in a way that frustrates users.

### Do / Don’t recommendations

| Do | Don’t |
|---|---|
| Reserve layout space before loading creative. | Inject a large active canvas after render and cause layout shift. |
| Use scroll progress as a storytelling input. | Hijack scrolling or force the page to snap aggressively. |
| Keep motion GPU-friendly. | Animate layout properties continuously. |
| Provide static fallback. | Depend on advanced animation for the only brand message. |
| Keep audio muted by default. | Start sound on scroll. |
| Test SafeFrame and iframe constraints. | Assume the creative can always access the parent page. |
| Use clear CTA and controls. | Use misleading controls or accidental click zones. |
| Cap heavy asset loads until near view. | Download all video and frame sequences on page load. |
| Treat mobile/app separately. | Shrink the desktop creative into mobile without redesign. |

---

## 5. Asset Specifications

### A. Image Assets

#### Supported formats

| Asset type | Recommended formats | Notes |
|---|---|---|
| Background images | JPG, WebP, AVIF, PNG fallback | Use JPG/WebP/AVIF for photographic backgrounds. |
| Transparent overlays | PNG, WebP with alpha, SVG for vector | Keep transparent overlays optimized. |
| Logos / icons | SVG preferred, PNG fallback | Ensure legibility on high-density screens. |
| Product cutouts | PNG/WebP with alpha | Use 2x assets for retina where needed. |
| Fallback image | JPG/WebP + PNG fallback | Must communicate core message without animation. |

#### Recommended compression

- Use WebP/AVIF where publisher and ad server support it; provide JPG/PNG fallback for compatibility.
- Compress photographic backgrounds aggressively without visible banding.
- Use SVG for simple vector icons and logos where allowed.
- Avoid shipping uncompressed PNG backgrounds.
- Use responsive image variants where the ad-builder can generate them.

#### Retina / high-density considerations

- Provide 2x resolution for logos, product cutouts, and key UI assets.
- Avoid 3x assets unless necessary; they can be too heavy for ad delivery.
- Use CSS to scale down high-density assets rather than serving oversized desktop images to mobile.

#### Background image rules

- Provide separate mobile and desktop crops.
- Keep focal point metadata in the ad-builder schema.
- Avoid placing required text inside the background image unless unavoidable.
- Use overlay gradients to ensure text contrast.

#### Transparent overlay rules

- Optimize alpha assets.
- Avoid full-screen transparent PNGs when CSS gradients or SVG can do the same job.
- Keep z-index layers documented.
- Do not put invisible clickable overlays over the whole unit except the declared CTA zone.

#### Maximum recommended image file sizes

| Asset | Initial load target | Polite / secondary load target | Notes |
|---|---:|---:|---|
| Fallback/poster image | 50-100 KB | N/A | Must load quickly. |
| Mobile background | 80-180 KB | 150-250 KB | Depends on visual complexity. |
| Desktop background | 120-250 KB | 250-400 KB | Use responsive variants. |
| Logo / icon | 5-30 KB | N/A | SVG or optimized PNG. |
| Product cutout | 40-120 KB | 100-180 KB | Avoid multiple large alpha PNGs. |
| Frame sequence | Avoid in initial load | 500 KB-1.5 MB total maximum | Use only with lazy loading and frame decimation. |

### B. Video Assets

Video is optional for Scroll Activated Ads. When used, video should support the scroll story and must not dominate initial load.

#### Supported video formats

| Field | Recommendation |
|---|---|
| Container | MP4 |
| Video codec | H.264 baseline/main profile for broad compatibility |
| Audio codec | AAC if audio exists |
| Autoplay | Muted only |
| Sound | User-initiated only |
| Mobile playback | `playsinline` required |
| Poster frame | Required |
| Fallback image | Required |
| Captions | Recommended when speech or important audio is used |

#### Duration guidance

| Use case | Recommended duration |
|---|---:|
| Ambient background loop | 3-8 seconds |
| Product demo snippet | 6-15 seconds |
| Trailer teaser | 6-15 seconds, with user-initiated full video click-out if needed |
| Interactive story clip | 5-12 seconds per section |

#### Looping guidance

- Loop only muted ambient clips.
- Avoid infinite heavy playback when out of view.
- Pause when the unit leaves view.
- Provide replay only after completion or on user request.

#### Max file-size guidance

| Video asset | Initial load | Polite / secondary load | Notes |
|---|---:|---:|---|
| Poster image | 50-150 KB | N/A | Required. |
| Short mobile MP4 | Avoid initial unless tiny | 500 KB-1.5 MB | Lazy-load near viewport. |
| Short desktop MP4 | Avoid initial unless tiny | 1-3 MB | Use adaptive variant if possible. |
| Long video | Not recommended in creative bundle | Serve through player/VAST or click out | Keep display unit lightweight. |

### C. HTML5 / JS / CSS Assets

#### Bundle expectations

- Prefer a single HTML5 creative bundle with `index.html`, CSS, JS, and assets.
- Use externally hosted assets only if publisher/ad server policy allows them.
- Keep all third-party domains approved and documented.
- Include a static fallback if JS fails.
- Avoid dependencies that are unnecessary for a single ad unit.

#### CDN-hosted assets

CDN assets may be acceptable for large shared libraries or dynamic creative assets, but should be:

- HTTPS only.
- Cacheable.
- Versioned.
- Approved by publisher/security policy.
- Covered by fallback logic.
- Avoided for critical first paint if latency is uncertain.

#### Avoiding heavy JS

- Avoid full animation frameworks unless needed.
- Prefer CSS transforms, lightweight requestAnimationFrame loops, and IntersectionObserver.
- Avoid blocking scripts in the initial render path.
- Avoid collecting unnecessary user/device data.
- Avoid parent-page DOM access unless using approved SafeFrame/MRAID APIs.

#### Animation performance

- Use `transform: translate3d(...)`, `scale`, and `opacity`.
- Add `will-change` sparingly and remove when not needed.
- Avoid huge box shadows and filters on mobile.
- Avoid simultaneous video + heavy parallax + multiple frame sequences.
- Throttle scroll progress updates.

#### Request count discipline

| Resource type | Recommended maximum |
|---|---:|
| Initial critical requests | 5-8 |
| Total creative requests | 15-25, depending on publisher policy |
| Third-party tracking pixels | 5 standard configurable slots maximum |
| Fonts | 0-1 families; prefer system fonts when possible |
| Video requests | Lazy-loaded only, unless required by template |

#### Fallback behavior

Fallback must display when:

- JS is blocked.
- IntersectionObserver is unavailable.
- SafeFrame prevents expansion/communication.
- MRAID APIs are unavailable.
- Video autoplay is blocked.
- Low bandwidth mode is detected.
- Creative errors occur.

### D. Optional Interactive Assets

Optional modules should be controlled by the ad-builder schema and enabled only when needed.

| Asset / module | Use case | Requirements |
|---|---|---|
| Hotspots | Product feature reveal | Keyboard/touch accessible, labelled, tracked. |
| Cards | Story panels or product details | Must not overflow mobile viewport. |
| Product tiles | Retail/auto/consumer durable comparison | Use clear CTA per tile; avoid too many on mobile. |
| Quiz / game state | Engagement and education | Keep optional, non-blocking, and short. |
| Swipe gestures | Mobile panels | Provide visible controls as fallback. |
| Drag gestures | Product rotate/reveal | Avoid interfering with page scroll. |
| Form fields | Lead gen add-on | Requires privacy, consent, validation, and secure handling. Not default. |
| Multiple CTAs | Multiple product/category destinations | Track separately; avoid click inflation. |

---

## 6. IAB / UX Compliance Considerations

The Scroll Activated Ad should align with modern lightweight and non-disruptive ad principles.

### Required compliance posture

| Principle | Requirement for this format |
|---|---|
| Lightweight initial load | Load only shell, fallback image, essential CSS/JS initially. |
| Polite loading | Load heavier assets only when close to viewport or after activation. |
| No unexpected audio | Audio must be muted by default and user-initiated. |
| Clear controls | CTA, mute, pause, replay, and close/minimize controls must be clear when present. |
| No blocked content | Do not trap the user or block reading. |
| Avoid layout shift | Reserve height before loading and define slot dimensions. |
| Respect mobile viewport | Use safe-area CSS and avoid overflow. |
| Avoid misleading UI | No fake OS alerts, fake publisher navigation, or deceptive close buttons. |
| User control | User can scroll past the unit naturally. |
| Measurement integrity | Do not fire engagement or click events without genuine user action or valid visibility trigger. |

### Format-specific compliance risks

| Risk | Why it matters | Mitigation |
|---|---|---|
| Looks like forced interstitial | May violate publisher UX expectations | Keep unit in page flow; no scroll trap; label as interscroller/rich media. |
| Scroll hijacking | Creates poor UX and accessibility issues | Map animation to scroll without preventing default scroll. |
| Layout shift | Damages page UX and metrics | Reserve height; use known slot dimensions. |
| Heavy video/frame sequences | Hurts performance and viewability | Lazy-load, compress, and provide fallback. |
| Accidental clicks during scroll | Inflates invalid clicks | Keep clickable areas explicit and avoid full-unit click overlays on mobile. |
| SafeFrame restrictions | Expansion/parent communication may fail | Build SafeFrame-aware and test in target environment. |
| In-app SDK differences | MRAID/OMID behavior varies | Test SDK-specific builds and fallbacks. |

---

## 7. GAM Implementation Specification

### Recommended GAM setup

| Item | Recommendation |
|---|---|
| Creative type | Custom creative or custom creative template for reusable trafficking. HTML5 creative may be used for simple static/fallback variants. |
| Template strategy | Use a custom creative template with configurable variables for assets, tracking, CTA, video, scroll thresholds, and variants. |
| SafeFrame | Enable/test SafeFrame carefully. Use SafeFrame-compatible APIs where possible. If expansion beyond iframe is required, publisher approval and SafeFrame support must be verified. |
| Required creative sizes | Declare all supported fixed sizes and responsive mappings used by the publisher. Recommended: 300x250, 320x50, 320x480, 728x90, 970x90, 970x250, 970x500 where approved. |
| Multi-size mapping | Use GPT size mapping for desktop/tablet/mobile. Multi-size slots must reserve enough space for the largest eligible size or use responsive layout strategy. |
| Key-values / custom fields | Use keys for format, device, placement, variant, industry, creative complexity, and test mode. |
| Click-through URL | Use GAM click macro or template click-through field. All CTAs should route through valid click tracking. |
| Impression tracking | Use GAM impression counting plus optional third-party impression pixels. Avoid duplicate billing signals. |
| Third-party tracking pixels | Support up to 5 configurable pixels with cachebusters. |
| Cachebuster handling | Use GAM cachebuster macros or template-generated random values for third-party pixels. |
| Preview and QA | Test in GAM preview, publisher staging page, SafeFrame on/off, desktop/mobile, app SDK where applicable. |

### Recommended GAM line item / creative notes

- Package as a **custom high-impact rich-media display unit**.
- Use a dedicated ad unit or placement group for in-content interscroller inventory.
- Avoid serving into ordinary small slots unless fallback mode is enabled.
- Coordinate with publisher engineering for reserved height, CSS containment, and safe scroll behavior.
- Separate the unit from forced interstitial inventory in naming, targeting, and reporting.

### Suggested GAM size mapping

| Viewport | Eligible sizes | Notes |
|---|---|---|
| Mobile narrow | 320x50, 300x250, 320x480 | 320x480 preferred for immersive variant. |
| Mobile wide / tablet | 300x250, 320x480, 728x90 | Use responsive active canvas. |
| Desktop standard | 728x90, 970x90, 970x250 | 970x250 preferred declared premium size. |
| Desktop immersive | 970x250, 970x500 | Requires publisher approval and reserved height. |
| Fallback only | 300x250, 728x90 | Static or light animation only. |

### Recommended key-values / custom fields

| Key | Example value | Purpose |
|---|---|---|
| `format` | `scroll_activated_ad` | Format identification. |
| `placement_type` | `interscroller` | Publisher placement mapping. |
| `device_group` | `mobile_web`, `desktop`, `app` | Device-specific rendering logic. |
| `variant` | `parallax_reveal`, `product_story`, `video_teaser` | Creative variant reporting. |
| `industry` | `auto`, `retail`, `bfsi` | Sales/package and creative reporting. |
| `animation_level` | `low`, `medium`, `high` | QA and performance classification. |
| `video_enabled` | `true`, `false` | Routing to video-capable template. |
| `safe_frame_tested` | `true`, `false` | Internal QA flag. |
| `publisher_approved` | `true`, `false` | Required before live launch. |

### GAM configurable variables

| Variable name | Type | Example | Required / Optional | Purpose |
|---|---|---|---|---|
| `creative_variant_id` | String | `scroll_auto_parallax_v1` | Required | Identifies the creative build and variant. |
| `click_url` | URL / GAM click macro field | `%%CLICK_URL_ESC%%https://brand.example/landing` | Required | Primary click-through destination with GAM click tracking. |
| `cta_text` | String | `Explore the range` | Required | CTA label shown in the unit. |
| `cta_url` | URL | `https://brand.example/landing` | Required if separate from `click_url` | Destination for CTA-specific tracking. |
| `backup_image_url` | URL | `https://cdn.example/fallback.jpg` | Required | Static fallback if JS/video/animation fails. |
| `desktop_background_url` | URL | `https://cdn.example/bg-desktop.webp` | Optional | Desktop background image. |
| `mobile_background_url` | URL | `https://cdn.example/bg-mobile.webp` | Optional | Mobile background image. |
| `logo_url` | URL | `https://cdn.example/logo.svg` | Optional | Brand logo asset. |
| `scroll_trigger_threshold` | Number | `0.5` | Required | Viewport ratio required to activate animation. |
| `preload_margin` | String / Number | `150vh` | Optional | Distance before viewport to begin loading secondary assets. |
| `animation_mode` | Enum | `parallax`, `static_reveal`, `layered_reveal`, `story_panels` | Required | Determines active creative behavior. |
| `animation_intensity` | Enum | `low`, `medium`, `high` | Optional | Controls motion strength. |
| `replay_enabled` | Boolean | `false` | Optional | Allows user replay after completion. |
| `close_button_enabled` | Boolean | `false` | Optional | Required only if unit overlays, pins, or expands beyond reserved content. |
| `collapse_on_exit` | Boolean | `true` | Optional | Whether active effects collapse/complete after scroll exit. |
| `frequency_cap_key` | String | `scroll_ad_brand_campaign_001` | Optional | Used by publisher/ad-builder to limit repeated heavy experience. |
| `autoplay` | Boolean | `true` | Optional, video only | Allows muted video playback when in view. |
| `muted` | Boolean | `true` | Required if video exists | Ensures compliant muted autoplay. |
| `video_loop` | Boolean | `false` | Optional, video only | Loops ambient video if approved. |
| `video_url` | URL | `https://cdn.example/video.mp4` | Optional, video only | HTML5 video asset. |
| `poster_image_url` | URL | `https://cdn.example/poster.jpg` | Required if video exists | Poster/fallback for video. |
| `impression_url` | URL | `https://tracker.example/imp?cb=%%CACHEBUSTER%%` | Optional | Third-party impression tracker. |
| `interaction_tracking_url` | URL | `https://tracker.example/interact?...` | Optional | Generic interaction tracker. |
| `video_start_tracking_url` | URL | `https://tracker.example/vstart?...` | Optional, video only | Video start tracking. |
| `video_complete_tracking_url` | URL | `https://tracker.example/vcomplete?...` | Optional, video only | Video completion tracking. |
| `custom_tracking_pixel_1` | URL | `https://tracker1.example/pixel?cb=%%CACHEBUSTER%%` | Optional | Third-party pixel slot. |
| `custom_tracking_pixel_2` | URL | `https://tracker2.example/pixel?cb=%%CACHEBUSTER%%` | Optional | Third-party pixel slot. |
| `custom_tracking_pixel_3` | URL | `https://tracker3.example/pixel?cb=%%CACHEBUSTER%%` | Optional | Third-party pixel slot. |
| `custom_tracking_pixel_4` | URL | `https://tracker4.example/pixel?cb=%%CACHEBUSTER%%` | Optional | Third-party pixel slot. |
| `custom_tracking_pixel_5` | URL | `https://tracker5.example/pixel?cb=%%CACHEBUSTER%%` | Optional | Third-party pixel slot. |
| `reduced_motion_fallback` | Boolean | `true` | Required | Enables accessible low-motion experience. |
| `debug_mode` | Boolean | `false` | Optional | Enables console logs in staging only. |

Variables intentionally not defaulted:

- `expand_on_load`: Not recommended for this format because activation should be scroll-triggered, not automatic on page load.
- `expand_on_click`: Optional only for a manual read-more variant; not part of the core behavior.

---

## 8. Tracking & Analytics Event Taxonomy

The event taxonomy should separate rendering, visibility, activation, interaction, video, and completion events. Do not over-count scroll-based events as user clicks.

### Core events

| Event name | Trigger | Required / Optional | Tracking method | Notes |
|---|---|---|---|---|
| `creative_loaded` | Creative JS/CSS initialized successfully | Required | JS event + internal log / pixel optional | Fires once per creative instance. |
| `impression_rendered` | Ad markup rendered in slot | Required | GAM impression + optional third-party pixel | Do not duplicate billing events unnecessarily. |
| `viewable_impression` | Meets viewability rule, commonly 50% in view for required duration | Required where measurable | Active View / OMID / verification vendor | Keep separate from render. |
| `creative_in_view` | Placement crosses configured viewport threshold | Required | IntersectionObserver / MRAID / SDK visibility | Used for scroll activation analysis. |
| `scroll_activation_start` | Animation begins due to scroll trigger | Required | JS event / event pixel | Key event for this format. |
| `scroll_progress_25` | User reaches 25% of scroll story | Optional | JS event, sampled if needed | Avoid firing repeatedly. |
| `scroll_progress_50` | User reaches 50% of scroll story | Optional | JS event | Useful for storytelling depth. |
| `scroll_progress_75` | User reaches 75% of scroll story | Optional | JS event | Useful for completion funnel. |
| `scroll_progress_100` | User reaches end of scroll story | Optional | JS event | May map to interaction completion if no other interaction. |
| `collapse` | Unit exits active region or returns to fallback state | Optional | JS event | Natural collapse, not necessarily user action. |
| `close` | User taps/clicks close or minimize | Optional / required if close exists | Click event + tracker | Must be separate from ad click. |
| `click` | User clicks any valid outbound click zone | Required | GAM click macro + click tracker | Do not fire from scroll gestures. |
| `cta_click` | User clicks primary CTA | Required | GAM click macro + CTA-specific event | Should include CTA ID if multiple CTAs. |
| `hotspot_click` | User clicks/taps a hotspot | Optional | JS event / interaction tracker | Track hotspot ID. |
| `card_view` | Story/product card becomes visible | Optional | JS event | Useful for card-based variant. |
| `card_click` | User clicks card/tile | Optional | JS event + click tracker if outbound | Track card ID. |
| `swipe_next` | User swipes or taps next panel | Optional | JS event | Mobile panel variant only. |
| `swipe_previous` | User swipes or taps previous panel | Optional | JS event | Mobile panel variant only. |
| `time_in_unit` | Total active/visible time accumulated | Required for engagement reporting | JS timer with visibility gating | Pause timer when out of view. |
| `interaction_complete` | User reaches final story state or completes intended interaction | Optional / recommended | JS event | Define per creative variant. |
| `error` | Creative fails to load module/asset | Optional internal | JS event / console in debug | Useful for QA and monitoring. |

### Video events, if video is enabled

| Event name | Trigger | Required / Optional | Tracking method | Notes |
|---|---|---|---|---|
| `video_start` | Video starts playback | Required if video exists | JS event / VAST event if player-served | Only after actual playback starts. |
| `video_25` | 25% quartile reached | Recommended | JS / VAST quartile | Pause when out of view. |
| `video_50` | 50% quartile reached | Recommended | JS / VAST quartile |  |
| `video_75` | 75% quartile reached | Recommended | JS / VAST quartile |  |
| `video_complete` | Video reaches completion | Recommended | JS / VAST complete |  |
| `video_mute` | User mutes video | Optional | JS event | Initial muted state should not count as user mute. |
| `video_unmute` | User explicitly unmutes | Required if sound available | JS event | User-initiated only. |
| `video_pause` | User pauses or unit pauses due to out-of-view | Optional | JS event | Distinguish user pause vs auto-pause if possible. |
| `video_replay` | User clicks replay | Optional | JS event | Should not auto-fire repeatedly. |

### Events intentionally excluded by default

| Event | Reason |
|---|---|
| `game_start` | Not core to this format unless a gamified module is added. |
| `game_complete` | Not core unless using a game variant. |
| `carousel_next` / `carousel_previous` | Use only if carousel variant exists. |
| `expand` | Optional; use `scroll_activation_start` or `active_state_enter` to avoid implying forced expansion. |

---

## 9. GAM Macros & Click Tracking

GAM macros should be used to preserve ad-server click tracking, cachebusting, and dynamic creative configuration without hardcoding final values in the creative.

### Click macro usage

Recommended pattern:

```html
<a id="primaryCta" href="%%CLICK_URL_ESC%%${CTA_URL}" target="_blank" rel="noopener noreferrer">
  ${CTA_TEXT}
</a>
```

Where:

- `%%CLICK_URL_ESC%%` is the GAM click tracking prefix placeholder.
- `${CTA_URL}` is the trafficked landing page or template variable.
- The creative must not manually redirect in a way that bypasses the click macro.

For multiple CTAs:

```html
<a href="%%CLICK_URL_ESC%%${CTA_URL_1}" data-cta-id="primary">Shop now</a>
<a href="%%CLICK_URL_ESC%%${CTA_URL_2}" data-cta-id="secondary">Learn more</a>
```

Each CTA should also fire a non-billing analytics event such as `cta_click` with `cta_id`.

### Impression / view macro usage

- Use GAM's native impression counting as the primary ad-server impression.
- Use third-party impression pixels only when required by the campaign.
- Fire optional third-party impression pixels once when the creative renders or per vendor requirements.
- Do not treat `creative_in_view` as the billable impression unless the commercial agreement explicitly defines it that way.

Example pixel pattern:

```html
<img src="${IMPRESSION_URL_WITH_CACHEBUSTER}" width="1" height="1" style="display:none" alt="" />
```

### Cachebuster macro usage

Use a cachebuster placeholder in third-party trackers:

```text
https://tracker.example/pixel?ord=%%CACHEBUSTER%%
```

If the ad server or tracker uses a different macro syntax, configure it at template level. Do not invent unsupported macros for a given platform.

### Third-party tracker usage

- Allow up to 5 configurable third-party pixels.
- Validate HTTPS.
- Validate cachebuster presence where required.
- Avoid blocking rendering on tracker requests.
- Do not expose user identifiers unless contractually and legally approved.

### Multiple CTA tracking

Each CTA should include:

- CTA ID
- CTA label
- Destination URL
- GAM click tracking prefix
- Optional third-party click tracker
- Creative variant ID

### Deep link / landing page handling

For app or mobile deep links:

- Confirm publisher and SDK allow deep links.
- Provide web fallback URL.
- Ensure click tracking wraps the final URL correctly.
- Avoid automatic deep-link attempts without user click.

### Avoiding invalid click inflation

- Do not make the entire unit clickable on mobile if users are likely to scroll through it.
- Exclude close, mute, pause, replay, and swipe controls from outbound click zones.
- Debounce click handlers.
- Do not fire click events on touchstart; use confirmed click/tap action.
- Do not trigger click from scroll progress or hover.

---

## 10. VAST / Video Handling

Video is optional for the Scroll Activated Ad.

### When VAST is required or relevant

| Scenario | VAST relevance |
|---|---|
| Video is served inside a video player or outstream player | VAST is relevant and may be required. |
| Video is served as an HTML5 `<video>` element inside a display/rich-media creative | VAST may not be required. Track video events manually or through approved measurement library. |
| Inventory is sold as outstream video | VAST compatibility is usually expected. |
| Inventory is sold as display rich media with optional video background | VAST is optional unless publisher/ad server requires it. |
| Video is click-to-play hosted on landing page | VAST not needed inside the display ad. |

### Recommended approach for this format

Default implementation should treat video as an **optional HTML5 video asset inside a rich-media display creative** unless the publisher specifically packages the placement as outstream video inventory.

### Video event tracking expectations

If video is present, track:

- `video_start`
- `video_25`
- `video_50`
- `video_75`
- `video_complete`
- `video_pause`
- `video_mute`
- `video_unmute`
- `video_replay`

If VAST is used, map these to VAST-compatible player events where applicable.

### Muted autoplay and sound rules

- Autoplay must be muted.
- Sound must require explicit user action.
- Video should pause when out of view.
- Provide visible mute/unmute control if audio exists.
- Use `playsinline` on mobile.
- Provide poster and fallback image.

---

## 11. OpenRTB / Programmatic Compatibility

The Scroll Activated Ad should be described carefully in programmatic systems. It is not a universal commodity banner placement, even though it may be technically delivered through display inventory.

### Likely inventory classification

| Context | Recommended classification |
|---|---|
| Standard web delivery through display slot | Banner/display with rich-media creative attributes |
| Publisher-custom in-content placement | Rich media / high-impact display |
| Optional video inside display creative | Display rich media with video asset, unless sold as outstream video |
| Player-based outstream variant | Video/outstream, VAST-compatible if supported |
| Native-like editorial module | May resemble native placement, but classify as native only if it follows native ad object structure and disclosure rules |
| In-app rich media | Banner/rich media with MRAID/OMID support, depending on exchange/SDK |
| Fullscreen forced modal | Not applicable; that would be a different interstitial/takeover format |

### Standard programmatic vs custom PMP / PG

This format is best suited for:

- Direct-sold campaigns
- Programmatic Guaranteed
- Preferred Deals
- Private Marketplace packages
- Curated high-impact inventory
- Publisher-approved rich-media templates

It is less suitable for unmanaged open auction unless the SSP/DSP, publisher, and creative template all support the exact behavior.

### Required metadata for buyers

Recommended buyer-facing metadata:

| Metadata | Example |
|---|---|
| Format name | Scroll Activated Ad / Interscroller Rich Media |
| Placement | In-content, full-width, non-blocking |
| Device support | Desktop, mobile web, app if SDK supports |
| Declared size(s) | 320x480, 300x250, 970x250, 970x500, etc. |
| Active canvas | Responsive, max 80-90vh mobile / 500-700 px desktop |
| Interaction | Scroll-triggered, optional tap/click hotspots |
| Video support | Optional muted HTML5 video or VAST if player-served |
| Audio | User-initiated only |
| Measurement | Active View / OMID / third-party verification where supported |
| SafeFrame/MRAID | Tested status required |
| Publisher approval | Required for live execution |

### Size declaration

Do not misdeclare the unit as only 300x250 if it requires a 970x500 or viewport-height active canvas. The declared size, active canvas, and reserved layout behavior must be aligned with the publisher's ad serving configuration.

### Creative attributes

Exact OpenRTB mapping depends on the SSP/DSP and exchange implementation. Do not invent unsupported OpenRTB fields. Where supported, communicate:

- Rich media behavior
- Expandable or responsive behavior, if applicable
- Video presence, if any
- MRAID requirement for app
- API frameworks supported, such as MRAID / OMID where applicable
- Creative technical attributes and blocked attributes according to the exchange taxonomy
- Landing page and advertiser domain
- Category and brand safety information

### API / MRAID / OMID considerations

| Environment | Consideration |
|---|---|
| Desktop web | SafeFrame and iframe constraints must be tested. |
| Mobile web | Same as web; add viewport/safe-area constraints. |
| In-app | MRAID may be needed for rich-media behavior; OMID recommended for measurement. |
| Video | VAST/SIMID may apply only when using a video player context. |

### Deal packaging recommendations

- Package as premium in-content rich media, not standard remnant display.
- Include screenshots/GIF/video preview in buyer spec.
- Include exact behavior notes: non-blocking, scroll-triggered, no forced interstitial.
- Provide device-specific previews.
- Require publisher allowlist and QA sign-off.
- Use curated deal IDs for controlled activation.

### Why this may require custom setup

This format often requires custom setup because:

- It depends on reserved in-content layout space.
- It may need scroll visibility signals.
- It may use responsive active canvases not captured by a single fixed size.
- SafeFrame or iframe constraints may limit expansion or parent communication.
- Standard open auction buyers may not understand the exact user experience.
- Publisher QA is required to prevent intrusive behavior and performance issues.

---

## 12. Measurement, Viewability & Verification

### Active View / viewability considerations

For display measurement, a common minimum viewability rule is that at least 50% of the ad area is in view for at least one continuous second. For video, a common minimum is at least 50% in view for at least two continuous seconds. Always follow the measurement vendor, GAM, and campaign contract definitions being used.

For this format, the measurement plan must account for the fact that:

- The creative may be partially visible during scroll.
- The active canvas may be taller than a standard banner.
- Users may pass through quickly without reaching the full story.
- Rendered impression, viewable impression, activation, and completion are different events.

### OM SDK / OMID considerations

For app and supported web/video measurement:

- Use OMID-compatible measurement when available.
- Coordinate with verification vendors.
- Confirm the host SDK supports OMID signals.
- Do not assume in-app webview visibility equals OMID viewability.
- Test measurement scripts inside the actual inventory environment.

### Scroll-triggered visibility rules

Recommended internal rules:

| Metric | Suggested definition |
|---|---|
| `creative_in_view` | Placement reaches configured threshold, e.g., 30-50% visible. |
| `scroll_activation_start` | Scroll animation begins after trigger threshold. |
| `active_time` | Time while placement is visible and document/app is active. |
| `story_depth` | Highest scroll progress milestone reached. |
| `interaction_complete` | User reaches final state or completes defined interaction. |

### Recommended KPIs

| KPI | Why it matters |
|---|---|
| Viewability rate | Confirms placement quality. |
| Activation rate | Shows how often users actually reach and trigger the unit. |
| Scroll depth / story depth | Measures narrative exposure. |
| Engagement time / time in unit | Indicates attention quality. |
| Interaction rate | Measures hotspots/cards/swipes/secondary actions. |
| CTR | Measures outbound intent, but should not be the only KPI. |
| CTA click rate | Cleaner than total click rate when controls exist. |
| Close/minimize rate | Detects intrusiveness if close exists. |
| Video start rate | Video exposure if video exists. |
| Video completion rate | Video effectiveness if video exists. |
| Swipe/interaction depth | Useful for mobile storytelling variants. |
| Brand lift suitability | Strong fit for awareness/consideration studies. |
| Attention metrics suitability | Strong fit if measured with approved attention vendors. |

### Verification notes

- Ensure verification pixels are not blocked by lazy-loading logic.
- Confirm third-party scripts do not break inside SafeFrame.
- Avoid duplicate measurement wrappers that slow the unit.
- Validate that scroll-based engagement events are not counted as clicks.
- Align billing, reporting, and optimization events before campaign launch.

---

## 13. Accessibility & User Control

### Keyboard accessibility

Where keyboard interaction applies:

- CTA, close, mute, pause, replay, hotspots, and cards must be focusable.
- Use visible focus states.
- Preserve logical tab order.
- Avoid keyboard traps.
- Escape key may close/minimize only if the unit has an overlay/pinned state.

### ARIA labels

Recommended labels:

| Control | Example ARIA label |
|---|---|
| Close/minimize | `aria-label="Close advertisement"` |
| Mute | `aria-label="Mute ad video"` |
| Unmute | `aria-label="Unmute ad video"` |
| Pause | `aria-label="Pause ad animation"` |
| Replay | `aria-label="Replay ad animation"` |
| Hotspot | `aria-label="View feature details"` |
| CTA | Use visible CTA text or explicit label |

### Visible close button

Required only when the unit overlays, pins, or expands beyond its reserved in-flow area. If included, it must be visible, tappable, and separate from the CTA.

### Tap target minimum guidance

- Minimum: 44x44 CSS px for touch controls.
- Preferred: 48x48 CSS px on mobile.
- Keep controls spaced to prevent mis-taps.

### Reduced motion

When `prefers-reduced-motion: reduce` is detected:

- Replace parallax with static reveal or fade.
- Disable rapid movement and auto-looping motion.
- Keep CTA and message available.
- Do not force a blank fallback.

### Pause / stop controls

Provide pause/stop controls when:

- Video plays.
- Animation loops longer than a few seconds.
- Motion is intense or continuous.
- The creative contains frame sequences or moving backgrounds.

### Sound control

- No forced sound.
- No sound on scroll trigger.
- Sound only after explicit tap/click.
- Show clear mute/unmute state.

### Clear CTA labeling

Use action-specific CTA labels such as:

- `Explore the model`
- `View offer`
- `Plan your trip`
- `Watch trailer`
- `Compare features`

Avoid vague or misleading labels such as:

- `Continue`
- `Next` if it looks like publisher navigation
- Fake system-style buttons

---

## 14. Performance & Loading Strategy

### Initial load strategy

Initial load should include only:

- Minimal HTML/CSS/JS shell
- Fallback/poster image
- Basic logo/CTA if required
- Measurement bootstrap if required
- No heavy video or large frame sequences

### Subload / lazy-load strategy

Use staged loading:

| Stage | Trigger | Assets loaded |
|---|---|---|
| Stage 0: Render shell | Ad response rendered | HTML/CSS/minimal JS/fallback image |
| Stage 1: Preload | Unit within 1-2 viewport heights | Mobile/desktop background, logo, key overlays |
| Stage 2: Activate | Unit reaches threshold | Animation modules, first interactive assets |
| Stage 3: Deep interaction | User reaches deeper story or taps | Product tiles, additional panels, video |
| Stage 4: Fallback | Error/unsupported/low bandwidth | Static image + CTA |

### Image optimization

- Generate mobile, tablet, and desktop crops.
- Use modern formats with fallbacks.
- Avoid oversized desktop assets on mobile.
- Use compression targets per asset role.
- Preload only the first critical image.

### Video lazy loading

- Do not preload full video on page load.
- Use `preload="metadata"` or `none` depending on publisher policy.
- Load only when near viewport or when user expresses intent.
- Pause when out of view.
- Avoid multiple simultaneous videos in repeated feed placements.

### Font loading

- Prefer system fonts for performance.
- If brand font is required, subset it.
- Use `font-display: swap` where allowed.
- Avoid loading multiple weights.

### Animation performance

- Use `requestAnimationFrame` for scroll progress updates.
- Throttle or debounce expensive calculations.
- Use CSS transforms and opacity.
- Avoid layout thrashing.
- Avoid large DOM trees for simple animation.

### GPU-friendly transforms

Preferred:

```css
.layer {
  transform: translate3d(0, var(--scroll-y), 0);
  opacity: var(--layer-opacity);
}
```

Avoid continuous animation of:

- `height`
- `width`
- `top`
- `left`
- `margin`
- `padding`
- complex filters

### Avoiding layout shift

- Reserve slot height in publisher CSS.
- Define min-height and max-height.
- Avoid injecting active canvas height after load without reserved space.
- For multi-size slots, reserve largest eligible height or use responsive placeholder logic.

### Low-bandwidth fallback

If bandwidth, device memory, or performance conditions are constrained:

- Use static fallback image.
- Disable video.
- Disable heavy parallax.
- Use fewer layers.
- Prioritize CTA and core message.

### Unsupported environment fallback

Fallback should activate when:

- SafeFrame blocks required behavior.
- MRAID unavailable in app.
- IntersectionObserver unsupported.
- Video autoplay unavailable.
- Third-party scripts fail.
- Browser is too old.

Fallback should still include:

- Brand/logo
- Core visual
- Headline
- CTA with click tracking
- Impression tracking

---

## 15. QA Checklist

### Creative rendering QA

- [ ] Creative renders in all declared sizes.
- [ ] Fallback image renders when JS is disabled.
- [ ] No clipped text, logos, CTAs, or legal copy.
- [ ] Mobile and desktop crops use correct focal points.
- [ ] CTA remains visible and readable.
- [ ] Ad disclosure/label appears if required by publisher.
- [ ] Creative does not visually mimic publisher navigation or system UI.

### Interaction QA

- [ ] Scroll activation starts only when threshold is met.
- [ ] User can scroll past the unit without obstruction.
- [ ] No body scroll lock occurs.
- [ ] Scroll progress animation is smooth.
- [ ] Hotspots/cards/swipes work where enabled.
- [ ] Close/minimize works where enabled.
- [ ] Close does not trigger outbound click.
- [ ] Replay does not double-count activation events.
- [ ] Accidental clicks during scroll are minimized.

### Tracking QA

- [ ] `creative_loaded` fires once.
- [ ] GAM impression is counted.
- [ ] Third-party impression pixels fire once with cachebuster.
- [ ] `creative_in_view` fires at correct threshold.
- [ ] `scroll_activation_start` fires once per configured policy.
- [ ] CTA click routes through GAM click macro.
- [ ] Multiple CTAs track separately.
- [ ] Video events fire only when video exists.
- [ ] Close/mute/pause events do not count as ad clicks.
- [ ] Tracking still works inside SafeFrame or approved fallback mode.

### GAM trafficking QA

- [ ] Correct creative type selected.
- [ ] Custom creative template variables populated.
- [ ] Declared sizes match line item and ad unit eligibility.
- [ ] Multi-size mapping tested.
- [ ] Click-through URL and click macro verified.
- [ ] Third-party trackers validated.
- [ ] Cachebuster macro present where required.
- [ ] SafeFrame setting tested on/off according to publisher policy.
- [ ] Preview works in GAM creative preview.
- [ ] Preview works on publisher staging page.

### Mobile QA

- [ ] Works on iOS Safari.
- [ ] Works on Android Chrome.
- [ ] No horizontal overflow.
- [ ] Safe-area insets respected.
- [ ] CTA and controls are at least 44x44 CSS px.
- [ ] Video uses muted autoplay and `playsinline`.
- [ ] Unit pauses video/motion when out of view.
- [ ] No scroll jank on mid-range devices.

### Desktop QA

- [ ] Works on Chrome, Edge, Safari, Firefox where required.
- [ ] Layout works at 1024, 1280, 1366, 1440, and 1920 widths.
- [ ] Wide background does not misplace key content.
- [ ] Parallax does not produce visible tearing or jank.
- [ ] Keyboard focus works for controls.

### App QA

- [ ] Tested in target ad SDK.
- [ ] MRAID state detected correctly if used.
- [ ] OMID measurement works if required.
- [ ] In-app click-out/deep-link behavior verified.
- [ ] App safe area and nav bars respected.
- [ ] SDK does not block required video or interaction behavior.
- [ ] Fallback works if MRAID APIs are unavailable.

### Performance QA

- [ ] Initial load stays within publisher weight limits.
- [ ] Heavy assets lazy-load only near viewport.
- [ ] No long main-thread blocking tasks during scroll.
- [ ] No large layout shifts.
- [ ] Video is compressed and lazy-loaded.
- [ ] Frame sequences are optimized or avoided.
- [ ] Tracker requests do not block rendering.

### Accessibility QA

- [ ] Interactive elements have accessible labels.
- [ ] Keyboard users can reach controls where applicable.
- [ ] No keyboard traps.
- [ ] Reduced-motion mode works.
- [ ] Text contrast is acceptable.
- [ ] No rapid flashing/strobing.
- [ ] Motion/video can be paused where needed.

### Publisher safety QA

- [ ] Does not cover navigation or editorial content unexpectedly.
- [ ] Does not force interstitial-like behavior.
- [ ] Does not break article layout.
- [ ] Does not conflict with sticky headers/footers.
- [ ] Does not degrade Core Web Vitals materially.
- [ ] Does not access parent DOM without approved API.
- [ ] Brand/category approvals completed.
- [ ] Publisher has signed off on screenshots and staging preview.

---

## 16. Common Failure Cases

| Failure case | Likely cause | Practical fix |
|---|---|---|
| Creative clipped inside iframe | Active canvas larger than declared iframe size | Declare correct active size, use responsive slot, SafeFrame expansion API, or keep animation inside iframe. |
| Expansion blocked by SafeFrame | Creative requires parent-page access or unsupported expansion | Build SafeFrame-aware behavior, use approved APIs, or use publisher custom integration. |
| Click tracking not firing | CTA bypasses GAM macro or JS redirect overrides link | Wrap all outbound URLs with GAM click macro and test in preview. |
| Close button hidden | Z-index conflict, safe-area issue, or animation layer covers control | Put controls in top UI layer, add safe-area padding, test across breakpoints. |
| Autoplay blocked | Video not muted, missing `playsinline`, browser policy | Start muted, add `playsinline`, show poster and play button fallback. |
| Audio starts unexpectedly | Video has audio enabled on activation | Force muted initial state and require user click to unmute. |
| Mobile viewport overflow | Fixed desktop width or oversized layer | Use responsive CSS, max-width: 100%, mobile crops, and overflow testing. |
| Scroll jank | Heavy scroll listener, large images, frame sequences, layout animations | Use IntersectionObserver, requestAnimationFrame, transforms, lazy assets, and reduce layers. |
| Video too heavy | Full video loads on page render | Use poster first, lazy-load video near viewport, compress and provide mobile variant. |
| Third-party pixels cached | Missing cachebuster | Add GAM cachebuster macro or approved random value. |
| Wrong size declared in GAM | Trafficker uses fallback size for immersive creative | Define approved size mapping and ensure line item/ad unit eligibility matches creative. |
| In-app SDK does not support required interaction | MRAID/OMID/resize/expand unsupported or disabled | Use static fallback, SDK-specific build, or limit app compatibility. |
| Viewability appears low | Active canvas too tall or user scrolls quickly | Optimize placement, trigger earlier, improve first frame, analyze scroll depth separately. |
| Accidental click rate high | Full-unit click overlay captures scroll gestures | Limit clickable zones to CTA/hotspots; ignore touchmove gestures. |
| Layout shift on load | No reserved height or late injection | Reserve container height before ad loads; use fixed min-height. |
| Animation restarts repeatedly | Re-entry logic fires activation every time | Store state per impression and allow replay only by user action. |
| Reduced-motion users still see parallax | CSS/JS ignores `prefers-reduced-motion` | Add reduced-motion branch and static reveal fallback. |
| Tracking double-counts engagement | Scroll milestones fire repeatedly | Gate milestone events once per impression or per session policy. |

---

## 17. Recommended Use Cases

| Industry | Campaign goal | Why this format fits | Example creative concept |
|---|---|---|---|
| Auto | Product launch / feature education | Scroll reveal can show exterior, interior, safety, and performance features without forcing a video. | A car emerges as the user scrolls; hotspots reveal ADAS, mileage, infotainment, and launch offer. |
| BFSI | Product education / lead consideration | Allows staged explanation of credit card, loan, insurance, or investment benefits in a controlled flow. | Scroll through three benefit panels: eligibility, rewards, and calculator CTA. |
| FMCG | Awareness / sensory storytelling | Motion and layered visuals can reveal pack, ingredients, flavors, or occasion. | Product pack appears through ingredient layers with final “Try the new flavour” CTA. |
| Retail | Seasonal sale / offer reveal | Strong for offer buildup and category-specific CTAs. | Scroll reveals sale tiers: fashion, electronics, home, with final sale CTA. |
| Entertainment | Trailer teaser / release awareness | Can use muted video, poster reveal, countdown, and character panels. | Movie poster splits into character panels as user scrolls; final “Watch trailer” CTA. |
| Real Estate | Project walkthrough / lead generation | Full-width space supports property visuals and amenity storytelling. | Scroll from facade to clubhouse to apartment view with “Book site visit” CTA. |
| Travel | Destination inspiration / package discovery | Parallax and scenic reveals match travel browsing behavior. | Destination landscape opens with flight/hotel/package cards revealed by scroll. |
| Tech | Feature storytelling / product launch | Ideal for device reveal, software feature sequence, or spec education. | Phone rotates subtly while scroll reveals camera, battery, AI feature, and pre-order CTA. |
| QSR | Menu launch / offer discovery | Can show food assembly, limited-time offer, and store/app CTA. | Burger builds layer by layer as user scrolls; final “Order now” CTA. |
| Consumer Durables | Product demo / comparison | Supports feature reveal for appliances, TVs, ACs, and electronics. | AC airflow animation reveals energy rating, cooling speed, warranty, and dealer CTA. |

---

## 18. Final Trafficker / Developer Handoff Summary

| Handoff area | Required items |
|---|---|
| Required assets | Fallback image, mobile/desktop background, logo, CTA text, landing URL, optional overlays/hotspots/cards, optional video + poster. |
| Required dimensions | At minimum one declared GAM size and one fallback. Recommended support: 300x250, 320x50, 320x480, 728x90, 970x90, 970x250, 970x500, plus responsive active canvas rules. |
| Required GAM variables | `creative_variant_id`, `click_url`, `cta_text`, `cta_url`, `backup_image_url`, `scroll_trigger_threshold`, `animation_mode`, `reduced_motion_fallback`, optional video/tracking variables. |
| Required tracking events | `creative_loaded`, `impression_rendered`, `viewable_impression`, `creative_in_view`, `scroll_activation_start`, `cta_click`, `click`, `time_in_unit`, optional scroll progress and video events. |
| Required QA checks | Rendering, scroll behavior, click tracking, SafeFrame, mobile viewport, performance, accessibility, publisher safety, GAM preview, staging page. |
| Publisher-side requirements | Approved in-content placement, reserved layout height, size mapping, SafeFrame policy, tracker approval, category/brand approval, staging page test. |
| Known limitations | May require custom template or direct integration; open auction compatibility varies; SafeFrame/MRAID constraints may limit behavior; heavy video/frame sequences can hurt performance; not a forced interstitial. |

---

## Recommended Ad-Builder / Editor Schema Fields

For future automation across 10+ formats, represent this format as a modular schema rather than one-off creative code.

```json
{
  "format_id": "scroll_activated_ad",
  "format_name": "Scroll Activated Ad",
  "classification": ["display", "rich_media", "in_content", "scroll_triggered", "immersive"],
  "is_official_iab_standard": false,
  "placement": "in-content-full-width-interscroller",
  "supported_devices": ["desktop", "mobile_web", "app"],
  "declared_sizes": [[300,250], [320,50], [320,480], [728,90], [970,90], [970,250], [970,500]],
  "responsive_canvas": {
    "mobile": { "width": "100vw", "height": "70-90vh", "max_height": "100svh" },
    "desktop": { "width": "100%", "height": "500-700px", "max_height": "85vh" }
  },
  "activation": {
    "type": "scroll_visibility",
    "default_threshold": 0.5,
    "preload_margin": "150vh",
    "retrigger_policy": "once_per_impression"
  },
  "motion": {
    "modes": ["parallax", "static_reveal", "layered_reveal", "story_panels"],
    "reduced_motion_required": true
  },
  "video": {
    "supported": true,
    "default_enabled": false,
    "autoplay": "muted_only",
    "playsinline_required": true,
    "vast_required": false
  },
  "controls": {
    "close_button_default": false,
    "pause_control_required_for_looping_motion": true,
    "mute_control_required_if_audio_exists": true
  },
  "tracking_events": [
    "creative_loaded",
    "impression_rendered",
    "viewable_impression",
    "creative_in_view",
    "scroll_activation_start",
    "cta_click",
    "click",
    "time_in_unit",
    "interaction_complete"
  ],
  "publisher_approval_required": true,
  "fallback_required": true
}
```

---

## Final Notes

The Scroll Activated Ad should be sold, designed, trafficked, and QA-tested as a **premium in-content rich-media display experience**. Its value comes from scroll-native storytelling, not from interruption. The production benchmark is simple: it should feel like a polished editorial module sponsored by a brand, while remaining technically compatible with GAM trafficking, publisher page safety, measurement vendors, and future ad-builder automation.
