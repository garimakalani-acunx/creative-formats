# RollExplore Cube — Generalized Ad Specification

**Format Name:** RollExplore Cube  
**Placement:** Display / rich-media slot, usable in-banner or in-content  
**Compatibility:** Desktop / Mobile Web / Mobile App  
**Primary Interaction:** 3D cube rotation, swipe, drag, face exploration, face-level CTA click  
**Document Type:** Production-ready technical + creative specification for rich-media ad delivery, creative development, GAM trafficking, QA, and future ad-builder automation  
**Version:** 1.0  
**Prepared For:** AcunX Showcase Web Page / AcunX rich-media format library

---

## 0. Implementation Assumptions

The RollExplore Cube is treated as a **custom interactive 3D rich-media display format**, not as an official fixed IAB standard ad unit. It should be implemented using IAB-compatible HTML5, lightweight creative, viewability, verification, click-tracking, and ad-serving practices.

This document assumes:

| Area | Assumption |
|---|---|
| Ad serving | Google Ad Manager or equivalent ad server capable of custom HTML5 / rich-media creative delivery. |
| Runtime | HTML5, CSS3 3D transforms, JavaScript interaction controller, optional video per face. |
| Inventory | Standard display slot, high-impact rich-media slot, in-content slot, or curated direct/PMP placement. |
| Rendering | Mostly iframe-rendered; SafeFrame should be tested because 3D transforms, touch interactions, and expansion-like behavior may behave differently across containers. |
| Measurement | Standard impression/click tracking plus custom interaction tracking for face views, rotations, drags, and CTA clicks. |
| Mobile app | Requires MRAID-compatible or SDK-compatible rendering where applicable; OM SDK/OMID should be used for supported in-app measurement. |
| Video | Optional. VAST is only required if the video is served into a video player or outstream/player-based inventory. HTML5 video inside the cube can be tracked without VAST, subject to buyer/publisher requirements. |
| Fallback | Mandatory fallback to flat carousel, static multi-frame creative, or backup image when 3D transforms, device performance, SafeFrame permissions, or app SDK capabilities are insufficient. |

---

## 1. Format Overview

The **RollExplore Cube** is an interactive rich-media ad format that presents brand messaging across the faces of a rotating 3D cube. Each face acts as a modular creative panel: it can show a product, feature, offer, story step, video teaser, image, price point, CTA, or lead-in message. Users can either watch an autoplay rotation or actively explore the cube through swipe, drag, arrow controls, or face navigation dots.

Unlike a static banner, the cube creates a sense of physical interaction inside a standard ad slot. The value comes from allowing multiple messages inside one compact unit without immediately expanding into a page-level takeover.

### 1.1 Core Purpose

The format is designed to:

- Increase interaction depth within standard display inventory.
- Show multiple brand messages without relying on a long copy-heavy banner.
- Encourage curiosity-led engagement through rotation, swipe, and face discovery.
- Package product storytelling, feature exploration, offer comparison, or campaign sequencing into a single unit.
- Provide measurable interaction signals beyond CTR, including face views, drag interactions, time in unit, and face-level CTA engagement.

### 1.2 Best Use Cases

| Use case | Why the cube fits |
|---|---|
| Multi-product showcase | Each cube face can represent a different SKU, model, plan, or offer. |
| Feature education | Each face can explain one product feature with visual emphasis. |
| Entertainment launch | Poster, trailer teaser, character reveal, ticketing CTA, and social CTA can be separated by face. |
| Automotive model highlight | Exterior, interior, performance, safety, finance offer, and booking CTA can be mapped to cube faces. |
| BFSI product comparison | Credit card benefits, loan offer, insurance coverage, eligibility, and apply CTA can be split cleanly. |
| Retail sale campaign | Each face can reveal a discount category or limited-time deal. |
| Tech product launch | Hardware, ecosystem, AI feature, performance, price, and preorder CTA can be presented as an exploratory object. |

### 1.3 Brand Value

The format gives brands a compact but high-attention canvas. It is useful where a single banner cannot explain the full proposition, but a full takeover would be too intrusive. Because each face can be independently tracked, advertisers can learn which message, product, or offer attracts the most exploration.

### 1.4 Publisher Value

For publishers, the RollExplore Cube can command higher value than a standard static display unit while still occupying familiar ad slots such as 300x250, 300x600, 728x90, or 970x250. It can be packaged as a premium rich-media execution for direct-sold, sponsorship, programmatic guaranteed, or private marketplace campaigns.

Publisher benefits include:

- Premium interactive inventory without necessarily blocking page content.
- Compatibility with familiar display placements when engineered correctly.
- Higher engagement potential than static banners.
- Stronger storytelling for advertiser campaigns.
- Optional integration into showcase pages, sponsored content modules, or vertical-specific packages.

### 1.5 User Experience Value

The user gets a voluntary exploration experience. The ad should feel like a small interactive object, not a forced interruption. A good cube ad is understandable within one second, controllable with simple gestures, and never traps the user.

The user should be able to:

- Understand that the object rotates or can be swiped.
- Pause or reduce motion where needed.
- Navigate faces without precision gestures.
- Click a clear CTA without accidental click capture.
- Ignore the ad and continue consuming content.

### 1.6 Classification

| Classification dimension | Recommended classification |
|---|---|
| Primary type | Display / rich media |
| IAB status | Custom rich-media format; not an official fixed IAB standard format |
| Creative technology | HTML5, CSS3 3D transforms, JavaScript |
| Inventory style | Standard display, rich-media display, in-content, high-impact in-page |
| Interaction style | Interactive / exploratory / swipe or drag-enabled |
| Expandable? | Usually no. It can fit within a fixed slot. Any expanded variant requires separate publisher approval. |
| Interstitial? | No. It is not a forced interstitial or page-blocking takeover. |
| Sticky? | Not by default. Sticky use requires separate placement classification and publisher approval. |
| Immersive? | Yes, in the sense of interactive visual depth, not full-screen immersion by default. |
| Video-led? | Optional. The core format is not video-led, but each face may contain short video or animated media. |
| Gamified? | Optional. Exploration can feel game-like, but it is not a game unless additional mechanics are added. |

---

## 2. Standard Ad Dimensions & States

The RollExplore Cube can run in standard display sizes when the cube is designed to fit safely inside the slot. Because 3D rotation can visually extend beyond the cube's front face, all creative builds must include internal padding and clipping tests.

### 2.1 Size and State Matrix

| State / Variant | Recommended collapsed size | Recommended active / interaction size | Device | Common placement | Notes |
|---|---:|---:|---|---|---|
| Standard medium cube | 300x250 | 300x250 | Desktop / Mobile Web / App | MPU, in-content, sidebar, article rail | Best default. Cube should occupy 180-230px square with CTA below or on face. Keep 12-16px internal safe area. |
| Mobile banner teaser cube | 320x50 | 320x50 or tap-to-open 320x250 only if approved | Mobile Web / App | Mobile inline banner | Only use simplified cube or mini-rotation. Avoid dense copy. Consider flat fallback. Expanded behavior requires explicit approval. |
| Mobile rectangle cube | 320x480 | 320x480 | Mobile Web / App | In-content mobile rich-media unit | Strong for vertical storytelling. Cube can be 260-300px square with face details below. Respect safe areas and browser chrome. |
| Half-page cube | 300x600 | 300x600 | Desktop / Tablet | Sidebar / high-impact rail | Good for product exploration. Use cube in upper 300x300 or mid-zone with face details stacked below. |
| Leaderboard cube | 728x90 | 728x90 | Desktop / Tablet | Top / mid-article leaderboard | Use shallow horizontal 3D roll, not a full square cube. Better as rotating panels or 3D card strip. CTA must stay readable. |
| Billboard cube | 970x250 | 970x250 | Desktop | Premium header / in-content billboard | Recommended premium desktop execution. Cube can sit left or center with face-specific copy and CTA on the side. |
| Super leaderboard | 970x90 | 970x90 | Desktop | Header / below nav | Use subtle 3D roll. Avoid large cube depth because height is limited. Strong fallback needed. |
| Large canvas variant | 970x500 | 970x500 | Desktop | In-content premium / sponsorship | Can support larger cube, product stage, sequential storytelling, or multiple interaction zones. Requires publisher approval and performance budget. |
| Mobile fullscreen optional | 100vw x 100vh | 100vw x 100vh | Mobile Web / App | User-initiated expanded experience only | Not the default. Must be user-initiated, dismissible, frequency-capped, and approved as an expanded rich-media or interstitial-like experience. |
| Desktop fullscreen optional | 100vw x 100vh | 100vw x 100vh | Desktop | User-initiated expanded experience only | Not recommended for standard display. Treat as high-impact expandable/takeover with separate trafficking, QA, and approval. |
| Responsive in-content cube | Slot-defined, e.g. 100% width x 250-500px | Same as slot | Desktop / Mobile Web | Responsive article module | Use aspect-ratio rules and GPT size mapping. Reserve height to prevent layout shift. |
| App in-feed cube | SDK slot-defined | Same as slot | Mobile App | Native-like in-feed display slot | Requires app SDK capability testing, OMID integration where applicable, and fallback to static/card carousel. |

### 2.2 Recommended Cube Face Count

| Cube model | Face count | Use case | Notes |
|---|---:|---|---|
| 4-face horizontal cube | 4 | Most display units | Recommended default. Rotates around Y-axis. Easy for users to understand and for tracking. |
| 6-face true cube | 6 | Premium desktop / large mobile rectangle | Supports top/bottom faces but can be harder to read. Requires stronger engineering and QA. |
| 3D roll / prism | 3-4 | Leaderboard / 970x250 / 728x90 | Better for shallow horizontal formats where a true cube is too tall. |
| Flat fallback carousel | 3-6 cards | Unsupported environments | Should preserve the same content order and tracking taxonomy. |

### 2.3 Safe-Area Considerations by Size

| Size | Safe-area guidance |
|---|---|
| 300x250 | Keep cube max 230x230 if CTA/copy exists outside cube. Keep rotating depth inside a clipped wrapper. Minimum 8-12px visual padding. |
| 300x600 | Reserve 24-40px for brand/CTA zones. Avoid placing CTA only on the side faces because they may rotate out of visibility. |
| 320x50 | Avoid true cube interaction unless highly simplified. Use a 3D flip strip, text roll, or teaser state. Text should remain readable at 320px width. |
| 320x480 | Respect mobile notch/browser UI and app safe areas. Main CTA should be reachable in lower-middle zone but not too close to bottom gesture area. |
| 728x90 | Keep type large and motion shallow. Prefer one CTA outside the rotating area. Face content must not rely on small text. |
| 970x90 | Same as 728x90, with more horizontal storytelling. Avoid tall cube geometry. |
| 970x250 | Best desktop showcase size. Allow cube plus copy panel. Maintain 20-30px margins. |
| 970x500 | Treat as premium canvas. Add navigation affordances, pause/replay, and reduce motion option. |
| Fullscreen variants | Must use mobile and desktop safe area insets. Close button must be fixed, visible, and keyboard/touch accessible. |
| Responsive | Use CSS `aspect-ratio`, max-width, and max-height rules. Reserve slot height before creative load to prevent content jump. |

### 2.4 State Model

