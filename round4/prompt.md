


You are an engineering and graphics-focused assistant. Build a single-file HTML page (one .html file with embedded CSS and JavaScript, no external libraries) that provides an interactive 2D top-down simulation for configuring two pivot mirrors around an existing makeup mirror so a seated person can see the back of her head.

Output only the complete .html file contents.

View orientation
	•	Top-down view only.
	•	The back wall with the central mirror is at the bottom of the canvas.
	•	The short wall is on the left, extending upward from the bottom-left corner.

Fixed geometry (not user-modifiable)

No controls for walls or desk geometry. These are constants:
	•	Desktop: 20 in deep x 29 in wide
	•	Central fixed mirror: 23 in wide x 29 in tall mounted on the back wall (bottom)
	•	Left short wall extends 11 in from the back wall
	•	Distance from the left edge of the central mirror to the short wall is 7 in
	•	Right side is open (no wall)

Fixed person model (not user-modifiable)

No controls for head size/shape or eye position.
	•	The head is beautiful and opaque (treat it as a solid occluder in the 2D plane).
	•	Use a “statistically typical” head in plan view (typical width and depth) and a typical seated eye position.
	•	The head center is positioned so the head is 10 inches away from the back wall (distance from back wall to the nearest point or to head center, choose one and document it clearly in an on-page “Assumptions” note).
	•	She can turn her head (yaw). You may either:
	•	Auto-solve head yaw to maximize visibility, or
	•	Provide a single “Head yaw” slider (allowed even though other head properties are fixed).
	•	She can gaze into mirrors other than the central mirror, so the simulation should not assume her gaze must be into the center mirror first.

Mirror product defaults (must match the specified Wayfair mirror)

Default each side mirror to match this product’s published dimensions:

Winston Porter “Corrente Pivot-N-View Squared Cornered Rectangle Mirror for Window Bathroom Vanity” (Wayfair Canada)

Published specs:
	•	Overall: 26” H x 16” W x 3” D  ￼
	•	Mirror (reflective area): 22” H x 14” W  ￼
	•	Glass thickness: 0.16”  ￼
	•	Product weight: 7.89 lb  ￼
	•	Description notes “overall (includes pivot grommets) … excludes pivot grommets … 22 by 14” and mentions 360° adjustability.  ￼

Pivot modeling requirement (important)
For this simulation, model each side mirror as:
	•	Mounted on the back wall (bottom wall) only.
	•	Offset from the wall by mounting brackets.
	•	Having a pivot point in the center of the mirror (center-pivot assumption requested by the user).

Also include a small on-page “Assumptions” note that the product page references “pivot grommets” and “tilt” but does not clearly specify center-pivot geometry, so the simulation is implementing a center-pivot bracket model as a design assumption for exploration.  ￼

Simplifications
	•	One plane only (top-down).
	•	No height modeling.
	•	No vertical tilt, pitch, or elevation controls.
	•	Mirrors are ideal planar reflectors.

Constraints
	•	Both side mirrors must be attached to the back wall (bottom wall).
	•	The left short wall constrains the left mirror’s yaw. It cannot rotate into or through the wall. Enforce this by clamping yaw to a safe range and/or preventing any configuration where the mirror segment intersects the wall region.
	•	Mirror yaw controls must allow -180° to +180° (but physically invalid ranges should be rejected or clamped, especially for the left mirror).
	•	Reflective surfaces should be oriented toward the subject by default (choose initial yaw angles that face inward).

What “works” means

Define a set of target points along an arc representing the back-of-head region. A configuration passes if, for at least one allowed head yaw (or the chosen head yaw), there exists a valid reflection path from the eyes to enough target points without missing mirror surfaces and without being blocked by walls or occluded by the opaque head.

Because she can gaze at mirrors other than the center mirror, consider paths including:
	•	Eye → left side mirror → central mirror → back-of-head target
	•	Eye → right side mirror → central mirror → back-of-head target
	•	Eye → central mirror → left side mirror → back-of-head target
	•	Eye → central mirror → right side mirror → back-of-head target
	•	Eye → side mirror → back-of-head target (direct, if it geometrically works and is meaningful)

Document exactly which paths you implement.

Interactive UI requirements

Use <canvas> for drawing. Live update as controls move. Provide:
	•	Prominent PASS/FAIL indicator
	•	Coverage score (percent of target points visible)
	•	Rays drawn on the canvas:
	•	Successful paths in green
	•	Failed attempts in red
	•	Clear drawing of walls, desk, central mirror, head, eyes, and both side mirrors.

Controls (keep key controls always visible, no scrolling)
A fixed control panel must keep these always on-screen:
	•	Left mirror: mount position along back wall (x), yaw (-180 to +180)
	•	Right mirror: mount position along back wall (x), yaw (-180 to +180)
	•	Optional: Head yaw (or an “auto-solve head yaw” toggle)
	•	Reset to defaults button

Advanced controls (hidden by default)
Mirror dimensions must be in an “Advanced” collapsible section:
	•	Mirror reflective width/height (defaults from product spec)
	•	Overall width/height (defaults from product spec)
	•	Bracket offset from wall (default to something reasonable if not specified, and label it as an assumption)
	•	Any other rarely-touched parameters

Defaults must try to work

On load, choose mirror mount positions and yaw angles that are likely to PASS given the fixed head position (10” from back wall) and the left-wall constraint. If you add an auto-solve mode, default it to on and show the chosen yaw angles.

Implementation details

Single HTML file with inline CSS/JS. Clean code with comments:
	•	Geometry model for walls, mirrors (segments), head (circle/ellipse), eyes (point)
	•	Reflection math and segment intersection
	•	Occlusion checks: walls block rays; opaque head can block rays
	•	Constraint logic for yaw limits due to left wall
	•	Coverage scoring over multiple back-of-head target points

Deliverable

Output only the complete contents of the .html file, ready to save and open locally.

⸻

