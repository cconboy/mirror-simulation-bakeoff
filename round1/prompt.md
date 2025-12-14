**Updated Prompt: Generate a single-file interactive HTML simulation**



You are an engineering-focused assistant. Build me a **single-file HTML page** (one .html file with embedded CSS and JavaScript, no external libraries) that provides an **interactive geometry + reflection simulation** for a three-mirror makeup/hair station.





## **Goal**





Help me choose the **size, position, and angles** of two side mirrors so that a seated person can see the **back of their head** (and ideally sides and crown) using reflections between mirrors.



The page must let me adjust parameters with sliders/inputs and must **clearly indicate when the current configuration works** (for example: a “PASS/FAIL” indicator, a coverage percentage, and/or green/red highlights on a target region representing the back of the head).





## **Start by simulating this specific mirror option**





Assume each side mirror could be a **wall-mounted pivot mirror** similar to “Pivot-N-View” style:



- Overall approx: **26 in H x 16 in W**
- Reflective surface approx: **22 in H x 14 in W**
- Mounted on a **vertical pivot** so it can rotate left-right (yaw). Allow optional up-down tilt (pitch) as a parameter too.





Treat these as defaults that I can modify in the UI.





## **Known station dimensions and constraints**





- Central fixed mirror: **23 in wide x 29 in tall**, mounted on back wall facing the user

- Desktop: **20 in (depth) x 29 in (width)**

- Desk is in a corner:

  

  - Back wall behind central mirror

  - One side has a **short wall** perpendicular to the back wall:

    

    - Short wall extends **11 in** outward from the back wall
    - Distance from the edge of the central mirror to the short wall is **7 in**

    

  - The other side is open (no wall)

  







## **Model assumptions (make them explicit in the UI)**





- Use a simple 2D top-down model first (plan view) for primary ray paths, plus an optional side view for vertical coverage.

- Include adjustable “user” parameters:

  

  - Eye position (x, y, and optionally height)
  - Head radius/size
  - “Back of head target point(s)” to test visibility (at least one point centered on the back of the head, ideally a small arc/region)

  

- Mirrors are ideal planar reflectors.







## **What the simulation must do**





1. Render a **top-down diagram** of the setup (walls, desk footprint, central mirror, side mirrors, head, eyes).

2. Let me interactively adjust for each side mirror:

   

   - Mount position (x, y) within allowed constraints
   - Mirror width/height (or reflective width/height)
   - **Yaw angle** (left-right pivot)
   - Optional pitch angle (up-down tilt) if you include vertical modeling

   

3. Compute ray paths and determine whether the eye can see the **back-of-head target** via reflections:

   

   - At minimum, test the path: **eye → side mirror → central mirror → back-of-head target** and/or **eye → central → side → target** (choose a consistent reflection order and document it).
   - If you implement both orders, even better.

   

4. Determine “works” based on whether at least one valid reflected path exists **without missing mirror surfaces** and without being blocked by walls.

5. Provide a clear indicator:

   

   - Large “PASS/FAIL” status
   - Optional “coverage” score based on how many target points on the back-of-head region are visible
   - Show working rays in green and failing rays in red

   







## **UI requirements**





- All controls on the page (sliders + numeric inputs)
- A “Reset to defaults” button
- A “Show advanced controls” toggle (for head/eye parameters, pitch, etc.)
- Live update as controls move
- Units in inches







## **Implementation details**





- Single HTML file with inline CSS/JS

- Use <canvas> for drawing

- Include clean code structure:

  

  - Data model for geometry
  - Reflection math functions
  - Intersection checks (ray with mirror segment)
  - Simple wall blocking checks

  

- Provide comments explaining the reflection math (law of reflection via vector reflection across mirror normal, or equivalent geometric method).







## **Deliverable**





Output only the complete contents of the .html file, ready for me to save and open locally in a browser.



Include a short instruction comment at the top of the HTML explaining what the simulation does and how to use it.
