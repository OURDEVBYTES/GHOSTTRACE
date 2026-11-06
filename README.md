# GhostTrace
**A single-pixel Hilbert anchor for deterministic generative forensics.**

## The Hypothesis
Modern AI image generators (like Stable Diffusion, Midjourney, etc.) are fundamentally deterministic. Given the same seed, prompt, and hardware, they will always produce the exact same image. 

**GhostTrace tests a radical idea:** If you map a single pixel to a 1D Hilbert spatial index, you can use it as a cryptographic anchor to trace the entire image back to its generation seed, hardware fingerprint, and original text prompt.

If this works, we can definitively prove whether an image is a real photograph or a synthetic hallucination—and trace it back to the exact GPU that birthed it.

## How It Works (The Math)
1. **The Hilbert Curve:** We use a space-filling fractal to map 2D pixel coordinates `(x, y)` into a 1D index `h`. This preserves spatial locality, meaning adjacent pixels remain mathematically adjacent in 1D space.
2. **The Deterministic Generator:** We simulate an AI generation by hashing a text prompt (SHA-256) into a seed, and using that seed to generate pixel noise.
3. **The Forensics:** We extract a single anchor pixel, map it to its Hilbert index, and reverse-engineer the seed to see if it matches the original prompt. 

## The 6-Week Micro-Sprint
*Building this 15 minutes a day, without burning out.*

- [x] **Week 0:** Setup repo, map the architecture, and define the license.
- [ ] **Week 1:** Build the Hilbert curve 2D→1D mapper (`hilbert.rs`).
- [ ] **Week 2:** Visualize the Hilbert curve as a generated PNG image.
- [ ] **Week 3:** Build the deterministic "AI" generator (`generator.rs`).
- [ ] **Week 4:** Implement the single-pixel forensic matcher (`forensics.rs`).
- [ ] **Week 5:** Output the forensic report as structured JSON.
- [ ] **Week 6:** File the Provisional Patent Application (PPA).

## Project Structure
```text
ghost_trace/
├── src/                 # Rust source code
│   ├── main.rs          # CLI entry point
│   ├── hilbert.rs       # Week 1: Spatial mapping engine
│   ├── generator.rs     # Week 3: Deterministic seed generator
│   └── forensics.rs     # Week 4: Single-pixel trace logic
├── data/                # Sample images & test prompts
├── logs/                # Forensic JSON outputs (Patent evidence)
├── docs/                # Weekly build logs & patent notes
├── Cargo.toml           # Rust dependencies
└── LICENSE              # Apache 2.0
