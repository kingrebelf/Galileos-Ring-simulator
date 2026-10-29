# Galileo's Ring Simulator

An interactive, top-down pendulum-ring experiment inspired by [Galileo's Ring II](https://www.youtube.com/shorts/l1rYPY-dCAk). Watch pendulums of different lengths fall in and out of alignment, and explore the patterns made by repeating those lengths around a circle.

The simulator is a single HTML file, with its interface, styles, and application code together. It uses Three.js for rendering and runs entirely in your browser; it does not require a build step or an account.

## Requirements

- A modern browser with JavaScript and WebGL enabled (for example, a current version of Chrome, Edge, Firefox, or Safari).
- An internet connection to load Three.js 0.160.1 from jsDelivr when the page opens. The HTML file itself contains the rest of the application.
- Git is optional; it is only needed for the clone method below. Python is optional for the local server method.

## Installation and opening

### Option 1: Download the file

1. On the GitHub repository page, select **Code → Download ZIP**.
2. Extract the ZIP archive.
3. Open `index.html` in your browser. The simulation starts automatically at real-time speed.

Alternatively, download `index.html` by itself from the repository and open it in a browser.

### Option 2: Clone the repository

```sh
git clone https://github.com/kingrebelf/Galileos-Ring-simulator.git
cd Galileos-Ring-simulator
```

Open `index.html` in your browser. No package installation or compilation is needed.

### Option 3: Run a local web server

If your browser or local security settings prevent the file from working directly, start a server from the repository directory:

```sh
python -m http.server 8000
```

On Windows, `py -m http.server 8000` may be used instead. Visit [http://localhost:8000](http://localhost:8000), and press `Ctrl+C` in the terminal to stop the server. If port 8000 is in use, choose another port in both the command and URL.

## Using the simulator

The pendulums begin swinging together as soon as the page opens. Use the controls on the left to change the arrangement:

| Control | Effect |
| --- | --- |
| **Pendulums** | Sets how many bobs are spaced around the ring, from 6 to 120. |
| **Length steps** | Sets the number of length levels in each repeated sequence, from 1 to 48. Depending on the pendulum count and repeated sections, not every level may have a bob. |
| **Repeated sections** | Repeats the length sequence 1 to 12 times around the ring. For evenly matched sections, choose a pendulum count divisible by this number. |
| **Longest length** | Sets the maximum pendulum length, from 0.5 to 5 meters. |
| **Length difference** | Sets how much shorter the shortest length is than the longest, from 0% to 70%. For example, 2.5 m and 30% produce a shortest length of 1.75 m. With one length step, all bobs use the longest length. |
| **Release angle** | Sets the common starting angle, from 3° to 40°. |
| **Simulation duration** | Sets the end of the timeline, from 10 to 600 simulated seconds. |
| **Show motion trails** | Shows or hides short traces of recent motion. |
| **Show swing paths** | Shows or hides the radial guide for each bob. |

Changing an arrangement setting returns the simulation time to zero while preserving whether playback is paused. Changing the duration retains the current time unless it is beyond the new endpoint, in which case the time is clamped to the endpoint.

The controls below the view manage playback:

- **Pause / Play** stops or resumes the simulation. If the timeline has reached its end, Play starts again from zero.
- **Reset** returns to zero and starts playback.
- Drag the **timeline** to inspect any point in the selected duration, including while paused.
- Choose **Playback** speed from 0.1× through 25×. The default 1× advances one simulated second per real second; 2× advances twice as fast, and 0.5× at half speed. Playback stops at the selected duration.

For a first experiment, leave the defaults at 48 pendulums, 16 length steps, and 3 repeated sections. Increase playback to 5× and watch the three repeated sectors change shape. Try a single length step to make all pendulums move together, or increase the length difference to make their phases separate faster.

## Model and limitations

Each pendulum is independent and begins at the same release angle with zero initial velocity. The model uses the ideal, undamped small-angle approximation:

```text
angular frequency ω = √(g / L)
period T = 2π√(L / g)
angle θ(t) ≈ θ₀ cos(ωt)
```

Here `L` is length in meters and `g` is 9.81 m/s². Shorter lengths therefore oscillate faster. The top-down display maps each bob to a radial line and uses a visual scaling factor for its displacement. Trails are short sampled visual traces, not a recorded history.

This is a visualization, not a precision physics tool: the small-angle approximation becomes less accurate at larger release angles, and the model omits friction, air resistance, collisions, coupling, and variations in gravity. Repeated sections produce exact rotational repetition when the pendulum count divides evenly by the section count.

## Troubleshooting

- **The ring does not appear and a Three.js error is shown:** check your internet connection and access to `cdn.jsdelivr.net`, then reload the page. The file loads Three.js from that CDN.
- **The page is blank or rendering fails:** enable JavaScript and hardware acceleration/WebGL in your browser, update the browser, and try the local web server instructions above.
- **The pendulums seem stationary:** check whether playback is paused, the timeline has reached its end, or the speed is set very low. Press Reset to restart.
- **The pattern is not evenly repeated:** choose a pendulum count divisible by the repeated-section count, and use enough pendulums per section to represent the desired length steps.

## Project structure

```text
index.html  Simulator, styles, controls, and Three.js integration
README.md   Setup, usage, and model notes
```

## Reference and dependencies

- Inspiration: [GALILEO'S RING II — Patterns with 120 degrees symmetry](https://www.youtube.com/shorts/l1rYPY-dCAk).
- Rendering: [Three.js](https://threejs.org/), loaded from jsDelivr.

