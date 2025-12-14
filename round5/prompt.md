
Prompt: Build a browser-based simulation to validate a three-mirror makeup station design

You are an engineering- and geometry-focused assistant.

Your task is to design and implement a simple but accurate interactive simulation that helps me determine whether proposed changes to a makeup station will allow a seated person to see the back of her head while styling her hair.

The simulation must model mirror placement, pivot angles, line-of-sight reflections, and space constraints, and must clearly indicate whether the configuration works or not.

The final output must be a single self-contained HTML file that I can open locally in a browser.
No external libraries, no build steps, no external assets.

⸻

Goal

I want to add two pivoting mirrors, one on each side of an existing central mirror, so my wife can see the back of her head while seated at her makeup station.

Before purchasing and installing these mirrors, I want to know if:

• The mirror dimensions
• The pivot geometry
• The wall and desk constraints
• The allowable mirror angles

will actually allow a clear reflective path from the back of her head to her eyes.

The simulation should answer this visually and unambiguously.

⸻

View and Coordinate System

• Top-down 2D view only
• The back wall is at the bottom of the canvas
• The seated person faces downward toward the bottom wall
• The central mirror is mounted on the back wall
• A short side wall exists on the left
• The right side is open

No perspective or 3D rendering required. This is a planar optics problem.

⸻

Fixed Geometry (Not User-Modifiable)

These are constants in the simulation.

Desk

• Width: 29 inches
• Depth: 20 inches
• Desk is placed in the corner formed by the back wall and the short side wall

Walls

• Back wall is horizontal at bottom
• Left side wall extends 11 inches upward from the back wall
• Distance from the left edge of the central mirror to the side wall is 7 inches
• No wall on the right side

Existing Central Mirror

• Mounted flush on the back wall
• Width: 23 inches
• Treated as a flat vertical mirror perpendicular to the wall

⸻

Proposed Side Mirrors

I am planning to buy this mirror model:

https://www.wayfair.ca/decor-pillows/pdp/winston-porter-corrente-pivot-n-view-squared-cornered-rectangle-mirror-for-window-bathroom-vanity-c009207780.html

You should retrieve mirror dimensions from this page and use them as defaults.

Important mounting and pivot details:

• Each mirror is wall-mounted on the back wall
• Each mirror pivots about a vertical axis through its center
• Mount arm is perpendicular to the wall
• Mirror edge offset from wall: 4 inches
• Pivot axis offset from wall: 15 inches
• Mirror yaw can rotate left or right but cannot pass through walls
• Mirrors must stay within the available wall space

Assume reflective surface faces inward toward the seated person.

⸻

Person Model

The head should be modeled as:

• Statistically typical adult human head size
• Opaque
• Circular or elliptical approximation is acceptable

Additional assumptions:

• She can lean forward so the front of her head is ~10 inches from the central mirror
• Eye position should be realistic relative to head center
• She can rotate her head and direct her gaze toward any mirror

She is exquisite and beautiful, but this has no bearing on geometry.

Do not provide controls for head size or eye anatomy. Those are fixed.

⸻

Simulation Requirements

Interactivity

The simulation must allow:

• Adjusting yaw angle of each side mirror
• Adjusting horizontal position of each side mirror along the back wall
• Adjusting head position within reasonable seated limits
• Optional head rotation or gaze direction

Controls should be on screen and immediately responsive.

⸻

Optics Logic

The simulation must:

• Trace line-of-sight rays
• Apply law of reflection correctly
• Determine whether a ray can travel:
back of head → side mirror → central mirror → eyes
or equivalent valid paths

Approximate ray tracing is acceptable if it is geometrically honest.

⸻

Success Criteria

The simulation must clearly indicate whether the current configuration works.

At least one of the following should be present:

• A PASS / FAIL indicator
• Highlighting of visible posterior head region
• Coverage percentage of back-of-head visibility
• Rays drawn in green when valid, red when blocked

The user should immediately understand if the setup is viable.

⸻

Defaults and Starting State

The simulation should attempt to initialize itself in a working configuration if one exists:

• Mirrors positioned and angled plausibly
• Head positioned naturally
• Some posterior visibility achieved at load time

If no valid configuration exists under constraints, say so clearly.

⸻

Output Requirements

• Output only the full HTML file contents
• Include a comment at the top explaining:
– What the simulation does
– How to use the controls
– What PASS / FAIL means

No markdown. No explanation text outside the file.

⸻

Design Philosophy

This is not about photorealism.
It is about answering a real physical question before drilling holes in a wall.

Favor:

• Clear geometry
• Honest constraints
• Visual truth over visual polish

If simplifying assumptions are made, document them in comments.

⸻