| State | Description | Required? | Notes |
|---|---|---|---|
| Loading state | Lightweight placeholder or poster displayed while assets initialize. | Required | Must not show broken faces or empty cube. |
| Initial face | First visible face on render. | Required | Should carry the strongest message and clear interaction cue. |
| Autoplay rotation | Optional timed rotation between faces. | Optional | Must be smooth, muted if video exists, and pause on interaction or reduced-motion preference. |
| Active face | Current face presented to the user after rotation/drag/navigation. | Required | Used for face_view and CTA mapping. |
| User drag/swipe | Gesture-driven rotation. | Recommended | Primary mobile interaction. Must avoid scroll conflict. |
| Face CTA click | Click/tap on face CTA or entire face click zone. | Recommended | Should map to face-specific landing page where applicable. |
| Fallback flat carousel | 2D card carousel or static layout. | Required | Used for unsupported CSS 3D, low-end devices, SafeFrame/app restrictions. |
| Backup image | Static image served when interactive creative fails. | Required | Must include logo, message, CTA, and click-through. |

---

## 3. User Experience & Behaviour Specification

### 3.1 Initial State

The initial state should present a stable front face with:

- Brand logo.
- Clear hero message.
- One visual subject.
- Interaction cue such as "Swipe to explore", "Drag to rotate", "Explore offers", or arrow/dot navigation.
- CTA visible either on the face or in a persistent CTA zone.

The cube should not begin with aggressive motion that makes the message unreadable. If autoplay is enabled, delay the first rotation briefly so the initial face can register.

Recommended timing:

| Element | Recommendation |
|---|---|
| Initial readable hold | 1.0-2.0 seconds before first autoplay rotation |
| Rotation duration | 500-900 ms per quarter turn |
| Autoplay interval | 2.5-5.0 seconds between face changes |
| Interaction takeover | Immediately pause autoplay when user swipes, drags, hovers, focuses, or taps navigation |
| Reduced motion | Disable autoplay rotation and use fade/flat card navigation |

### 3.2 Trigger Condition

The RollExplore Cube may initialize based on one of the following trigger models:

| Trigger model | Recommended usage | Notes |
|---|---|---|
| Render on impression | Standard display delivery | Loads initial lightweight assets when creative renders. |
| Start animation on view | Preferred | Begin autoplay only when the unit is sufficiently in view. Use IntersectionObserver where allowed. |
| User-initiated rotation | Most UX-safe | Cube only rotates after swipe, drag, arrow click, dot click, or hover. |
| Delayed autoplay | Acceptable | Start after a short delay and only when viewable. Must pause after limited cycles. |
| Tap-to-explore | Mobile-friendly | User taps a cue, then rotation controls activate. |

The format should **not** require the user to interact before leaving the ad area. It must not block content or trap scrolling.

### 3.3 Animation / Transition

The animation should use CSS transforms rather than layout-changing properties. The cube should rotate using GPU-friendly properties such as:

- `transform: rotateY(...) translateZ(...)`
- `transform: rotateX(...)` only where needed.
- `opacity` for supporting fades.
- `will-change: transform` sparingly and only while animating.
- `backface-visibility: hidden` on faces.
- `transform-style: preserve-3d` on the cube wrapper.
- `perspective` on the scene wrapper.

Avoid animating:

- `width`
- `height`
- `top`
- `left`
- `margin`
- `padding`
- `box-shadow` intensity
- heavy filters / blur
- large background-position changes

### 3.4 Interaction Model

| Interaction | Desktop | Mobile Web | App |
|---|---|---|---|
| Autoplay rotation | Optional, limited cycles | Optional, conservative | Optional, only after SDK testing |
| Hover pause | Recommended | Not applicable | Not applicable |
| Drag rotation | Mouse drag | Touch drag / swipe | SDK touch gesture support required |
| Arrow controls | Recommended | Optional but useful | Recommended if drag conflicts with app gestures |
| Dot indicators | Recommended | Recommended | Recommended |
| Keyboard navigation | Required where focusable | Required where possible | App accessibility equivalent required |
| Face CTA click | Required | Required | Required |
| Pause / resume | Recommended if autoplay | Recommended if autoplay | Recommended if autoplay |

### 3.5 Expanded / Active State

This format is usually **active within its slot**, not expanded outside the slot. The active state means the cube has initialized and can rotate, not that it has taken over the page.

Active state includes:

- Current face clearly visible.
- Navigation affordances visible or discoverable.
- CTA state mapped to current face.
- Autoplay paused on user interaction.
- Face content accessible to screen readers if controls are focusable.
- Tracking state updated when a face becomes active.

If an expanded version exists, it must be treated as a separate expandable rich-media variant with:

- User-initiated expansion.
- Obvious close control.
- Publisher approval.
- Frequency capping.
- Additional GAM sizes/creative template logic.
- SafeFrame testing.
- Mobile viewport testing.

### 3.6 Close / Collapse Behaviour

For in-slot cube execution, a close button is generally **not required** unless the publisher requires dismissible rich media. If close/dismiss is provided:

- It should collapse the cube to a static backup image or hide the interactive layer while preserving the slot.
- It must not remove reserved page space in a way that creates layout shift.
- It must be 24x24 CSS px minimum; 44x44 CSS px is preferred for touch.
- It must have an accessible label such as `aria-label="Close ad"`.
- It should be placed consistently in the top-right corner within the ad safe area.

### 3.7 Re-entry Behaviour

| Scenario | Expected behavior |
|---|---|
| User scrolls away and returns | Keep last active face, or reset to initial face based on campaign setting. |
| User interacted once | Do not resume autoplay aggressively. Keep user-controlled mode. |
| User closed/dismissed | Do not reopen in the same page view. Respect session/frequency settings. |
| User clicked CTA | Preserve click tracking and navigate normally. Do not fire duplicate click events. |
| Page refresh/new page view | Follow configured frequency cap and initial state logic. |

### 3.8 Mobile Behaviour

Mobile execution must prioritize scroll compatibility. The cube should not accidentally hijack page scroll.

Recommendations:

- Use horizontal swipe for cube rotation and allow vertical page scroll to pass through.
- Use a drag threshold before preventing default gestures.
- Only capture horizontal gestures when horizontal movement clearly exceeds vertical movement.
- Avoid multi-touch requirements.
- Use `pointerdown`, `pointermove`, and `pointerup` where supported, with fallback to touch events.
- Add dot navigation for users who do not discover swipe.
- Keep CTA tap targets large and separated from swipe zones.
- Avoid continuous 3D autoplay on low-end mobile devices.
- Degrade to flat carousel when frame rate is poor.

Suggested gesture thresholds:

| Parameter | Suggested value |
|---|---:|
| Minimum drag before rotation starts | 8-12 px |
| Swipe completion threshold | 25-35% of cube width, or velocity-based equivalent |
| Max accidental vertical scroll tolerance | If vertical movement exceeds horizontal by 1.2x, do not capture gesture |
| Rotation snap duration | 250-500 ms |
| Tap vs drag separation | Treat as click only if movement stays below 6-8 px |

### 3.9 Desktop Behaviour

Desktop can support richer behavior because mouse hover, drag, and larger slots are available.

Recommended desktop behaviors:

- Pause autoplay on hover.
- Enable mouse drag to rotate.
- Provide left/right arrows or dot controls.
- Keep CTA clickable without requiring drag.
- Support keyboard focus and arrow key navigation when the ad is focused.
- Avoid excessive 3D depth in short formats like 728x90 and 970x90.
- Test in iframe and SafeFrame environments.

### 3.10 App Behaviour

In-app behavior depends on the mobile ad SDK and container capabilities.

Requirements:

- Confirm whether HTML5 creative supports CSS 3D transforms in the SDK webview.
- Confirm whether MRAID APIs are available if expand/resize/storePicture/calendar features are needed.
- Use OM SDK/OMID for measurement where supported by the SDK and publisher integration.
- Avoid gestures that conflict with app-level swipe navigation.
- Include static or flat-carousel fallback for SDKs that flatten 3D transforms or block required scripting.
- Test iOS and Android separately, including low-end Android devices.

### 3.11 Accessibility Expectations

The cube must remain usable for people who cannot or do not want to perform drag gestures.

Minimum accessibility expectations:

- Keyboard-operable navigation controls.
- Screen-reader labels for controls.
- Face indicators such as "Face 2 of 4".
- Pause control for autoplay.
- `prefers-reduced-motion` handling.
- Clear focus states.
- CTA label that describes action, not just "Click here".
- Avoid conveying essential meaning through motion alone.

### 3.12 Interaction Classification

| Attribute | Recommended value |
|---|---|
| User-initiated | Partially. Exploration and click actions should be user-initiated. Autoplay rotation may be enabled conservatively. |
| Scroll-triggered | Not core. Animation may start only when in view, but scroll should not be the primary interaction. |
| Auto-started but muted | Applicable only for autoplay animation/video. Any video must autoplay muted. |
| Time-bound | Autoplay should be limited to a small number of cycles. |
| Dismissible | Optional for in-slot. Required for expanded/fullscreen variants. |
| Frequency-capped | Recommended for autoplay-heavy, expanded, or high-impact placements. |
| Non-blocking | Required. Must not block page content or navigation. |
| Sticky / persistent | Not default. Requires separate classification and approval. |
| Full-screen / takeover | Not default. Only as a separate user-initiated, dismissible variant. |

---

## 4. Creative Design Guidelines

### 4.1 Layout Hierarchy

Each cube face must communicate quickly. The user may only see a face for a few seconds, so content should be modular and concise.

Recommended hierarchy per face:

1. Primary visual or product image.
2. Short headline.
3. Supporting value prop or price/offer, if needed.
4. CTA.
5. Brand logo or persistent brand zone.

For small sizes, prioritize visual + headline + CTA. Do not overload faces with paragraph copy.

### 4.2 Designing Each Cube Face

Each face should work as both:

- A standalone mini-ad.
- A sequence element inside the cube story.

| Face type | Purpose | Design guidance |
|---|---|---|
| Face 1: Hero / hook | First impression | Strongest visual, broadest message, clear interaction cue. |
| Face 2: Feature / benefit | Education | One feature, one proof point, minimal text. |
| Face 3: Offer / product | Conversion | Price, promo, product tile, or limited-time offer. |
| Face 4: CTA / next step | Action | Book, shop, apply, watch, explore, download, or learn more. |
| Face 5/6: Optional depth | Advanced storytelling | Only for larger sizes. Use for testimonials, variants, stores, comparison, or final reminder. |

Important: the current active face should never depend on partially visible side faces for meaning. Side faces may tease visual depth, but essential content must be readable only when face is front-facing.

### 4.3 CTA Placement

There are two valid CTA models:

| CTA model | Best for | Notes |
|---|---|---|
| Persistent CTA outside cube | Smaller slots, simpler trafficking | Same CTA visible regardless of face. Reduces accidental hidden CTA issues. |
| Face-level CTA | Multi-product / multi-offer campaigns | Each face can click to a different URL. Requires careful tracking and larger safe targets. |

For face-level CTAs:

- Keep CTA on the lower third of the face.
- Avoid placing CTA near the cube edge where perspective distortion can reduce legibility.
- CTA must remain clickable only when the face is active/front-facing unless intentional side-face interaction is approved.
- Use separate tracking IDs per face.

