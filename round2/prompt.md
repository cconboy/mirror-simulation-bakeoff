

You are an engineering and graphics-focused assistant. Build a single-file HTML page (one .html file with embedded CSS and JavaScript, no external libraries) that provides an interactive simulation for configuring two pivot mirrors on either side of an existing makeup mirror so a seated person can see the back of their head.

At the top of the HTML file include a comment describing what the page does and how to use it.

⸻

Simulation Setup (Geometry and Environment)
	1.	Top-down view orientation
	•	The wall with the current central mirror is located at the bottom of the top-down view.
	•	The short wall that extends 11 inches is located on the left side of the view.
	2.	Existing makeup station
	•	Central fixed mirror: 23 in wide x 29 in tall mounted on the bottom wall.
	•	Desktop: 20 in (depth) x 29 in (width).
	•	Desk placed in a corner:
	•	Back wall (bottom)
	•	Short wall (left) extends 11 in from the back wall.
	•	Distance from the edge of the central mirror to the short wall is 7 in.
	•	Right side is open (no wall).
	3.	User’s head
	•	Model the head as an exquisitely beautiful but statistically typical human head.
	•	Include typical head width, depth, and eye position.
	•	Provide controls to adjust eye height slightly but default should approximate typical seated eye height.

⸻

Side Mirror Option (Default)

Retrieve and use the dimensions and details for the pivot mirror from the product at:

https://www.wayfair.ca/decor-pillows/pdp/winston-porter-corrente-pivot-n-view-squared-cornered-rectangle-mirror-for-window-bathroom-vanity-c009207780.html?piid=1993632662

Use the real mirror specs as defaults in the UI (e.g., reflective surface size, overall size). Include:
	•	Reflective surface width and height
	•	Overall width and height
	•	Pivot mount properties
If the product page includes any tilt limitation or pivot axis info describe assumptions clearly.

⸻

Interactive Requirements

The HTML must provide an interactive UI that:
	1.	Displays a clear top-down diagram of:
	•	Walls (bottom and left)
	•	Desk surface
	•	Central mirror
	•	Head/eye position
	•	Two side mirrors
	2.	Live adjustment controls (always visible without scrolling) for both side mirrors:
	•	Horizontal position (x offset from central mirror)
	•	Vertical position (y offset from the desktop or floor)
	•	Mirror size (width & height)
	•	Tilt angles
	•	Yaw: pivot left/right
	•	Optional pitch: tilt up/down
	•	Controls should be sliders with numeric displays.
	3.	Simulation logic
	•	Use simple 2D ray tracing in the top-down plane to simulate whether the eye can see the back of the head via reflection paths.
	•	At minimum consider these paths:
	•	Eye → Side Mirror → Central Mirror → Back-of-Head
	•	Eye → Central Mirror → Side Mirror → Back-of-Head (if applicable)
	•	Apply the law of reflection for each mirror interaction.
	•	Include wall blocking checks (walls block rays behind them).
	•	Provide real-time feedback: show rays on the canvas, coloring them green for successful paths and red for rays that miss.
	4.	Indicators
	•	A prominent PASS / FAIL indicator showing whether the current mirror setup lets the eye see the back of the head.
	•	Optionally a coverage score representing how many target points on the back of the head are visible.
	•	Graphical overlays to visualize coverage arcs on the head region (if applicable).
	5.	Default initial configuration
	•	Try to pre-set the default mirror positions, sizes, and angles to a configuration that should work so the PASS indicator is true on load.

⸻

UI Layout and Behavior
	•	Key controls for mirror adjustments should be:
	•	Placed in a fixed panel adjacent to or below the canvas
	•	Always visible without scrolling (use a responsive layout)
	•	Include:
	•	Labels and real-time numeric values for slider controls
	•	A Reset Defaults button that returns all controls to the initial working setup
	•	Tooltips or small help text explaining each control

⸻

Implementation Details
	•	Use a <canvas> or SVG for drawing the top-down view.
	•	Include all CSS and JS inline so this is a single .html file.
	•	Write clean, commented code that includes:
	•	Geometry and reflection math functions
	•	Head, mirror, and wall models
	•	Ray intersection and visibility checks
	•	UI event handlers
	•	Use clear variable names (e.g., mirrorLeftYaw, mirrorRightPosX, eyeHeight).

⸻

Deliverable

Output only the complete contents of the .html file, ready for me to open in a browser and interact with immediately.

The HTML should be self-contained and require no external resources.

