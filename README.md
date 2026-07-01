# GNN-DQN Warm-Start Pathfinding Demo

Live demo for the ICDM 2026 paper **"Quantum-Inspired Warm-Start GNN-RL for Dynamic Graph Routing"**.
Two GraphSAGE-DQN agents race on the same perturbed graph: one warm-started from a multi-scenario
oracle replay buffer, one trained from scratch on that single graph (cold start). At 25×25 you can
also compare three oracle training sources: full pool, classical-only, and quantum-only.

MIT License — see [LICENSE](LICENSE).

---

## Prerequisites

- Python 3.11 (3.12+ not supported by the current PyTorch build)
- A GPU is optional; CPU inference works fine (startup takes ~60 s on CPU, ~10 s on GPU)

---

## Install

```bash
python -m venv .venv
# Linux / macOS:
source .venv/bin/activate
# Windows:
.venv\Scripts\activate

pip install -e .
```

`pip install -e .` pulls in PyTorch (CPU build), PyG, FastAPI, and Uvicorn automatically.

**GPU (optional):** If you have an NVIDIA GPU, install the CUDA build of PyTorch first, then
re-run `pip install -e .` — it will not downgrade torch:

```bash
pip install torch --index-url https://download.pytorch.org/whl/cu128
pip install -e .
```

---

## Run

```bash
python -m demo_app.server
```

Wait for `All startup tasks complete. Server ready.` in the terminal (≈10–60 s depending on hardware),
then open **http://127.0.0.1:8765** in a browser.

---

## Usage

1. **Reach tab** — pick a scenario from the dropdown (try `25x25_s2` for the clearest warm/cold gap),
   click **Load**, then **Play** to animate paths step-by-step.
   - Green = warm-start agent · Orange = cold-start agent · Blue = Dijkstra optimal
2. **Sandbox tab** — block nodes manually and race agents on your custom obstacle layout.
3. **Oracle selector (25×25 only)** — switch between *Full pool*, *Classical only*, and *Quantum only*
   training sources to see how each shapes the warm agent's learned policy.

---

## Repo contents

```
demo_app/        FastAPI server + single-page HTML UI
src/qwarm/       Minimal runtime package (GNN-DQN model, graph env, utilities)
demo_agents/     Pre-trained checkpoints (warm, cold, oracle arms) + manifest.json
```


<img width="1401" height="1029" alt="demo_screenshot" src="https://github.com/user-attachments/assets/0c452f05-5a28-4d49-889e-531d36f494dd" />
