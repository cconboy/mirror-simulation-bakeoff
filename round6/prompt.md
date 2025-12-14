
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

No perspective or 3D rendering is required. This is a planar optics problem.

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

Use the following explicit dimensions and mechanics for the side mirrors.

Mirror Geometry

• Overall mirror assembly width: 16 inches
• Reflective surface width: 14 inches
• One surface only is reflective
• Reflective surface is oriented inward toward the makeup station

Pivot and Mount

• Each mirror is mounted on the back wall
• Mirror pivots about a vertical axis through its center
• Pivot axis offset from wall:
– Half reflective width: 7 inches
– Plus mounting bracket offset: 2 inches
– Total pivot offset from wall: 9 inches

• Mirror edge closest to the wall will therefore be closer than the pivot axis
• Pivot allows a full 360-degree rotation
• Mirror yaw is unconstrained mechanically but constrained spatially

Constraints

• Mirrors cannot pass through walls
• Mirrors must remain within the available back-wall mounting span
• Mirror rotation must respect collision with the left side wall

⸻

Person Model

The head should be modeled as:

• Statistically typical adult human head size
• Opaque
• Circular or elliptical approximation is acceptable

Additional assumptions:

• She can lean forward so the front of her head is approximately 10 inches from the central mirror
• Eye position should be realistic relative to head center
• She can rotate her head and direct her gaze toward any mirror

She is exquisite and beautiful, but this has no bearing on geometry.

Do not provide controls for head size or eye anatomy. Those are fixed.

⸻

Simulation Requirements

Interactivity

The simulation must allow:

• Adjusting yaw angle of each side mirror
• Adjusting horizontal mounting position of each side mirror along the back wall
• Adjusting head position within reasonable seated limits
• Optional head rotation or gaze direction

Controls should be visible without scrolling and respond immediately.

⸻

Optics Logic

The simulation must:

• Trace line-of-sight rays
• Apply the law of reflection correctly
• Determine whether a ray can travel:
back of head → side mirror → central mirror → eyes
or any equivalent valid reflective path

Approximate ray tracing is acceptable as long as it is geometrically correct and consistent.

⸻

Success Criteria

The simulation must clearly indicate whether the current configuration works.

At least one of the following must be present:

• PASS / FAIL indicator
• Highlighting of visible posterior head regions
• Coverage percentage of back-of-head visibility
• Rays drawn in green when valid and red when blocked

The result should be immediately understandable without interpretation.

⸻

Defaults and Starting State

The simulation should attempt to initialize in a plausible working configuration if one exists:

• Mirrors positioned and angled reasonably
• Head positioned naturally
• Some posterior head visibility achieved on load

If no valid configuration exists under the constraints, state this clearly in the UI.

⸻

Output Requirements

• Output only the full HTML file contents
• Include a comment at the top explaining:
– What the simulation does
– How to use it
– How success or failure is determined

No markdown. No explanatory text outside the HTML file.

⸻

Design Philosophy

This is not about photorealism.
It is about answering a real physical question before drilling holes in a wall.

Favor:

• Correct geometry
• Honest constraints
• Visual truth over polish

If simplifying assumptions are made, document them in comments.

⸻