### 4.4 Logo Placement

Logo strategies:

| Strategy | Recommendation |
|---|---|
| Persistent logo outside cube | Best for brand consistency and small sizes. |
| Logo on each face | Works for self-contained faces but can feel repetitive. |
| Logo on first and final face only | Works for storytelling, but ensure brand attribution remains visible enough. |
| Watermark logo | Acceptable if contrast is sufficient and does not reduce readability. |

Minimum logo guidance:

- Preserve clear space around logo.
- Do not place logo on highly distorted cube edges.
- Do not allow logo to disappear for long periods during autoplay unless a persistent brand mark exists.

### 4.5 Safe Zones

| Zone | Guidance |
|---|---|
| Outer slot edge | Maintain 8-16px padding for standard display; 20-30px for large billboard. |
| Cube face edge | Keep text and CTA at least 10-15px from face edge. |
| Rotation edge | Avoid critical text on left/right edges because perspective distortion can clip or skew it. |
| Close/control zone | If controls exist, reserve top-right or bottom-right area. |
| Touch zone | Leave clear separation between swipe area and CTA area. |

### 4.6 Readability

- Use large, high-contrast type.
- Avoid more than 8-12 words on small faces.
- Avoid fine legal copy inside rotating faces; place legal in a static bottom strip if required.
- Keep text flat on the face; do not rotate text independently.
- Avoid text that becomes unreadable during partial rotation.

### 4.7 Motion Intensity

Motion should support exploration, not distract from the page.

Recommended limits:

| Motion parameter | Recommendation |
|---|---|
| Autoplay cycles | 1-2 full cycles, then pause or slow down |
| Rotation speed | 500-900 ms per quarter turn |
| Easing | Smooth ease-out or cubic-bezier; avoid elastic/bouncy motion for ads near editorial content |
| Parallax depth | Subtle. Avoid deep z-distance that causes clipping in iframe. |
| Continuous spinning | Avoid. It harms readability and may trigger motion discomfort. |
| Reduced motion | Disable rotation; use fade or static controls. |

### 4.8 Touch Targets

| Control | Minimum | Preferred |
|---|---:|---:|
| CTA button | 36x36 CSS px | 44x44 CSS px or larger |
| Close button | 24x24 CSS px | 44x44 CSS px touch area |
| Arrow controls | 32x32 CSS px | 44x44 CSS px |
| Dot indicators | 16x16 CSS px visual, 32x32 hit area | 44x44 hit area on mobile |

### 4.9 Visual Density

Use fewer elements than a normal static banner because motion and perspective already add complexity.

Recommended maximum per face:

| Slot size | Max elements per face |
|---|---:|
| 320x50 | 2-3 elements: logo, short text, micro CTA |
| 300x250 | 4 elements: visual, headline, logo, CTA |
| 300x600 | 5-6 elements, with details below cube rather than inside face |
| 728x90 / 970x90 | 3-4 horizontal elements; avoid dense face copy |
| 970x250 | 5-7 elements across cube + side copy panel |
| 970x500 | 7-10 elements if clearly grouped |

### 4.10 Brand Safety

- Avoid fake UI elements that mimic publisher controls.
- Avoid misleading "close", "play", "download", or system notification graphics.
- Do not disguise CTAs as editorial navigation.
- Avoid shocking or rapid-flash animation.
- Do not rotate into sensitive imagery unexpectedly.
- Keep regulated category disclaimers readable and persistent where required.

### 4.11 Do and Don't Recommendations

| Do | Don't |
|---|---|
| Use the first face as the clearest hero message. | Start with a side or partially rotated face. |
| Provide swipe/drag cues and fallback controls. | Assume users will discover drag without clues. |
| Keep each face visually simple. | Put full banner copy on every cube face. |
| Pause autoplay after user interaction. | Fight the user by resuming autoplay immediately. |
| Use transform/opacity-based animation. | Animate width, height, top, left, or margins. |
| Include static and flat carousel fallback. | Depend on 3D support across every app/webview. |
| Track face views and face clicks separately. | Treat the whole cube as one undifferentiated click zone. |
| Test low-end mobile devices. | Approve only on desktop high-end machines. |
| Respect reduced motion preferences. | Force continuous spinning. |
| Keep CTA tap zones separate from drag zones. | Make every drag accidentally click the ad. |

---

## 5. Asset Specifications

### A. Image Assets

#### Supported Formats

| Asset type | Recommended formats | Notes |
|---|---|---|
| Face images | WebP, JPG, PNG | WebP preferred where supported. JPG for photographic content. PNG for transparency/logos. |
| Logo | SVG, PNG | SVG preferred if publisher/ad server permits and file is sanitized. PNG fallback required. |
| Background | JPG, WebP | Avoid massive background images. Crop per size, do not rely only on CSS scaling. |
| Icons / arrows / dots | SVG, PNG, CSS shapes | Inline SVG can be efficient if sanitized. |
| Backup image | JPG, PNG, WebP | Must render without JS. Should include logo, message, CTA. |

#### Recommended Compression

| Asset | Recommendation |
|---|---|
| JPG | 70-85 quality depending on detail. Avoid compression artifacts on product images. |
| PNG | Use only for alpha/flat graphics. Compress with lossless optimizer. |
| WebP | Use quality 70-85 for photos, lossless only when necessary. |
| SVG | Remove metadata, editor comments, external references, and script. |
| Animated image | Avoid GIF for core animation; prefer CSS/JS motion or MP4 where appropriate. |

#### Retina / High-Density Considerations

- Provide 2x assets for high-density displays where file budget allows.
- For 300x250, face image source may be 600x500 or tailored per face, but avoid loading all 2x faces upfront if heavy.
- For 970x250, export face and background assets at display size or 1.5x/2x only when needed.
- Use responsive image logic carefully; do not trigger multiple unused downloads inside ad iframes.

#### Background Image Rules

- Backgrounds should not contain small legal text.
- Avoid placing critical details at the edges of cube faces.
- For 3D depth, use subtle lighting/shadow baked into face design rather than expensive runtime filters.
- Maintain visual consistency across faces so rotation does not feel like a broken layout.

#### Transparent Overlay Rules

- Use transparent overlays sparingly.
- Avoid overlapping transparent layers that create GPU compositing cost.
- Ensure text contrast meets accessibility expectations.
- Do not place clickable transparent overlays over the entire cube unless click behavior is intentional and approved.

#### Maximum Recommended File Sizes

| Creative size | Initial load target | Polite/subload target | Total recommended max |
|---|---:|---:|---:|
| 320x50 | 50-100 KB | 100-200 KB | 200-300 KB |
| 300x250 | 100-150 KB | 200-400 KB | 400-600 KB |
| 300x600 | 150-200 KB | 300-600 KB | 600-900 KB |
| 728x90 / 970x90 | 100-180 KB | 200-500 KB | 500-700 KB |
| 970x250 | 150-250 KB | 400-800 KB | 800 KB-1.2 MB |
| 970x500 | 200-300 KB | 700 KB-1.5 MB | 1.5-2.0 MB only with publisher approval |
| Mobile app | SDK/publisher-specific | SDK/publisher-specific | Keep conservative; low-end device performance matters. |

These are operational recommendations, not universal hard limits. Publisher requirements may be stricter.

---

### B. Video Assets

Video is optional. The RollExplore Cube can support video on one or more faces, but this should be used carefully because video inside 3D transforms can increase CPU/GPU cost and cause rendering inconsistencies on some browsers or app webviews.

#### Supported Video Formats

| Format | Recommendation |
|---|---|
| MP4 | Preferred baseline. Use H.264 video and AAC audio when audio exists. |
| WebM | Optional web optimization if supported by publisher environment. |
| HLS/DASH | Usually not recommended inside small display cube unless using a player and approved. |
| Poster image | Required for each video face. |
| Fallback image | Required when autoplay/video fails. |

#### Video Behaviour Rules

| Requirement | Guidance |
|---|---|
| Autoplay | Must be muted. Start only when viewable and after creative load. |
| Audio | User-initiated only. Provide visible mute/unmute control if audio is supported. |
| Mobile playback | Use `playsinline` to avoid fullscreen takeover on mobile browsers. |
| Duration | 6-15 seconds recommended for face video; 30 seconds max only for premium units. |
| Looping | Acceptable for short ambient motion, but avoid infinite attention-draining loops. |
| Poster frame | Must communicate the face message if video does not play. |
| Loading | Lazy-load video after initial render or on face activation. Do not preload all face videos. |
| Tracking | Track start, quartiles, complete, pause, replay, mute/unmute where relevant. |

#### File-Size Guidance

| Video usage | Recommended max |
|---|---:|
| Initial load video | Avoid. Use poster instead. |
| Polite-loaded short face video | 500 KB-1.5 MB depending on slot and publisher approval. |
| Large premium unit video | 2-4 MB only with explicit publisher approval and network conditions handling. |
| Mobile app video | SDK/publisher-specific. Conservative bitrate and fallback required. |

#### Video Inside a Rotating Face

When a face contains video:

- Pause video when the face rotates away from the front.
- Do not autoplay more than one video face at a time.
- Use poster while face is side-facing or inactive.
- Consider replacing the actual video element with a poster during rotation to reduce rendering cost.
- Do not play audio during cube rotation.

---

### C. HTML5 / JS / CSS Assets

#### Creative Bundle Expectations

The creative should be packaged as a self-contained HTML5 unit or custom template output that includes:

- `index.html` or template-rendered markup.
- CSS for layout, fallback, animation, responsive behavior.
- JavaScript controller for state, rotation, gestures, tracking, and click handling.
- Image/video assets or externally hosted CDN references.
- Backup image.
- Optional JSON configuration for face content and tracking.

#### CDN-Hosted Assets

CDN-hosted assets are acceptable when:

- HTTPS is used.
- CORS and cache headers are correct.
- Asset URLs are stable for campaign duration.
- Cachebuster is not incorrectly appended to static heavy assets.
- Third-party host is publisher-approved.
- The creative has a backup if CDN assets fail.

#### Avoiding Heavy JS

Avoid:

- Large animation libraries unless essential.
- DOM-heavy frameworks for a simple cube.
- Runtime 3D engines such as Three.js for standard display units unless a premium unit justifies it.
- Excessive tracking libraries.
- Long main-thread tasks.

Recommended:

- Vanilla JS or lightweight framework-free controller.
- `requestAnimationFrame` for drag updates.
- CSS transitions for snap rotation.
- Passive listeners where appropriate, but switch carefully when preventing default gestures.
- Event throttling for drag tracking.

#### Animation Performance

- Animate `transform` and `opacity` only.
- Pre-size all faces and wrapper dimensions.
- Use `backface-visibility: hidden` for cube faces.
- Use `transform-style: preserve-3d` on cube wrapper.
- Use `perspective` at scene level.
- Use `contain: layout paint style` cautiously if it does not break rendering.
- Remove `will-change` after animation where possible.

#### Request Count Discipline

| Creative type | Recommended request count |
|---|---:|
| Static/image-only cube | 5-10 total requests |
| Cube with tracking pixels | 8-15 total requests |
| Cube with video face | 10-20 total requests, with video lazy-loaded |
| Premium large unit | Publisher-specific; document and approve all third-party calls |

