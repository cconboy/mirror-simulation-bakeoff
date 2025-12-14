You are an engineering and graphics-focused assistant. Build a single-file HTML page (one .html file with embedded CSS and JavaScript, no external libraries) that provides an interactive 2D top-down simulation for configuring two side pivot mirrors around an existing makeup mirror so a seated person can see the back of her head.

Output only the complete .html file contents.

View orientation
	•	Top-down view only.
	•	The back wall with the current central mirror is at the bottom of the canvas.
	•	The short wall is on the left, extending upward from the bottom-left corner.

Fixed geometry (not user-modifiable)

These are constants in the simulation. Do not provide controls to change them.
	•	Desktop: 20 in deep x 29 in wide
	•	Central fixed mirror on the bottom wall: 23 in wide x 29 in tall
	•	Corner constraints:
	•	Left short wall extends 11 in from the bottom wall
	•	Distance from the left edge of the central mirror to the short wall is 7 in
	•	Right side is open (no wall).

Fixed person model (not user-modifiable)

Do not provide controls for head size/shape or eye position.
	•	Model the head as an exquisitely beautiful but statistically typical human head (use typical head width/depth and a typical seated eye position in plan view).
	•	The person can rotate her head (yaw). Include this as a simulation degree of freedom. You may either:
	•	Treat head yaw as something the solver can vary automatically to achieve visibility, or
	•	Provide a single “Head turn angle” control. This is allowed even though head size/eyes are fixed.

Mirror product defaults (use real specs)

Default the side mirrors to match this specific product (use these values as the default mirror parameters and mention them in the UI as “Default product spec”):
Winston Porter “Corrente Pivot-N-View Squared Cornered Rectangle Mirror for Window Bathroom Vanity” on Wayfair Canada.

From the product page:
	•	Overall: 26” H x 16” W x 3” D  ￼
	•	Mirror (reflective area): 22” H x 14” W  ￼
	•	Glass thickness: 0.16”  ￼
	•	Weight: 7.89 lb  ￼

Pivot and offset modeling requirement:
	•	The simulation must model that the mirror is mounted on the bottom wall (back wall) only.
	•	Use the overall-vs-mirror width difference to infer pivot hardware footprint:
	•	Overall width 16” vs mirror width 14” implies about 1” per side for pivot grommets/hardware.  ￼
	•	Model the pivot axis for each mirror as being located at the wall attachment points near the left and right edges of the overall width (use the inferred 1” margin).
	•	Model the mirror as rotating in plan view around that pivot axis.

If any pivot detail is missing, make a reasonable explicit assumption in a small “Assumptions” box inside the UI.

Simplifications
	•	One plane only (top-down). No height modeling.
	•	Remove any controls for vertical tilt, height, or pitch.
	•	Mirrors are ideal planar reflectors.

Constraints
	•	Both side mirrors are attached to the bottom wall (the same wall as the central mirror).
	•	The left short wall constrains the left mirror’s pivot range: it cannot rotate “through” the wall. Implement an angular limit so the mirror cannot intersect the wall region in plan view.
	•	The right mirror has no side-wall constraint, but it still cannot rotate into the back wall (no self-intersection with the wall line).

What “works” means

The simulation should indicate when the configuration allows the user to see the back of her head, given:
	•	She can look into mirrors other than the central mirror (so the “eye gaze direction” can be toward either side mirror or the central mirror as needed).
	•	She can rotate her head (yaw) to bring the back-of-head region into the reflection chain.

Define a target set of points representing the “back of head” in plan view (for example an arc on the rear of the head). A configuration “passes” if at least one valid reflection path exists from the eyes to enough target points (define a threshold and show coverage percentage).

At minimum, evaluate reflection paths including:
	•	Eye → Left side mirror → Central mirror → Back-of-head target
	•	Eye → Right side mirror → Central mirror → Back-of-head target
Also allow direct gaze to a side mirror first if that yields a valid chain (document what you implement).

Interactive UI requirements
	•	Use <canvas> for drawing.
	•	Live update as controls move.
	•	Provide a prominent PASS/FAIL indicator plus a coverage score.
	•	Show rays:
	•	Successful rays in green
	•	Failed rays in red
	•	Show the head, eyes, mirrors, and walls clearly.

Controls (must stay visible without scrolling):
	•	Left mirror: position along bottom wall (x), mirror width (reflective), yaw angle
	•	Right mirror: position along bottom wall (x), mirror width (reflective), yaw angle
	•	Optional single control: head turn angle (yaw), if you choose not to auto-solve it
	•	Reset to defaults button
	•	Keep the key mirror controls in a fixed panel beside or above/below the canvas so I do not have to scroll to adjust mirror position/size/tilt.

Note: Wall positions and dimensions are fixed. Head size/shape/eye position are fixed.

Implementation details
	•	Single HTML file with inline CSS/JS.
	•	Clean code structure:
	•	Geometry model for walls, mirrors (as segments), head (circle/ellipse), eyes (point)
	•	Reflection math and ray intersection with mirror segments
	•	Constraint logic (angle limits due to left wall, mirror-wall intersection checks)
	•	A scoring function for “coverage” over multiple back-of-head target points
	•	Add concise comments explaining the reflection math approach.

Defaults must try to work

On load, choose mirror x positions and yaw angles that are likely to PASS (even if approximate), then let me tweak from there.
