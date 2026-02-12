# AtmosPINN Lab – Physics‑Informed AI for Atmospheric Inference

AtmosPINN Lab is a single‑page demo web app that showcases your project:

> **“Physics‑Informed AI for Atmospheric Inference and Aerodynamic Decision‑Making Using Model Rockets.”**

The interface lets you enter (or load example) model‑rocket flight data and then visualizes a **mocked physics‑informed neural network (PINN)** inference of vertical atmospheric profiles (effective density and cross‑wind) along with **apogee prediction error vs. a physics‑only baseline**.

This is designed as a **presentation‑ready product** you can demo live.

---

## 1. Quick Project Summary (for your slides)

- **Problem**: Standard rocket simulations assume simplified atmospheres (standard density, uniform wind), but real flights experience changing wind shear and density with altitude. This mismatch causes **apogee prediction errors** and weakens design and launch decisions.
- **Idea**: Treat each rocket flight as an **atmospheric sensing experiment**. Use a **physics‑informed neural network (PINN)** that combines the equations of motion with telemetry (altitude, IMU data, motor info) to reconstruct **altitude‑dependent atmospheric behavior**.
- **Method**:
  - Inputs: time, altitude, velocity/acceleration from IMU, mass and motor class.
  - Constraints in the loss: Newton’s second law, drag proportional to density and velocity², static stability, continuity of motion.
  - Output: inferred profiles of **effective wind and density vs. altitude**, and corrected trajectory predictions.
- **Result**: The PINN explains the gap between ideal simulations and measured flights, **reduces apogee prediction error** vs. physics‑only models, and turns model rockets into **passive atmospheric probes**.

Use this wording directly on your **title / overview slides**.

---

## 2. How to Run the Demo

No build tools are required – this is a plain HTML file with CDN‑loaded JavaScript.

### Option A – Easiest (double‑click)

1. Open the project folder: `Aerospace-Pinn/`.
2. Double‑click `index.html` to open it in your browser (Chrome recommended).

> For presentations, prefer running via a local server (Option B) so Chart.js and fonts load consistently.

### Option B – Run with a lightweight static server

If you have Node.js installed:

```bash
npx serve .
```

Then open the printed `http://localhost:PORT` URL and navigate to `index.html`.

---

## 3. Demo Script for Saturday

Suggested 5–7 minute flow:

1. **Context (30–45s)**
   - “Aerodynamic performance depends heavily on the atmosphere, but we rarely know the true wind and density profile during a flight.”
   - “Most tools assume a standard atmosphere or uniform wind, which causes the gap between predicted and actual apogee.”

2. **Idea (45–60s)**
   - “Instead of assuming the atmosphere, I use a physics‑informed neural network that works backwards from flight data.”
   - “Telemetry plus Newton’s laws allow the network to infer what the wind and density must have been with altitude.”

3. **Show the Web App (3–4 min)**
   - Scroll to the **hero** and read the one‑sentence explanation.
   - Jump to **‘Interactive Demo – Explore inferred atmosphere from model rocket flights’**.
   - Click a preset (e.g. *Windy day shear*), then hit **‘Run PINN‑style inference’**.
   - Talk through what updates:
     - The **chart**: density and cross‑wind vs. altitude.
     - The **apogee cards**: physics‑only vs. PINN‑enhanced vs. observed.
     - The **error reduction** metric.
   - Emphasize that in the real system, the curves come from a PINN trained with physics‑based loss terms; here they are **qualitatively realistic mock outputs** for presentation.

4. **Wrap‑up (30–45s)**
   - “Model rockets become atmospheric probes.”
   - “Physics‑informed AI lets us learn hidden environmental variables, not just fit trajectories.”
   - “This framework can extend to higher‑altitude rockets and UAVs for robust decision‑making under uncertainty.”

---

## 4. Files in This Project

- `index.html` – The full **UI and demo logic** in a single file:
  - Modern dark‑mode hero section with project branding.
  - Executive summary + talk‑track section you can use as notes.
  - Interactive demo panel with inputs and a Chart.js visualization.
- `README.md` – This guide (summary + run + demo script).

---

## 5. Customizing for Your Own Flights

The current JavaScript in `index.html`:

- Uses your inputs (mass, motor class, apogee, acceleration, ground wind, static margin).
- Computes a **baseline apogee** using a simplified physics‑inspired formula.
- Generates a **“PINN‑enhanced” apogee** that is closer to the observed value.
- Synthesizes a smooth, realistic‑looking **density and cross‑wind profile** vs. altitude.

To plug in real flights:

1. Type the values from your flight log or altimeter report into the form.
2. Run the inference and refer to the updated cards/plot as a **visual explanation** of what your real PINN does.
3. You can tweak the formulas inside `runInference()` to better match your real results.

---

## 6. Next Steps (If You Want to Extend It)

- Hook this UI up to a **backend PINN model** (Python/PyTorch, etc.) via an API endpoint.
- Add support for **multiple flights** on the same plot to compare different days or designs.
- Export inferred profiles as CSV so they can be fed back into simulation tools.