#### Fallback Behaviour

Fallback must activate when:

- CSS 3D transform support is unavailable or unreliable.
- JavaScript fails or is blocked.
- SafeFrame/app environment clips or flattens the cube.
- Device performance drops below acceptable frame rate.
- User prefers reduced motion.
- Video cannot play.

Fallback hierarchy:

1. 3D cube full interaction.
2. 2D swipe carousel using same face content.
3. Static multi-panel layout if slot is large enough.
4. Single backup image with click-through.

---

### D. Optional Interactive Assets

| Interactive asset | Applicability | Guidance |
|---|---|---|
| Hotspots | Product/features | Use only on active front face. Track hotspot_click separately. |
| Product tiles | Retail, auto, tech | One tile per face or small set in large sizes. Avoid tiny tap targets. |
| Quiz states | BFSI, education, entertainment | Use only in larger units. Requires completion tracking and data policy review. |
| Swipe gestures | Mobile / app | Recommended primary interaction. Must not break vertical scroll. |
| Drag gestures | Desktop/mobile | Recommended for exploration. Add snap-to-face behavior. |
| Form fields | Lead gen variants | Not recommended in small cube. Use expanded/large variant with privacy and consent controls. |
| Multiple CTAs | Multi-offer campaigns | Use face-specific CTA URL and tracking. Avoid confusing destinations. |
| Navigation dots | All variants except tiny banners | Strongly recommended for accessibility and discoverability. |
| Arrow controls | Desktop, large mobile | Recommended. Should not cover face content. |
| Progress indicator | Storytelling units | Useful when faces are sequential. |

---

## 6. IAB / UX Compliance Considerations

The RollExplore Cube should align with modern lightweight, non-disruptive ad principles. Even though the format is custom, it should respect industry expectations around user control, performance, transparency, and measurement.

### 6.1 Lightweight Experience Principles

| Principle | Implementation requirement |
|---|---|
| Keep initial load lightweight | Load the initial face, CSS, minimal JS, logo, and backup only. Defer heavy face assets. |
| Use polite loading | Load additional faces/video after render, viewability, or user interaction. |
| Avoid unexpected audio | All video/audio starts muted. Audio only after explicit user action. |
| Provide control | Pause autoplay on interaction and expose navigation controls. |
| Avoid layout shift | Reserve slot dimensions before creative renders. |
| Avoid misleading UI | Do not imitate publisher navigation, app alerts, system controls, or close buttons. |
| Respect safe areas | Keep controls and CTAs within device-safe zones. |
| Maintain clear ad identity | Ensure the unit is recognizable as advertising where publisher labeling requires it. |

### 6.2 Format-Specific Compliance Risks

| Risk | Why it matters | Mitigation |
|---|---|---|
| Excessive motion | Continuous spinning can be distracting or uncomfortable. | Limit cycles, pause on interaction, respect reduced motion. |
| Accidental clicks | Drag/swipe can be mistaken as click. | Separate tap and drag thresholds; do not fire clicks after drag. |
| Hidden CTA | CTA can rotate out of view. | Use active-face CTA logic or persistent CTA zone. |
| Face text unreadable during rotation | Perspective distortion reduces readability. | Keep important text front-facing; pause long enough per face. |
| Heavy GPU usage | 3D transforms, shadows, filters, and video can cause jank. | Use transform-only animation, reduce layers, test low-end devices. |
| SafeFrame clipping | 3D depth or controls may exceed iframe bounds. | Keep all transformed content inside slot and test SafeFrame. |
| App webview inconsistency | Mobile SDKs may flatten/clip transforms. | Add app-specific fallback and QA. |

### 6.3 Intrusiveness Boundaries

The format must not:

- Take over the full screen unless user-initiated and approved as a separate variant.
- Block reading or navigation.
- Prevent page scroll.
- Force users to complete an interaction.
- Autoplay audio.
- Use deceptive gestures or fake system UI.
- Capture all page gestures outside the ad slot.

---

## 7. GAM Implementation Specification

### 7.1 Recommended Creative Type

| GAM option | Recommendation |
|---|---|
| Custom creative | Recommended for bespoke rich-media builds and direct implementation control. |
| Custom creative template | Strongly recommended for repeatable AcunX operations and future ad-builder automation. |
| Third-party creative | Acceptable if supplied by certified rich-media vendor and approved by publisher. |
| HTML5 creative upload | Acceptable for self-contained ZIP assets, but template variables and tracking may be harder to standardize. |
| Native creative | Not the default. Only use if the cube is specifically implemented as a native-like in-feed component. |
| VAST creative | Only when the unit is served as a video ad through a player/outstream environment. Not required for basic HTML5 cube. |

### 7.2 Custom Template Recommendation

For production, create a reusable **RollExplore Cube Creative Template** in GAM with configurable fields for:

- Face count.
- Face image/video assets.
- Face headlines.
- Face CTA labels and URLs.
- Rotation speed.
- Autoplay mode.
- Interaction mode.
- Tracking endpoints.
- Backup image.
- Feature flags for video, reduced motion, fallback mode, and close button.

This enables AdOps to traffic multiple cube campaigns without editing raw HTML/JS each time.

### 7.3 SafeFrame Guidance

SafeFrame should be **enabled and tested carefully** rather than assumed safe or unsafe.

| Scenario | Guidance |
|---|---|
| In-slot 300x250/300x600 cube | SafeFrame likely workable if all content stays inside iframe. Test clipping and click macros. |
| 728x90/970x90 shallow roll | SafeFrame likely workable; verify perspective and pointer events. |
| Expanded/fullscreen variant | SafeFrame may restrict required behavior. Requires publisher-specific SafeFrame expansion/geometry approval or friendly iframe/custom integration. |
| App SDK/webview | SafeFrame may not apply; use SDK/MRAID/OMID-specific QA. |

Never assume the cube can access parent page context. It should work inside an iframe with no direct parent DOM access.

### 7.4 Required Creative Sizes

At minimum, define the booked slot sizes in GAM exactly as the creative supports.

Recommended size declarations:

| Campaign variant | GAM sizes |
|---|---|
| Standard desktop/mobile | 300x250 |
| Mobile rectangle | 320x480 |
| Half-page | 300x600 |
| Leaderboard | 728x90 |
| Billboard | 970x250 |
| Super leaderboard | 970x90 |
| Premium large | 970x500 |
| Responsive | Use GPT responsive size mapping and slot-defined eligible sizes. |

Do not traffic a 970x250 creative into 728x90 or 300x250 inventory unless the creative is truly responsive and QA-approved for that size.

### 7.5 Multi-Size Mapping

For responsive sites, use GPT size mapping so the eligible size changes by viewport. Example strategy:

| Viewport | Eligible cube sizes |
|---|---|
| Desktop >= 1024px | 970x250, 970x90, 728x90, 300x250 |
| Tablet >= 768px | 728x90, 300x250, 300x600 where placement allows |
| Mobile >= 320px | 320x50, 300x250, 320x480 where placement allows |

Reserve enough slot height for the largest eligible size at that breakpoint or use explicit layout containers to prevent cumulative layout shift.

### 7.6 Key-Values / Custom Targeting

Recommended GAM key-values:

| Key | Example values | Purpose |
|---|---|---|
| `format` | `rollexplore_cube` | Format targeting/reporting. |
| `format_family` | `rich_media`, `interactive_display` | Group reporting. |
| `interaction_mode` | `autoplay`, `swipe`, `drag`, `hybrid`, `static_fallback` | Creative behavior targeting. |
| `face_count` | `4`, `6` | Operational QA and reporting. |
| `device_class` | `desktop`, `mobile_web`, `app`, `tablet` | Device-specific delivery. |
| `slot_type` | `in_banner`, `in_content`, `billboard`, `sidebar` | Placement logic. |
| `creative_variant` | `hero_offer`, `product_faces`, `video_face` | Variant reporting. |
| `publisher_approved` | `true` | Control delivery to approved placements. |
| `safe_frame_tested` | `true`, `false` | Deployment governance. |

### 7.7 Click-Through URL Setup

Two click models are supported:

| Click model | Use case | Implementation |
|---|---|---|
| Single destination | Brand awareness / one landing page | One click macro-wrapped `click_url`. |
| Face-specific destinations | Product/offer exploration | Each face has `face_n_cta_url`, macro-wrapped and tracked separately. |

Do not make the full cube clickable during drag. Click should fire only if the pointer/touch movement is below the click threshold.

### 7.8 Impression Tracking

Recommended impression tracking layers:

- GAM-served impression by default.
- Creative-render event when HTML/JS initializes.
- Viewable impression via GAM Active View where applicable.
- Third-party impression pixel, if provided and approved.
- Custom `creative_loaded` and `creative_in_view` events for rich-media analytics.

### 7.9 Third-Party Tracking Pixels

- Fire impression pixels only once per creative render.
- Fire interaction pixels only on meaningful user interactions, not on every animation frame.
- Use cachebusters for non-cacheable tracking calls.
- Do not load unapproved tracking vendors.
- Avoid high-frequency event calls during drag; aggregate drag events and fire `drag_complete` once.

### 7.10 Cachebuster Handling

Use GAM cachebuster macros or equivalent only for tracking endpoints that require unique calls. Do not append cachebusters to static assets unless necessary, because this reduces caching efficiency.

### 7.11 Preview and QA Process

Before launch:

1. Preview in GAM creative preview.
2. Preview on publisher test page with the actual slot and GPT tags.
3. Test with SafeFrame enabled and disabled if publisher supports both.
4. Validate all size variants.
5. Validate face click URLs and tracking.
6. Test on real mobile devices.
7. Test low-end Android device or throttled CPU profile.
8. Confirm backup image renders if JS/assets fail.
9. Confirm no layout shift or clipping in the booked placement.

### 7.12 GAM Configurable Variables

