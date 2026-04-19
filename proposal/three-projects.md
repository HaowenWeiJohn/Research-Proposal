# Three Research Projects — Distilled

**Thesis:** Ultrasound is the missing *internal* sensing modality for understanding human physical intelligence. Vision sees surface geometry; sEMG suffers from cross-talk and depth ambiguity; tactile sensors capture effects, not causes. Only ultrasound images sub-surface muscle deformation in real time — the engine, not the trajectory.

---

### 1. UltraPose — Multimodal Sensor Fusion for Hand Pose & Force

**Hook:** The first systematic study quantifying what wearable ultrasound uniquely contributes beyond EMG, vision, motion capture, and force.

**Problem:** Sonomyography works, but no one has rigorously measured *when* ultrasound adds information vs. when EMG or vision already suffice.

**Approach:** Synchronized US + EMG + MoCap + multi-view cameras + per-finger force on 15-25 subjects across controlled hand poses (~20-40 hrs); exhaustive cross-modal ablation, per-pose breakdown, mutual-information analysis.

**Outcome:** Open dataset + per-pose evidence of ultrasound's "sweet spots" — the empirical foundation the field lacks. Target: NeurIPS D&B / Nature Scientific Data.

---

### 2. Ultrasound for Biomechanics Reasoning — Multimodal Benchmark

**Hook:** The first multimodal reasoning benchmark that adds ultrasound — the only internal modality — to vision, tactile, and EMG during free-form manipulation.

**Problem:** External multi-tactile already yields +18.9% on manipulation reasoning (MMTouch); no benchmark tests whether *internal* muscle dynamics improve reasoning about how movements are produced.

**Approach:** Free-form daily-object manipulation dataset (~30K annotated interactions); train multimodal/VLM models with QA annotations; ablate US contribution; test cross-modal prediction (train with US, infer without).

**Outcome:** Open benchmark + trained models + per-task evidence of where internal sensing improves reasoning. Target: CVPR / NeurIPS / ECCV.

---

### 3. Agentic AI for Physical Training & Rehabilitation

**Hook:** A real-time coach that sees inside the body — detecting recruitment errors invisible to cameras and giving muscle-specific feedback.

**Problem:** Every existing rehab/training AI relies on external observation; it can detect that a squat deviates from reference but not *why* — wrong muscle dominance, compensatory recruitment, weak deep activation.

**Approach:** US + EMG + vision pipeline benchmarked against expert reference patterns; agentic system that proactively flags compensation and gives specific corrections ("your deep flexor is underactivating").

**Outcome:** Deployed system + clinical/sports validation showing gains over external-observation baselines. Target: Nature-family capstone + CHI / UIST.