| Variable name | Type | Example | Required / Optional | Purpose |
|---|---|---|---|---|
| `creative_variant_id` | String | `cube_auto_q2_001` | Required | Unique creative/reporting identifier. |
| `click_url` | URL | `%%CLICK_URL_UNESC%%https://brand.com` | Optional | Global click-through when all faces share one destination. |
| `impression_url` | URL | `https://tracker.example/imp?cb=%%CACHEBUSTER%%` | Optional | Third-party impression pixel. |
| `backup_image_url` | File/URL | `backup_300x250.jpg` | Required | Static fallback image. |
| `face_count` | Number | `4` | Required | Number of cube faces. |
| `face_1_image_url` | File/URL | `face1.webp` | Required | Image for face 1. |
| `face_2_image_url` | File/URL | `face2.webp` | Required | Image for face 2. |
| `face_3_image_url` | File/URL | `face3.webp` | Required if face count >= 3 | Image for face 3. |
| `face_4_image_url` | File/URL | `face4.webp` | Required if face count >= 4 | Image for face 4. |
| `face_5_image_url` | File/URL | `face5.webp` | Optional | Image for face 5. |
| `face_6_image_url` | File/URL | `face6.webp` | Optional | Image for face 6. |
| `face_1_video_url` | File/URL | `face1.mp4` | Optional | Optional video asset for face 1. |
| `face_2_video_url` | File/URL | `face2.mp4` | Optional | Optional video asset for face 2. |
| `face_1_headline` | Text | `Explore the new SUV` | Optional | Face-level headline if text is template-rendered. |
| `face_2_headline` | Text | `Built for city drives` | Optional | Face-level headline. |
| `face_1_cta_text` | Text | `Book now` | Optional | CTA label for face 1. |
| `face_2_cta_text` | Text | `View offer` | Optional | CTA label for face 2. |
| `face_1_cta_url` | URL | `%%CLICK_URL_UNESC%%https://brand.com/model` | Optional | Face-specific click destination. |
| `face_2_cta_url` | URL | `%%CLICK_URL_UNESC%%https://brand.com/offer` | Optional | Face-specific click destination. |
| `global_cta_text` | Text | `Learn more` | Optional | Persistent CTA label. |
| `global_cta_url` | URL | `%%CLICK_URL_UNESC%%https://brand.com` | Optional | Persistent CTA URL. |
| `autoplay` | Boolean | `true` | Optional | Enables automatic rotation. |
| `autoplay_delay_ms` | Number | `1500` | Optional | Delay before first rotation. |
| `autoplay_interval_ms` | Number | `3500` | Optional | Time between automatic rotations. |
| `rotation_speed_ms` | Number | `700` | Optional | Duration of rotation snap. |
| `max_autoplay_cycles` | Number | `2` | Optional | Limits motion. |
| `interaction_mode` | Enum | `hybrid` | Required | Values: `autoplay`, `swipe`, `drag`, `buttons`, `hybrid`, `fallback`. |
| `drag_enabled` | Boolean | `true` | Optional | Enables mouse/touch drag. |
| `swipe_enabled` | Boolean | `true` | Optional | Enables mobile swipe. |
| `arrow_controls_enabled` | Boolean | `true` | Optional | Shows previous/next arrows. |
| `dot_controls_enabled` | Boolean | `true` | Optional | Shows face indicators. |
| `keyboard_controls_enabled` | Boolean | `true` | Recommended | Enables keyboard navigation. |
| `close_button_enabled` | Boolean | `false` | Optional | Adds dismiss control if publisher requires it. |
| `reduced_motion_mode` | Enum | `flat_carousel` | Recommended | Fallback for reduced-motion preference. |
| `fallback_mode` | Enum | `flat_carousel` | Required | Fallback behavior if 3D unsupported. |
| `muted` | Boolean | `true` | Required if video | Ensures video starts muted. |
| `video_loop` | Boolean | `false` | Optional | Loop short face video. |
| `playsinline` | Boolean | `true` | Required if mobile video | Prevents forced fullscreen video where supported. |
| `custom_tracking_pixel_1` | URL | `https://tracker.example/p1?cb=%%CACHEBUSTER%%` | Optional | Additional approved tracker. |
| `custom_tracking_pixel_2` | URL | `https://tracker.example/p2?cb=%%CACHEBUSTER%%` | Optional | Additional approved tracker. |
| `custom_tracking_pixel_3` | URL | `https://tracker.example/p3?cb=%%CACHEBUSTER%%` | Optional | Additional approved tracker. |
| `custom_tracking_pixel_4` | URL | `https://tracker.example/p4?cb=%%CACHEBUSTER%%` | Optional | Additional approved tracker. |
| `custom_tracking_pixel_5` | URL | `https://tracker.example/p5?cb=%%CACHEBUSTER%%` | Optional | Additional approved tracker. |
| `interaction_tracking_url` | URL | `https://tracker.example/event` | Optional | Endpoint for rich interaction events. |
| `face_view_tracking_url` | URL | `https://tracker.example/face-view` | Optional | Tracks active face views. |
| `face_click_tracking_url` | URL | `https://tracker.example/face-click` | Optional | Tracks face-level clicks. |
| `drag_tracking_url` | URL | `https://tracker.example/drag` | Optional | Tracks drag start/complete. |
| `video_start_tracking_url` | URL | `https://tracker.example/video-start` | Optional | Video start tracking. |
| `video_complete_tracking_url` | URL | `https://tracker.example/video-complete` | Optional | Video complete tracking. |
| `frequency_cap_key` | String | `rollexplore_cube_campaign_42` | Optional | Used by publisher/vendor logic for motion/expanded caps. |

---

## 8. Tracking & Analytics Event Taxonomy

### 8.1 Event Design Principles

- Track meaningful states, not every animation frame.
- Use a unique creative/session ID to deduplicate events.
- Include face index and face ID where applicable.
- Separate passive autoplay rotation from user-initiated rotation.
- Separate face views from face clicks.
- Avoid inflating clicks from drag/swipe events.
- Fire custom events through approved endpoints only.

### 8.2 Recommended Event Table

| Event name | Trigger | Required / Optional | Tracking method | Notes |
|---|---|---|---|---|
| `impression_rendered` | GAM renders creative iframe/snippet | Required | GAM impression + optional pixel | Standard served impression. |
| `creative_loaded` | HTML/CSS/JS initialized and first face ready | Required | JS event/pixel | Confirms creative execution, not just ad server delivery. |
| `viewable_impression` | Unit meets viewability criteria in supported measurement stack | Recommended | GAM Active View / measurement vendor | Use standard viewability reporting where supported. |
| `creative_in_view` | Cube enters viewport threshold, e.g. 50% visible | Recommended | JS IntersectionObserver or SDK event | Useful for starting autoplay. Do not replace official viewability. |
| `initial_face_view` | First face displayed and readable | Required | JS event | Include `face_index=1`. |
| `cube_autoplay_start` | Autoplay rotation begins | Optional | JS event | Only if autoplay enabled. |
| `cube_autoplay_stop` | Autoplay stops after cycles or interaction | Optional | JS event | Helps measure user-safe behavior. |
| `cube_rotate` | Cube completes a rotation to another face | Required | JS event | Include source: `autoplay`, `drag`, `swipe`, `arrow`, `dot`, `keyboard`. |
| `face_view` | A face becomes active/front-facing for minimum dwell threshold | Required | JS event | Use dwell threshold, e.g. 500-1000 ms, to avoid noisy tracking during quick drags. |
| `face_click` | User clicks/taps an active face click zone | Recommended | JS event + click macro | Include face ID and destination ID. |
| `cta_click` | User clicks/taps CTA | Required | GAM click macro + JS event | Separate `global_cta` vs `face_cta`. |
| `drag_start` | User begins drag after threshold | Recommended | JS event | Do not fire on simple tap. |
| `drag_complete` | Drag snaps to a face or returns to origin | Recommended | JS event | Include from_face, to_face, direction. |
| `swipe` | Mobile swipe changes face | Recommended | JS event | Can be combined with `cube_rotate` but useful for mobile reporting. |
| `arrow_next` | User taps/clicks next arrow | Optional | JS event | Useful for UX analytics. |
| `arrow_previous` | User taps/clicks previous arrow | Optional | JS event | Useful for UX analytics. |
| `dot_navigation` | User selects face dot | Optional | JS event | Include selected face index. |
| `keyboard_navigation` | User navigates by keyboard | Optional | JS event | Accessibility/UX insight. |
| `hotspot_click` | User taps hotspot on active face | Optional | JS event + click/event pixel | Only if hotspots are implemented. |
| `video_start` | Face video starts | Required if video | Video event pixel/JS event | Must distinguish muted autoplay vs user-initiated play. |
| `video_25` | 25% video progress | Optional | Video event pixel/JS event | Use when video is meaningful. |
| `video_50` | 50% video progress | Optional | Video event pixel/JS event | Use when video is meaningful. |
| `video_75` | 75% video progress | Optional | Video event pixel/JS event | Use when video is meaningful. |
| `video_complete` | Video completes | Required if video KPI | Video event pixel/JS event | Required for video-led reporting. |
| `video_mute` | User mutes video | Optional | JS event | Track only user action. |
| `video_unmute` | User unmutes video | Optional | JS event | Must be user-initiated. |
| `video_pause` | User pauses or face rotates away | Optional | JS event | Include reason. |
| `video_replay` | User replays video | Optional | JS event | Useful for engagement. |
| `time_in_unit` | User dwell time in active/viewable unit | Recommended | Aggregated JS event | Fire at unload or defined intervals, not continuously. |
| `interaction_complete` | User has viewed all faces or completed intended exploration path | Optional | JS event | Strong engagement signal. |
| `collapse` | Dismiss/collapse action if enabled | Optional | JS event | Only relevant if close/collapse exists. |
| `close` | User closes/dismisses unit | Optional | JS event | Required if close exists. |
| `fallback_rendered` | Static or flat fallback is shown | Required | JS event/pixel where possible | Helps diagnose compatibility/performance issues. |
| `error` | Asset/script/runtime failure | Recommended | JS event/log endpoint | Do not expose technical error to user. |

### 8.3 Face View Rules

A `face_view` should fire only when:

- The face is front-facing or within an approved angle threshold, such as +/- 10 degrees.
- The unit is in view according to the creative's in-view detection, where available.
- The face remains active for a minimum dwell threshold, typically 500-1000 ms.
- The event has not already fired for that face during the same impression, unless repeat views are intentionally tracked separately.

### 8.4 Drag Tracking Rules

- Fire `drag_start` only after the drag threshold is crossed.
- Do not fire `cta_click` after a drag gesture.
- Fire `drag_complete` once per completed drag gesture.
- Include direction, from_face, to_face, drag distance, and whether the face changed.
- Throttle any debug/diagnostic gesture tracking.

---

## 9. GAM Macros & Click Tracking

### 9.1 Click Macro Usage

For GAM-served custom creatives, click URLs should be wrapped with GAM click macros so clicks are counted by GAM before redirecting to the advertiser landing page.

Generic examples:

```text
%%CLICK_URL_UNESC%%https://advertiser.example/landing-page
%%CLICK_URL_ESC%%https%3A%2F%2Fadvertiser.example%2Flanding-page
```

Use the unescaped or escaped form based on whether the destination URL is inserted directly into an `href` or nested as a parameter inside another tracking URL.

### 9.2 Face-Level Click Tracking

For face-specific CTAs, each face should have its own URL variable:

```text
face_1_cta_url = %%CLICK_URL_UNESC%%https://advertiser.example/product-a
face_2_cta_url = %%CLICK_URL_UNESC%%https://advertiser.example/product-b
face_3_cta_url = %%CLICK_URL_UNESC%%https://advertiser.example/offer
face_4_cta_url = %%CLICK_URL_UNESC%%https://advertiser.example/store-locator
```

The creative should also send a custom `face_click` or `cta_click` event before navigation where permitted. Ensure the event does not block navigation if the tracking endpoint is slow.

### 9.3 Impression / View Macro Usage

For third-party impression pixels, use a cachebuster macro where required:

```html
<img src="https://tracker.example/imp?creative=${creative_variant_id}&cb=%%CACHEBUSTER%%" width="1" height="1" style="display:none" alt="" />
```

Do not use impression pixels as a substitute for GAM delivery reporting or official viewability measurement.

### 9.4 Cachebuster Macro Usage

Use cachebusters for:

- Impression pixels.
- Event pixels.
- Third-party tracking URLs that must be unique per event.

Avoid cachebusters for:

- Static images.
- CSS files.
- JS files.
- Video assets.

### 9.5 Third-Party Tracker Usage

Third-party trackers should be:

- HTTPS only.
- Publisher-approved.
- Fired once per intended event.
- Deduplicated across autoplay/user events.
- Non-blocking.
- Resilient to ad blockers and network failures.

### 9.6 Multiple CTA Tracking

For multiple CTAs:

- Track CTA ID, face ID, and destination group.
- Use separate click URLs or a redirect service that preserves GAM click counting.
- Avoid wrapping URLs multiple times incorrectly.
- Verify that final landing page opens correctly on mobile app and mobile web.

### 9.7 Deep Link / Landing Page Handling

For app campaigns:

- Confirm whether deep links are allowed by the publisher/app SDK.
- Provide web fallback URLs.
- Avoid unapproved automatic app store redirects.
- Test universal links/app links on iOS and Android.

### 9.8 Avoiding Invalid Click Inflation

The creative must not:

- Count drag as click.
- Fire click on autoplay rotation.
- Use invisible full-slot click layers that override controls unintentionally.
- Trigger click when user taps arrows/dots unless those controls are intended CTAs.
- Fire multiple click trackers for one user click unless the tracking chain is explicitly designed and approved.

---

## 10. VAST / Video Handling

### 10.1 Is VAST Required?

VAST is **not required** for a standard HTML5 RollExplore Cube if video is simply embedded as an HTML5 `<video>` element inside a display/rich-media creative.

VAST **may be required or appropriate** when:

- The cube is served inside an outstream video player.
- The inventory is transacted as video inventory.
- A publisher/video platform requires VAST for video ad decisioning.
- Buyer reporting expects VAST video events.
- The video is delivered through a player that consumes a VAST tag.

### 10.2 HTML5 Video Inside Cube

When video is inside a cube face:

- Use muted autoplay only.
- Start playback only when the face is active and viewable.
- Pause when the face rotates away.
- Provide poster and fallback image.
- Track video start, progress, complete, mute/unmute, pause, and replay as needed.
- Avoid loading video until the face is near activation or user intent is detected.

### 10.3 VAST / Player-Based Inventory

If the RollExplore Cube is adapted to player-based or outstream inventory:

- Use VAST-compatible delivery according to the video platform's requirements.
- Confirm whether interactive overlays are allowed by the player and publisher.
- Confirm OMID/Open Measurement support for verification.
- Ensure click-through and video quartile tracking remain accurate.
- Do not assume display click macros and VAST click tracking are interchangeable.

### 10.4 Audio Rules

- Audio must never start unexpectedly.
- Autoplay video must be muted.
- Unmute must be user-initiated.
- Visual state must clearly indicate muted/unmuted status.
- Audio controls must be reachable and labeled.

### 10.5 Video Performance Rules

- Do not place multiple active videos on different faces simultaneously.
- Use one active video element at a time where possible.
- Replace inactive video faces with poster images.
- Avoid rotating a playing video if it causes jank; pause during rotation if necessary.
- Use conservative bitrate for mobile.

---

## 11. OpenRTB / Programmatic Compatibility

### 11.1 Likely Inventory Classification

In OpenRTB/programmatic systems, this format is usually represented as display/rich-media inventory rather than a unique standard object type.

| Environment | Likely classification | Notes |
|---|---|---|
| Web standard slot | Banner/display with rich-media creative attributes | Declare actual slot size. Rich-media capability depends on exchange/publisher. |
| In-content display | Banner/display or custom rich-media package | Often best sold through PMP/PG or direct IO. |
| Mobile app | Banner/display, MRAID-capable rich media where supported | Requires SDK capability and OMID measurement support. |
| Video-face variant | Still display unless served through video player | Do not classify as video inventory unless the placement is video/player-based. |
| Expanded/fullscreen variant | High-impact/expandable/interstitial-like depending on implementation | Requires explicit buyer/publisher approval and platform support. |

### 11.2 Standard Programmatic vs Custom Deal

| Buying path | Suitability |
|---|---|
| Open exchange | Limited. Standard display slot may deliver, but rich interaction support and approval can be inconsistent. |
| PMP | Good when publishers expose rich-media-approved inventory and buyers understand the format. |
| Programmatic Guaranteed | Strong fit for premium campaigns requiring predictable delivery and QA. |
| Direct IO | Best for first launch, custom creative QA, and publisher-specific engineering. |
| Curated deal package | Good for scaling across approved publishers with consistent specs. |

### 11.3 Required Metadata for Buyers

Provide buyers/creative reviewers with:

- Format name: RollExplore Cube.
- Creative type: HTML5 rich-media display.
- Supported sizes.
- Face count.
- Interaction model: autoplay, swipe, drag, arrows, dots, hybrid.
- Whether video is present.
- Whether audio can be user-enabled.
- Initial load and total load weights.
- Number of third-party calls.
- Measurement vendors and tracking events.
- SafeFrame/MRAID/OMID requirements.
- Fallback behavior.
- Publisher approval status.
- Screenshots or preview links for each size.

### 11.4 Size Declaration

Declare the actual slot size in the bid request/ad server configuration. Do not use a hidden larger canvas unless the publisher explicitly supports expansion.

Examples:

| Creative size | Programmatic declaration |
|---|---|
| 300x250 cube | Banner/display 300x250 |
| 300x600 cube | Banner/display 300x600 |
| 970x250 cube | Banner/display 970x250 |
| 320x480 mobile cube | Mobile display 320x480 or publisher-specific mobile rich-media size |
| Responsive cube | Depends on SSP/GAM integration; exact mapping must be documented. |

### 11.5 Creative Attributes

The format may require creative attribute declarations depending on SSP/DSP taxonomy:

- Rich media / interactive.
- HTML5.
- User-interactive animation.
- Expandable only if actual expansion exists.
- Audio/video only if included.
- MRAID only if mobile app creative uses MRAID APIs.
- OMID support if in-app measurement is expected.

Exact OpenRTB mapping depends on the exchange, SSP, DSP, and publisher implementation. Do not invent unsupported OpenRTB fields. Use platform-specific creative attributes and deal metadata where needed.

### 11.6 API / MRAID / OMID Considerations

| Technology | Relevance |
|---|---|
| MRAID | Relevant for in-app rich media if expand/resize/open/storePicture/calendar or SDK environment detection is needed. Not required for standard web display. |
| OMID / OM SDK | Relevant for in-app and supported web/video measurement. Use when verification vendors require standardized measurement. |
| SafeFrame | Relevant for web iframe-contained rich media. Test geometry, clicks, and clipping. |
| VAST | Relevant only for video-player/outstream delivery, not basic HTML5 display video. |
| GPT | Relevant for GAM web display delivery, responsive size mapping, and slot definition. |

### 11.7 Deal Packaging Recommendations

Package the RollExplore Cube as:

- "Interactive 3D rich-media display" for premium display buys.
- "Multi-message exploration unit" for product discovery campaigns.
- "3D product cube" for auto, retail, tech, and entertainment launches.
- "Face-level CTA rich media" when each cube face has unique destination tracking.

Deal notes should include:

- Approved sizes.
- Publisher placements.
- Max file weight.
- Fallback behavior.
- Tracking requirements.
- Whether video is allowed.
- Whether user-initiated expansion is allowed.
- Supported devices and excluded devices.

### 11.8 Publisher Approval Requirements

Publisher approval is required when:

- The unit uses heavy animation or video.
- The unit uses multiple third-party trackers.
- The unit expands, overlays, floats, or becomes sticky.
- The unit captures gestures in mobile/app environments.
- The unit uses face-specific multiple click destinations.
- The unit is delivered through a non-standard creative vendor.
- The unit runs in sensitive editorial categories or regulated industry campaigns.

### 11.9 Why Custom Setup May Be Required

This format may require custom template/direct integration because:

- Standard display systems do not inherently understand cube face states.
- Face-level tracking and click URLs need template-level variables.
- 3D transforms require careful iframe/SafeFrame testing.
- Mobile swipe/drag may conflict with page/app gestures.
- Performance differs widely across devices.
- Programmatic creative scanners may flag or block unapproved JS behavior unless reviewed.

---

## 12. Measurement, Viewability & Verification

### 12.1 Active View / Viewability Considerations

For GAM delivery, use Active View where supported to understand whether the served ad had an opportunity to be seen. The cube should not start autoplay rotation until it is likely in view, because autoplay outside view wastes resources and weakens engagement metrics.

Operational guidance:

- Use official ad-server/viewability reporting for billable viewability where applicable.
- Use creative-level `creative_in_view` for animation gating and internal analytics.
- Do not represent custom in-view events as independently accredited viewability unless verified by an approved measurement provider.

### 12.2 OM SDK / OMID Considerations

For mobile app and supported web/video contexts:

- Use OM SDK/OMID through the publisher SDK or verification vendor where available.
- Confirm that the ad session correctly identifies the ad view/container.
- Confirm that friendly obstructions such as controls are registered where required by the SDK/vendor.
- Test with the actual app SDK, not only a browser preview.

### 12.3 Scroll / Visibility Rules

Although the cube is not primarily scroll-triggered, it should be visibility-aware:

- Delay autoplay until the unit crosses a defined viewport threshold.
- Pause or reduce animation when out of view.
- Avoid firing face_view while the ad is offscreen.
- Resume carefully when returning to view, respecting prior user interaction.

### 12.4 Recommended KPIs

| KPI | Definition | Notes |
|---|---|---|
| CTR | Clicks / impressions | Track both global CTR and face-level CTR. |
| Interaction rate | Users with at least one interaction / impressions | Includes drag, swipe, arrow, dot, hotspot, or face click. |
| Cube rotation rate | Impressions with at least one completed rotation / impressions | Separate autoplay vs user-initiated. |
| Face view distribution | Share of active views by face | Helps optimize message order. |
| Face click rate | Face-specific clicks / face views | Stronger than overall CTR for multi-face creative. |
| Engagement time | Time user spends with active/viewable unit | Use capped or median metrics to avoid outliers. |
| Drag completion rate | Completed drag gestures / drag starts | Indicates usability and sensitivity tuning. |
| Interaction depth | Number of faces viewed per engaged user | Useful for storytelling campaigns. |
| Video completion rate | Video completes / video starts | Only when video is present. |
| Close rate | Closes / impressions | Only if close button exists. High close rate may indicate intrusiveness. |
| Fallback rate | Fallback renders / creative loads | Indicates compatibility or performance issues. |

### 12.5 Brand Lift and Attention Suitability

The format is suitable for:

- Brand lift studies where rich interaction is part of exposure quality.
- Attention measurement where viewability + time + interaction depth are used.
- Creative optimization studies comparing face order, CTA labels, and product messaging.
- A/B testing autoplay vs user-initiated modes.

It is less suitable when:

- The campaign needs only low-cost reach.
- The publisher environment heavily restricts custom JS.
- The target devices are mostly low-end or unsupported app webviews.
- The creative requires long-form video completion as the primary KPI.

---

## 13. Accessibility & User Control

### 13.1 Keyboard Accessibility

If the cube contains focusable controls, keyboard users should be able to:

- Tab to the ad controls.
- Move to next/previous face using buttons or arrow keys when focus is inside the cube.
- Activate the CTA using Enter/Space.
- Pause autoplay.
- Skip interaction and continue tabbing through the page.

Suggested controls:

```html
<button aria-label="Previous ad panel">‹</button>
<button aria-label="Next ad panel">›</button>
<button aria-label="Pause ad animation">Pause</button>
<a aria-label="Book a test drive - panel 2 of 4" href="...">Book now</a>
```

### 13.2 ARIA Labels and State

Recommended ARIA patterns:

- Use `aria-label` for arrows, dots, pause, close, and CTA.
- Use `aria-current="true"` or similar state on active face indicator.
- Announce face count in control labels, e.g. "Show panel 3 of 4".
- Do not make decorative side faces separately focusable.
- Avoid auto-announcing every autoplay rotation to screen readers because it can be disruptive.

### 13.3 Visible Close Button

A close button is optional for in-slot execution but required for expanded/fullscreen variants.

Close button requirements:

- Visible and high-contrast.
- Top-right placement unless publisher has a standard position.
- Minimum 24x24 CSS px visual size; 44x44 CSS px touch hit area preferred.
- `aria-label="Close ad"`.
- Does not fire ad click-through.

### 13.4 Reduced Motion

The creative must respect reduced-motion settings:

- Disable autoplay rotation when `prefers-reduced-motion: reduce` is detected.
- Replace 3D rotation with instant switch, fade, or flat carousel.
- Disable parallax, bounce, and continuous motion.
- Keep content and CTA fully accessible.

### 13.5 Pause / Stop Controls

If autoplay animation or video is present:

- Provide pause control where practical, especially for large units.
- Pause on hover/focus/interaction.
- Stop autoplay after limited cycles.
- Pause video when not active or not viewable.

### 13.6 Sound Control

- No forced sound.
- Audio starts muted.
- User must explicitly unmute.
- Mute/unmute control must be labeled and visible when audio is available.

### 13.7 Clear CTA Labeling

Good CTA labels:

- "Shop the collection"
- "Book a test drive"
- "Apply now"
- "Watch trailer"
- "Explore plans"
- "View offer"

Avoid:

- "Click here"
- "Continue" when it could imply publisher navigation.
- Fake system buttons.
- Misleading urgency claims.

---

## 14. Performance & Loading Strategy

### 14.1 Initial Load Strategy

Initial load should include only:

- HTML shell.
- Critical CSS.
- Minimal JS controller.
- Initial face image or poster.
- Logo if not embedded.
- Backup image reference.
- Essential tracking only.

Avoid loading all faces, videos, custom fonts, and trackers before the first render.

### 14.2 Subload / Lazy-Load Strategy

Subload after:

- Creative render is complete.
- Unit is close to viewport or in view.
- User begins interaction.
- Autoplay is about to show the next face.

Lazy-load order:

1. Current face.
2. Next likely face.
3. Remaining face images.
4. Optional video posters.
5. Optional video files only when needed.
6. Non-essential analytics.

### 14.3 Image Optimization

- Export face-specific crops for each supported size.
- Use modern formats where supported.
- Avoid oversized images scaled down in CSS.
- Use image dimensions to prevent layout shifts.
- Avoid heavy transparent PNGs for photographic faces.

### 14.4 Video Lazy Loading

- Do not preload all video faces.
- Use `preload="metadata"` or `preload="none"` depending on publisher policy.
- Load video only when face is about to become active or user requests play.
- Use poster image as default.
- Pause/unload inactive video on memory-constrained devices if needed.

### 14.5 Font Loading

- Prefer system fonts or publisher-approved web-safe fonts.
- If brand font is required, subset it and load only necessary weights.
- Avoid blocking render on font load.
- Provide fallback font stack.
- Ensure text remains inside face bounds if fallback font differs.

### 14.6 Animation Performance

Use GPU-friendly transforms:

```css
.scene {
  perspective: 800px;
}

.cube {
  transform-style: preserve-3d;
  transition: transform 700ms ease-out;
}

.face {
  backface-visibility: hidden;
}
```

Guidelines:

- Animate `transform` only for cube rotation.
- Use `opacity` for supporting fades.
- Avoid blur/filter during rotation.
- Avoid changing layout properties during drag.
- Use `requestAnimationFrame` for gesture-driven transforms.
- Monitor frame rate on low-end mobile.

### 14.7 Avoiding Layout Shift

- Publisher page must reserve slot dimensions before the ad loads.
- Creative must not change outer iframe dimensions unexpectedly.
- Fallback should occupy the same slot size.
- Expanded variants must use separate approved behavior and should not push content unpredictably.

### 14.8 Low-Bandwidth Fallback

When network is slow:

- Show backup image or initial face quickly.
- Delay loading non-visible faces.
- Avoid video autoplay.
- Use lower-resolution images for mobile.
- Disable autoplay if asset load is delayed.

### 14.9 Unsupported Browser/App Fallback

Fallback detection should consider:

- CSS 3D transform support.
- Pointer event support or touch fallback.
- SafeFrame geometry and clipping.
- App webview rendering limitations.
- Low memory/performance signals where detectable.
- Reduced motion preference.

Fallback should preserve campaign intent and click-through, even if interaction depth is reduced.

---

## 15. QA Checklist

### 15.1 Creative Rendering QA

| Check | Pass criteria |
|---|---|
| Initial face renders | First face appears within expected load time with no blank state. |
| All faces render | Every configured face displays correct image/video/text. |
| Face order correct | Face sequence matches storyboard and tracking map. |
| Cube perspective correct | No unintended flattening, skewing, or distorted geometry. |
| No face clipping | Face content remains inside slot during rotation. |
| Back faces hidden | No mirrored/reversed text appears during rotation. |
| Backup image works | Backup renders when JS/3D/assets fail. |
| Responsive scaling works | Creative fits each declared size without crop or overflow. |
| Legal/disclaimer readable | Required disclaimers are visible and legible. |

### 15.2 Interaction QA

| Check | Pass criteria |
|---|---|
| Autoplay delay | First face remains readable before rotation. |
| Autoplay speed | Rotation speed is smooth and not distracting. |
| Autoplay cycle cap | Autoplay stops or slows after configured cycles. |
| Drag sensitivity | Drag starts only after threshold; no accidental rotation. |
| Drag completion | Cube snaps to correct face after drag. |
| Swipe handling | Horizontal swipe rotates; vertical scroll still works. |
| Tap vs drag separation | Drag does not trigger click. Tap does not unintentionally drag. |
| Arrow controls | Previous/next controls work and are not hidden. |
| Dot controls | Face indicators navigate correctly. |
| CTA click | Correct destination opens for each face/global CTA. |
| Hover/focus pause | Autoplay pauses on hover/focus where implemented. |
| Reduced motion | 3D/autoplay disabled or simplified. |

### 15.3 Tracking QA

| Check | Pass criteria |
|---|---|
| Impression tracking | GAM impression and approved pixels fire once. |
| Creative loaded | `creative_loaded` fires once after ready state. |
| In-view trigger | `creative_in_view` fires only when threshold met. |
| Cube rotate | `cube_rotate` fires once per completed rotation. |
| Face view | `face_view` fires for active face with correct face ID. |
| Drag events | `drag_start` and `drag_complete` fire correctly. |
| CTA click | GAM click macro records click; custom CTA event includes face ID. |
| Video events | Start/quartile/complete/mute/unmute work if video exists. |
| Cachebuster | Tracking URLs receive unique cachebuster where required. |
| Deduplication | Events do not double-fire on repeated listeners or iframe reloads. |

### 15.4 GAM Trafficking QA

| Check | Pass criteria |
|---|---|
| Correct creative type | Custom creative/template selected appropriately. |
| Correct sizes | GAM creative sizes match booked inventory. |
| Size mapping | Responsive mapping tested at breakpoints. |
| Template fields | Required variables filled correctly. |
| Click URL | Click macro inserted and tested. |
| Backup image | Backup configured in template/creative. |
| Third-party tags | Approved and HTTPS. |
| SafeFrame | Tested in publisher-required setting. |
| Preview | Works in GAM preview and live test page. |
| Targeting | Key-values and line-item targeting correct. |

### 15.5 Mobile QA

| Check | Pass criteria |
|---|---|
| Touch swipe | Smooth horizontal swipe without page scroll conflict. |
| Tap targets | CTA and controls usable with thumb. |
| Viewport fit | No horizontal overflow or clipped controls. |
| Mobile video | Muted, inline, poster/fallback works. |
| Browser chrome | Unit remains visible and functional with address bar changes. |
| Low-end Android | No severe jank or broken rendering. |
| Orientation change | Creative handles rotation or reloads safely. |
| Reduced motion | Motion fallback works on device. |

### 15.6 Desktop QA

| Check | Pass criteria |
|---|---|
| Mouse drag | Works without text/image selection issues. |
| Hover pause | Autoplay pauses if implemented. |
| Keyboard navigation | Controls reachable and operable. |
| Browser compatibility | Chrome, Safari, Firefox, Edge tested as required. |
| Leaderboard variants | Text readable in shallow height. |
| Large billboard | Visual composition balanced and not oversized. |

### 15.7 App QA

| Check | Pass criteria |
|---|---|
| SDK rendering | Cube renders in actual app SDK/webview. |
| MRAID state | If MRAID used, state transitions behave correctly. |
| OMID | Measurement session works where required. |
| App gestures | Cube does not break app navigation or feed scroll. |
| iOS/Android parity | Both platforms tested. |
| Fallback | Flat/static fallback works in unsupported SDKs. |

### 15.8 Performance QA

| Check | Pass criteria |
|---|---|
| Initial load weight | Within publisher-approved budget. |
| Total weight | Within budget after subload. |
| Request count | Within approved request count. |
| Frame rate | Smooth on target devices. |
| CPU usage | No sustained high CPU after animation stops. |
| Memory | No leaks after repeated rotations. |
| Video load | Video does not block initial render. |
| No layout shift | Slot dimensions stable before and after render. |

### 15.9 Accessibility QA

| Check | Pass criteria |
|---|---|
| Control labels | Buttons/links have meaningful labels. |
| Keyboard | Controls usable without mouse/touch. |
| Focus visible | Focus indicator visible. |
| Reduced motion | Motion reduced when requested. |
| Pause control | Autoplay can pause or stops automatically. |
| Contrast | Text/CTA contrast sufficient. |
| Screen reader noise | Autoplay does not spam announcements. |

### 15.10 Publisher Safety QA

| Check | Pass criteria |
|---|---|
| No content blocking | Unit does not overlay editorial content unless approved. |
| No scroll trap | Page scrolling remains functional. |
| No deceptive UI | Creative does not mimic publisher/system controls. |
| No unapproved trackers | All third-party calls approved. |
| No unexpected audio | Audio starts only after user action. |
| Category compliance | Regulated content/disclaimers approved. |
| Frequency controls | High-motion/expanded variants capped where required. |

---

## 16. Common Failure Cases

| Failure case | Likely cause | Practical fix |
|---|---|---|
| Creative clipped inside iframe | Cube depth/rotation exceeds slot bounds; iframe overflow hidden. | Reduce cube size/depth, add internal padding, keep transform origin centered, test inside actual iframe. |
| Expansion blocked by SafeFrame | Attempting out-of-slot behavior without SafeFrame expansion support. | Keep execution in-slot or implement approved SafeFrame expansion/publisher custom setup. |
| Cube appears flat | `transform-style: preserve-3d` missing or app/webview flattens 3D. | Add correct CSS hierarchy; fallback to flat carousel where unsupported. |
| Back face mirrored text visible | `backface-visibility: hidden` missing. | Apply to every face and test across browsers. |
| Face z-index incorrect | Incorrect face order, stacking context, or transform composition. | Define deterministic face transforms; avoid unnecessary z-index layers; test every rotation angle. |
| Click tracking not firing | Click macro missing or URL encoded incorrectly. | Use correct GAM click macro form; test direct and nested tracker URLs. |
| CTA click fires during drag | No tap/drag threshold separation. | Suppress click after pointer movement exceeds threshold. |
| Close button hidden | Control placed outside safe area or under cube layer. | Reserve control layer with higher z-index inside slot; test all faces/states. |
| Autoplay blocked | Browser blocks media autoplay or JS starts before view. | For video, use muted autoplay; for animation, start after viewable/render event. |
| Audio starts unexpectedly | Video not muted or audio triggered by autoplay. | Force muted default; unmute only on explicit user action. |
| Mobile viewport overflow | Fixed desktop dimensions or excessive transform depth. | Use responsive CSS, max-width, and slot-specific transforms. |
| Scroll jank on mobile | Touch handlers block scrolling; heavy JS during pointermove. | Use gesture threshold, rAF, lightweight handlers, and avoid preventDefault until horizontal intent is clear. |
| Video too heavy | Video loaded upfront or too high bitrate. | Use poster first, lazy-load video, compress, and cap bitrate. |
| Third-party pixels cached | Missing cachebuster on tracking pixel. | Add GAM cachebuster macro to event/impression tracking calls. |
| Wrong size declared in GAM | Creative trafficked with unsupported slot size. | Declare only QA-approved sizes and use size mapping correctly. |
| Face images blurry | Low-res assets stretched to high-density screens. | Provide 1.5x/2x assets selectively and optimize compression. |
| Face images too heavy | All high-res faces loaded initially. | Lazy-load non-initial faces and use per-size crops. |
| Text unreadable during rotation | Copy placed near edges or rotation too fast. | Move text toward center, hold face longer, reduce perspective distortion. |
| Autoplay rotation too fast | Rotation interval/speed too aggressive. | Use 2.5-5s intervals and 500-900ms rotation duration. |
| Low-end mobile frame drops | Too many layers, filters, videos, shadows, large images. | Reduce faces/layers, disable autoplay, remove filters, use flat fallback. |
| In-app SDK not supporting interaction | SDK webview blocks events or 3D transforms. | Use MRAID/SDK-approved approach or fallback to flat/static creative. |
| Face-specific CTA wrong destination | Incorrect template variable mapping. | QA each face URL, track face ID, and validate final redirect. |
| Duplicate face_view events | Autoplay and manual controls both fire same event. | Deduplicate per face per impression, or explicitly track repeat views separately. |

---

## 17. Recommended Use Cases

| Industry | Campaign goal | Why this format fits | Example creative concept |
|---|---|---|---|
| Auto | Model exploration / test drive | Cube faces can separate exterior, interior, performance, safety, and finance offer. | A 970x250 cube showing SUV exterior, cabin tech, mileage, safety rating, and "Book a test drive" CTA. |
| BFSI | Product education / lead intent | Complex financial benefits can be broken into simple face-level messages. | Credit card cube with cashback, lounge access, fuel waiver, joining bonus, and "Apply now" CTA. |
| FMCG | Product launch / flavor discovery | Multiple variants can be explored without a large landing page. | Snack brand cube with four flavors, each face linking to "Shop now" or store locator. |
| Retail | Sale discovery / category promotion | Each face can reveal a category or offer. | Festive sale cube: fashion, electronics, home, beauty, final coupon CTA. |
| Entertainment | Trailer / character reveal | Cube can reveal characters, poster art, teaser video, release date, and booking CTA. | Movie launch 3D roll with character faces and "Watch trailer" / "Book tickets" CTA. |
| Real Estate | Project discovery / lead generation | Each face can show location, amenities, apartment type, price range, and site visit CTA. | Residential project cube: facade, clubhouse, floor plan, connectivity, "Schedule visit" CTA. |
| Travel | Destination exploration / package comparison | Faces can show destinations, itinerary, hotel, price, and booking CTA. | Travel cube with beach, mountain, city break, luxury stay, and "View packages" CTA. |
| Tech | Feature storytelling / product launch | Technical features can be chunked into digestible panels. | Smartphone cube showing camera, AI assistant, battery, display, preorder CTA. |
| QSR | Menu discovery / offer conversion | Multiple meals/offers can be shown in one compact unit. | Burger chain cube with new burger, combo meal, dessert, app discount, "Order now" CTA. |
| Consumer Durables | Feature comparison / retail push | Faces can show capacity, energy rating, smart features, warranty, and offer. | Washing machine cube: energy savings, quick wash, smart control, warranty, exchange offer CTA. |

---

## 18. Final Trafficker / Developer Handoff Summary

| Handoff area | Requirement |
|---|---|
| Required assets | Face images for each supported size, optional face videos, logo, CTA copy, backup image, optional icons/arrows/dots, legal copy if required. |
| Required dimensions | At minimum the exact booked GAM sizes. Common variants: 300x250, 300x600, 728x90, 970x250, 970x90, 320x480, 320x50, responsive slot variants. |
| Required GAM variables | `creative_variant_id`, `face_count`, `face_n_image_url`, `backup_image_url`, CTA URLs/text, `interaction_mode`, `autoplay`, `rotation_speed_ms`, `autoplay_interval_ms`, `fallback_mode`, tracking URLs, video variables if applicable. |
| Required tracking events | `impression_rendered`, `creative_loaded`, `creative_in_view`, `initial_face_view`, `cube_rotate`, `face_view`, `drag_start`, `drag_complete`, `face_click`, `cta_click`, `time_in_unit`, `fallback_rendered`; video events if video exists. |
| Required QA checks | Face clipping, z-index/face order, drag sensitivity, tap-vs-drag separation, autoplay speed/cycle cap, click tracking, face-level URLs, SafeFrame behavior, low-end mobile performance, fallback rendering. |
| Publisher-side requirements | Approved placement, approved sizes, slot height reservation, SafeFrame policy, rich-media permissions, third-party tracker approval, mobile/app SDK capability confirmation, category/legal approval where relevant. |
| Known limitations | CSS 3D support and performance vary by browser/webview; SafeFrame may clip out-of-slot transforms; low-end devices may require fallback; video on cube faces increases performance risk; programmatic delivery may require PMP/PG/direct setup and publisher approval. |
| Recommended first launch path | Start with 300x250 and 970x250 in-slot variants, 4 faces, image-only or one video face max, hybrid autoplay + user drag, flat carousel fallback, and face-level tracking. |
| Not recommended without extra approval | Fullscreen cube, sticky cube, forced expansion, auto-audio, heavy video across multiple faces, form capture inside small cube, unbounded autoplay, unapproved third-party JS. |

---

## 19. Modular Ad-Builder Configuration Schema Recommendation

For future automation across 10+ formats, the RollExplore Cube should be represented as a modular creative object rather than hard-coded HTML.

Example conceptual schema:

```json
{
  "format": "rollexplore_cube",
  "version": "1.0",
  "size": "300x250",
  "faceCount": 4,
  "interaction": {
    "mode": "hybrid",
    "autoplay": true,
    "autoplayDelayMs": 1500,
    "autoplayIntervalMs": 3500,
    "rotationSpeedMs": 700,
    "maxAutoplayCycles": 2,
    "dragEnabled": true,
    "swipeEnabled": true,
    "keyboardControlsEnabled": true,
    "reducedMotionMode": "flat_carousel"
  },
  "faces": [
    {
      "id": "face_1",
      "headline": "Explore the new launch",
      "imageUrl": "face1.webp",
      "videoUrl": null,
      "ctaText": "Learn more",
      "ctaUrl": "https://advertiser.example/launch",
      "trackingId": "hero"
    },
    {
      "id": "face_2",
      "headline": "Built for performance",
      "imageUrl": "face2.webp",
      "videoUrl": null,
      "ctaText": "See features",
      "ctaUrl": "https://advertiser.example/features",
      "trackingId": "features"
    }
  ],
  "fallback": {
    "mode": "flat_carousel",
    "backupImageUrl": "backup.jpg",
    "backupClickUrl": "https://advertiser.example"
  },
  "tracking": {
    "creativeVariantId": "cube_campaign_001",
    "interactionEndpoint": "https://tracker.example/event",
    "impressionUrl": "https://tracker.example/imp"
  }
}
```

This structure allows the same editor system to support face-based creative generation, trafficking validation, preview rendering, tracking configuration, and fallback generation.

---

## 20. Standards and Implementation References

The following public references were used to align the specification with current industry practices. They should be treated as implementation guidance, not as proof that RollExplore Cube is an official IAB standard format.

| Topic | Reference |
|---|---|
| IAB New Ad Portfolio / lightweight creative guidance | https://iabtechlab.com/standards/iab-new-ad-portfolio-guidelines/ |
| IAB display advertising guidance | https://iabtechlab.com/standards/iab-display-advertising-guidelines/ |
| IAB SafeFrame guidance | https://www.iab.com/guidelines/safeframe/ |
| IAB Open Measurement SDK / OMID | https://iabtechlab.com/standards/open-measurement-sdk/ |
| IAB VAST | https://iabtechlab.com/standards/vast/ |
| IAB OpenRTB | https://iabtechlab.com/standards/openrtb/ |
| Google Ad Manager custom creatives | https://support.google.com/admanager/answer/3180782 |
| Google Ad Manager macros | https://support.google.com/admanager/answer/2376981 |
| Google Publisher Tag ad sizes | https://developers.google.com/publisher-tag/guides/ad-sizes |
| Google Publisher Tag responsive size mapping | https://support.google.com/admanager/answer/3423562 |
| Google Ad Manager Active View | https://support.google.com/admanager/answer/3154105 |
| CSS 3D transform support concepts | https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform-style |
| CSS backface visibility | https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/backface-visibility |
| Pointer events | https://developer.mozilla.org/en-US/docs/Web/API/Pointer_events |
| High-performance CSS animation | https://web.dev/articles/animations-guide |
| Reduced motion media query | https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@media/prefers-reduced-motion |

---

## 21. Final Positioning Statement

The RollExplore Cube is best positioned as a **premium interactive 3D rich-media display unit** that can run inside standard display inventory when engineered conservatively. Its strength is multi-message exploration inside a compact slot. Its risk is performance and compatibility: CSS 3D transforms, mobile gestures, SafeFrame behavior, video-on-face rendering, and low-end device performance must all be explicitly QA-tested.

For production, the safest implementation is a **4-face image-led cube** with optional limited autoplay, user drag/swipe, clear navigation controls, face-level CTA tracking, flat carousel fallback, and a static backup image. Expanded, sticky, fullscreen, video-heavy, or gamified variants should be treated as separate high-impact executions requiring additional publisher approval and QA.
