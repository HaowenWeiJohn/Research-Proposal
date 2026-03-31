# Ultrasound as the Missing Modality for Understanding Human Physical Intelligence

## A 3-Year Research Proposal

**Researcher:** Haowen Wei
**Lab:** Device Realization Lab & Immersion Lab, MIT
**Date:** March 2026

---

## 1. Abstract

Humans perceive the physical world through the seamless integration of multiple sensory channels, yet current AI systems for understanding human movement rely almost exclusively on external observation through cameras and motion capture systems that can only see the body's surface geometry, not what happens beneath the skin. While surface electromyography (sEMG) attempts to peer deeper by measuring muscle electrical activity, it suffers from poor spatial resolution, cross-talk between adjacent muscles, and sensitivity to noise and electrode placement — making it unreliable for fine-grained analysis of complex multi-muscle coordination. Neither modality reveals the *internal mechanical reality* of human movement: how muscles deform, tendons slide, and tissues coordinate to produce dexterous manipulation. This proposal argues that **ultrasound is the missing modality** for understanding human physical intelligence. Ultrasound uniquely images sub-surface muscle dynamics in real time, distinguishing movement strategies that are invisible to external sensors — two people performing the same plank exercise can look identical from the outside while using completely different muscle groups internally. We propose a 3-year research program to: (1) build **UltraPose**, a multimodal sensor correlation study pairing wearable ultrasound with EMG, motion tracking, cameras, and force sensors on controlled hand poses, rigorously quantifying ultrasound's unique contribution through comprehensive cross-modal ablation; (2) construct a **multimodal reasoning benchmark** that adds ultrasound as the internal modality alongside vision, tactile, and EMG during free-form object manipulation, training and evaluating multimodal models on their ability to reason about human manipulation; and (3) build an **agentic AI system for physical training and rehabilitation** that uses ultrasound+EMG+vision to evaluate movement correctness at the internal muscle level, providing personalized real-time feedback that goes beyond external observation to guide optimal muscle recruitment. By opening the window to the internal physics of human movement, this research bridges the gap between surface-level observation and deep biomechanical understanding.

---

## 2. Motivation and Problem Statement

### 2.1 The "Invisible" Problem

Two people performing a plank exercise can look visually identical — same body alignment, same hold duration — while engaging completely different muscle groups to support their body. One may rely primarily on the rectus abdominis, while the other engages the transverse abdominis and obliques. A coach watching from the outside cannot distinguish these strategies, yet this difference has profound implications for injury risk, training effectiveness, and rehabilitation progress.

This "invisible" problem extends far beyond exercise. During hand manipulation, multiple forearm muscles coordinate to produce finger movements and grip forces. The forearm contains over 20 muscles packed tightly together, many controlling individual fingers through long tendons. Two people grasping a cup may achieve identical hand poses while using entirely different muscle recruitment strategies, with significant implications for fatigue patterns, injury risk, and motor learning efficiency.

### 2.2 Limitations of Current Sensing Modalities

**Vision (cameras, motion capture)** captures the external geometry of movement but cannot see beneath the skin. Advanced pose estimation systems like OpenCap [1] can estimate joint angles and even infer muscle activations through physics-based simulation, but cannot directly observe internal muscle dynamics — they infer them from external kinematics, with accuracy dependent on model assumptions.

**Surface Electromyography (sEMG)** detects electrical activation of muscles but suffers from fundamental limitations: (a) **cross-talk** between adjacent muscles makes it difficult to isolate individual muscle contributions [2]; (b) **spatial resolution** is poor — sEMG cannot distinguish between superficial and deep muscles; (c) signals are sensitive to electrode placement, skin impedance, and sweat [2]. The comprehensive emg2pose benchmark (370 hours, 193 users) [3] demonstrates the scale achievable with EMG but also highlights these inherent limitations.

**Tactile sensors** (e.g., pressure-sensitive gloves, force plates) measure the *effect* of muscle action at the contact surface — where force is applied and how much — but not the *cause*: which muscles generated that force, whether the person was near maximum effort, or whether they were about to adjust their grip. The recent MMTouch benchmark [4] demonstrates the power of multi-tactile supervision (+18.9% gain), but requires instrumenting the hand with gloves, which alters natural behavior.

### 2.3 Ultrasound: The Unique Internal Modality

Ultrasound imaging provides what no other sensing modality can: **real-time visualization of sub-surface tissue dynamics**. A wearable ultrasound transducer on the forearm can image:

- **Muscle deformation** — individual muscles shortening, lengthening, and changing shape during contraction
- **Tendon sliding** — tendons gliding through sheaths as fingers move
- **Fascicle architecture** — the geometric arrangement of muscle fibers (pennation angle, fascicle length) that determines force-generating capacity
- **Deep muscle activation** — muscles buried beneath superficial layers that sEMG cannot reliably detect

This information is **causally upstream** of both the external movement (captured by vision) and the contact forces (captured by tactile sensors). Ultrasound sees the engine, not just the car's trajectory or tire tracks.

Recent advances in wearable ultrasound hardware make this vision feasible. The ETH Zurich WULPUS platform [5] achieves <30 mW power consumption with open-source hardware. UC San Diego's flexible wearable ultrasound [6] recognizes 13 degrees of freedom during free movement. The Nature Communications 2025 work [7] demonstrated user-generic VR control from a portable ultrasound armband — no per-user calibration needed.

### 2.4 Three Critical Gaps

Despite ultrasound's unique capabilities, three critical gaps prevent it from fulfilling its potential:

1. **No systematic sensor correlation study exists for ultrasound.** While individual studies have demonstrated ultrasound-based gesture classification or joint angle estimation with 6-12 subjects [8, 9, 10], no work has rigorously quantified how ultrasound correlates with and complements other sensing modalities (EMG, vision, force, motion capture) across all meaningful combinations. The field lacks comprehensive cross-modal ablation studies that reveal exactly when and why ultrasound provides unique information.

2. **No multimodal reasoning benchmark includes ultrasound.** MMTouch [4] demonstrated the power of multi-view multi-tactile benchmarks for reasoning about physical interactions, achieving +18.9% gains from multi-tactile supervision. However, ultrasound — the only modality that reveals internal muscle dynamics — is entirely absent from all such benchmarks. No dataset pairs ultrasound with vision, tactile, and EMG data during naturalistic object manipulation to enable multimodal reasoning about both internal causes and external effects.

3. **No AI system leverages ultrasound for real-time physical training guidance.** Current rehabilitation and sports training AI relies exclusively on external observation — cameras that assess posture and joint angles. These systems cannot detect the internal muscle recruitment errors that determine movement quality: two athletes performing the same exercise with identical external form may be using completely different muscle strategies, with vastly different implications for injury risk and training effectiveness. No system uses ultrasound's internal muscle visibility to provide real-time, personalized training feedback.

This proposal addresses all three gaps.

---

## 3. Research Questions

**RQ1: How accurately can each sensor modality and their combinations infer hand pose and force, and what is ultrasound's unique contribution?**
Using controlled, standardized hand poses, we will systematically evaluate every meaningful sensor combination — US-only, EMG-only, Vision-only, US+EMG, US+Vision, EMG+Vision, US+EMG+Vision, and others — for continuous hand pose (23+ DoF) and per-finger force estimation. We will identify for which specific poses and tasks ultrasound provides the greatest advantage, and where it offers little beyond existing modalities.

**RQ2: Can a multimodal reasoning benchmark incorporating ultrasound enable AI models to better reason about human manipulation?**
We will construct a multimodal reasoning benchmark that pairs ultrasound with vision, tactile, and EMG during free-form object manipulation. We will evaluate whether ultrasound improves model performance on reasoning tasks — such as predicting manipulation outcomes, identifying grip strategies, and inferring applied forces — beyond what vision+tactile+EMG achieve alone.

**RQ3: Can a multimodal AI system using ultrasound evaluate movement correctness and provide personalized real-time feedback for physical training?**
We will build an agentic system that uses ultrasound+EMG+vision to assess whether a person is performing an exercise correctly at the internal muscle level — detecting recruitment errors invisible to cameras — and provides real-time, personalized guidance to improve movement quality during training and rehabilitation.

---

## 4. Proposed Approach and 3-Year Timeline

### Year 1: Sensor Correlation Study — The "UltraPose" Dataset

**Objective:** Build the first multimodal dataset for hand biomechanics that pairs wearable ultrasound with EMG, vision, force, and motion tracking, and conduct comprehensive ablation studies to quantify ultrasound's unique contribution across all sensor combinations.

#### 4.1.1 Data Collection Protocol

**Sensor Suite (captured simultaneously):**
| Sensor | Purpose | Specification |
|--------|---------|---------------|
| Wearable forearm ultrasound | Internal muscle dynamics | B-mode imaging, ≥15 fps |
| 8-16 channel sEMG | Muscle electrical activation | 2 kHz sampling, forearm band |
| Motion tracking (optical) | Hand pose ground truth | Marker-based or markerless, sub-mm accuracy |
| Vision cameras (multi-view) | Visual reference | 4-8 cameras, 30+ fps |
| Force sensors (tactile hand glove) | Force ground truth | Per-finger force measurement |

**Task Taxonomy (controlled, standardized poses):**
- **Individual finger movements** — flexion/extension of each finger at graded speeds
- **Standard grasps** — power, precision, lateral, tripod (following Feix taxonomy), performed in air or against a fixed standardized apparatus
- **Force-graded tasks** — light touch through maximum voluntary contraction against standardized apparatus
- **Static holds** — sustained poses at various configurations

Tasks are deliberately controlled and standardized — no free-form object manipulation, no daily objects — to eliminate variance from object differences and manipulation style, isolating clean sensor correlation signals. Free-form manipulation is reserved for the Year 2 benchmark.

**Subjects:** 15-25 participants with diverse hand sizes, ages, and skill levels.

**Scale:** ~20-40 hours of synchronized multimodal data.

**Synchronization:** All sensors software-synchronized to <5 ms, following best practices from multi-sensor capture systems.

#### 4.1.2 Ablation Studies and Correlation Analysis

This is the centerpiece contribution of Year 1 — not merely releasing a dataset, but providing rigorous findings about ultrasound's value.

- **Exhaustive sensor combination ablation:** Test all meaningful subsets for both hand pose and per-finger force estimation:
  - Single modality: US-only, EMG-only, Vision-only
  - Pairs: US+EMG, US+Vision, EMG+Vision
  - Triples: US+EMG+Vision
  - With force/MoCap as supervision signal vs. additional input
- **Per-pose performance breakdown:** Which specific poses and tasks does ultrasound help most? Where does it provide minimal advantage over EMG or vision alone? Identify the "sweet spots" for ultrasound (e.g., deep muscle discrimination, individual finger force, pre-movement intent).
- **Cross-participant generalization:** Leave-one-subject-out evaluation AND few-shot adaptation. How well does each modality and combination transfer across users?
- **Correlation analysis:** Statistical analysis of information redundancy and complementarity between modalities (mutual information, canonical correlation analysis). Quantify what unique information ultrasound captures that other modalities cannot.
- **Model architectures:** CNN and transformer baselines mapping sensor inputs to continuous 23-DoF hand pose and per-finger force.

#### 4.1.3 Deliverables

- Public dataset release (open-access, following emg2pose's CC-BY-NC-SA model)
- Comprehensive sensor correlation paper: the contribution is the *findings* — what ultrasound adds, where, and why — not just the dataset
- **Publication targets:** NeurIPS Datasets and Benchmarks Track, Nature Scientific Data

#### 4.1.4 Risk Mitigation

- **Probe placement variability:** Include multiple sessions per subject with re-mounting; develop probe-shift augmentation strategies
- **Subject recruitment:** 15-25 subjects is manageable with MIT's subject pool; 1-hour sessions per participant
- **Hardware:** Use commercial B-mode probes initially (no custom hardware risk); consider WULPUS for A-mode comparison

---

### Year 2: Multimodal Reasoning Benchmark

**Objective:** Build a multimodal reasoning benchmark that adds ultrasound as the internal modality alongside vision, tactile, and EMG during free-form object manipulation. Train multimodal models and evaluate how much ultrasound improves reasoning about human manipulation.

#### 4.2.1 New Dataset: Free-Form Manipulation

This is a **separate dataset from Year 1's UltraPose.** Where UltraPose captured controlled, standardized poses to isolate sensor correlations, this dataset captures naturalistic, free-form manipulation of daily objects — introducing the real-world variance that a reasoning benchmark must handle.

**Sensor Suite (captured simultaneously):**
| Sensor | Purpose | Specification |
|--------|---------|---------------|
| Wearable forearm ultrasound | Internal muscle dynamics | B-mode imaging, ≥15 fps |
| 8-16 channel sEMG | Muscle electrical activation | 2 kHz sampling, forearm band |
| Vision cameras (multi-view) | Visual context | Multi-view, 30+ fps |
| Force sensors (tactile hand glove) | Contact force ground truth | Per-finger force measurement |

**Task Taxonomy:**
- **Grasping** — cups, bottles, tools, small objects with varying shapes and weights
- **Tool use** — scissors, screwdrivers, pens, kitchen utensils
- **Daily actions** — opening containers, pouring, typing, buttoning, turning knobs
- **Force-sensitive tasks** — handling fragile objects, squeezing, pressing buttons with graded force
- **Bimanual tasks** — coordinated two-hand manipulation

Participants manipulate real daily objects freely, naturally varying their grip strategies, force application, and manipulation style.

**Annotation Schema:**
- Task labels and manipulation type categories
- QA pairs for multimodal reasoning (e.g., "What muscle group is primarily engaged?", "Is the grip force appropriate for this object?", "What manipulation strategy is being used?")
- Force annotations, grasp type labels, object properties
- Targeting scale of ~30,000+ annotated interactions

#### 4.2.2 Multimodal Model Training

- Train VLM-based or multimodal models on the benchmark
- **Fusion strategies:** Early fusion, late fusion, and cross-attention mechanisms
- **Cross-modal prediction:** Evaluate the practical question — can models trained with ultrasound supervision deploy without it? (Train with US, infer from vision+EMG alone)
- Self-supervised pretraining on ultrasound sequences (adapting approaches from clinical ultrasound [11] and temporal reconstruction [12]) to reduce labeled data requirements

#### 4.2.3 Evaluation and Analysis

- **Modality ablation:** Evaluate with/without ultrasound across all task types. Quantify the per-task and per-modality contribution — directly answering: how much does adding the internal modality improve reasoning about manipulation?
- **Cross-participant generalization:** How well do models transfer across users for each modality combination?
- **Comparison with external-only baselines:** Vision+Tactile only vs. Vision+Tactile+US vs. all modalities
- **Per-task breakdown:** Identify which manipulation tasks benefit most from ultrasound (e.g., force-sensitive tasks, tasks requiring deep muscle engagement)

#### 4.2.4 Deliverables

- Open benchmark release (dataset + annotations + evaluation protocol + trained models)
- Comprehensive benchmark paper with modality ablation findings
- **Publication targets:** CVPR, NeurIPS, or ECCV (1-2 papers)

---

### Year 3: Agentic AI for Physical Training and Rehabilitation

**Objective:** Build an agentic AI system that uses ultrasound+EMG+vision to understand muscle activation during exercise, evaluate movement correctness at the internal muscle level, and provide personalized real-time feedback for physical training and rehabilitation.

#### 4.3.1 Multimodal Exercise Understanding

Building on the models and data infrastructure from Years 1-2, develop a system that understands muscle activation and movement during physical exercises:
- **Exercise recognition:** Identify which exercise is being performed from multimodal input (US+EMG+vision)
- **Muscle recruitment analysis:** Map which muscles are activating, how much, and in what sequence during each exercise
- **Movement quality assessment:** Distinguish correct vs. incorrect form, not just from external appearance (which cameras can do) but from internal muscle recruitment patterns (which only ultrasound reveals)
- **Compensatory pattern detection:** Identify when a person is compensating with the wrong muscle groups — the plank principle applied across exercises (squats, planks, physical therapy movements, etc.)

#### 4.3.2 Motion Correctness Evaluation

Build a system that evaluates specific movements against reference patterns:
- **Expert reference modeling:** Capture exercise data from trained professionals (physical therapists, athletic trainers) to establish "correct" internal muscle recruitment patterns
- **Internal error detection:** Detect recruitment errors invisible to cameras — e.g., relying on rectus abdominis instead of transverse abdominis during a plank, or compensating with wrist extensors during a bicep curl
- **Graded assessment:** Not just "correct/incorrect" but a continuous assessment of movement quality with specific identification of what is suboptimal
- **Comparison across skill levels:** Quantify how muscle recruitment patterns differ between novice and expert performers for the same exercise

#### 4.3.3 Personalized Feedback Generation

Generate actionable, specific guidance that goes beyond external observation:
- **Specific muscle feedback:** "Your deep flexor is underactivating — focus on engaging it" rather than generic "keep your back straight"
- **Adaptive baselines:** Track individual progress over sessions, adjusting expectations to the person's current ability and goals
- **Rehabilitation-specific guidance:** For post-surgery or injury recovery, guide patients to activate target muscles correctly, avoiding compensatory patterns that could delay recovery
- **Training optimization:** For athletes, identify inefficient recruitment strategies and suggest corrections to improve performance and reduce injury risk

#### 4.3.4 Agentic Real-Time System

The system should ultimately operate as an interactive agent during training sessions:
- **Real-time inference pipeline:** US+EMG+Vision input → movement assessment → feedback generation, running at interactive rates
- **Proactive interaction:** The system initiates feedback when it detects issues, rather than waiting to be asked — like a coach watching and intervening
- **Adaptive guidance:** Responds to the user's corrections in real time, confirming improvements or suggesting further adjustments
- **Session management:** Guides users through exercise sequences, adjusting difficulty and focus based on observed performance
- **Natural interaction modality:** Voice feedback and/or visual overlay showing muscle activation states
- **Pilot deployment:** Validate with clinicians and sports trainers in physical therapy and athletic training settings

#### 4.3.5 Deliverables

- Deployed multimodal physical training AI system with real-time feedback capabilities
- Clinical/sports validation study demonstrating improved training outcomes vs. external-observation-only baselines
- **Publication targets:** Nature-family journal (capstone paper), CHI or UIST (interaction design), clinical rehabilitation venue

---

## 5. Lab Capabilities and Positioning

### 5.1 MIT Immersion Lab

The MIT.nano Immersion Lab provides the infrastructure essential for this research:
- **Motion capture system** — high-precision optical tracking for hand pose ground truth
- **Multi-camera rigs** — configurable camera arrays for multi-view capture
- **Ultrasound equipment** — B-mode imaging capability
- **EMG systems** — multi-channel surface EMG acquisition
- **Computing infrastructure** — GPU clusters for model training
### 5.2 Unique Positioning

The MIT Immersion Lab is uniquely positioned to pursue this research:
1. Access to ultrasound, motion capture, EMG, and camera infrastructure in a single facility
2. PI expertise in ultrasound imaging, sensing, metrology, and human-machine interfaces 
3. Institutional focus on sensing and human-machine interaction (Immersion Laboratory, Device Realization Laboratory)
4. Interdisciplinary environment enabling collaboration with clinicians, sports scientists, and rehabilitation specialists at MIT

---

## 6. Expected Contributions

1. **UltraPose Sensor Correlation Study** — The first systematic cross-modal ablation study quantifying how ultrasound correlates with and complements EMG, vision, force, and motion tracking for hand pose and force estimation. Open dataset released for the research community.

2. **Quantified Ultrasound Advantage** — Per-pose, per-task evidence of exactly when and why ultrasound provides unique information beyond other modalities, and where it offers minimal advantage — providing the field with a rigorous empirical foundation for ultrasound-based sensing.

3. **Multimodal Reasoning Benchmark** — A benchmark that adds ultrasound as the internal modality alongside vision, tactile, and EMG during free-form object manipulation, with trained multimodal models and comprehensive evaluation of ultrasound's contribution to manipulation reasoning.

4. **Agentic Physical Training System** — A validated AI system that uses ultrasound+EMG+vision to evaluate movement correctness at the internal muscle level and provides personalized real-time feedback for physical training and rehabilitation — demonstrating that ultrasound enables coaching guidance impossible with external observation alone.

5. **Open-Source Tools** — All datasets, model weights, training code, and evaluation protocols released publicly to enable broader research.

---

## 7. Related Work

---

## 8. Broader Impact

### Rehabilitation
By making internal muscle dynamics visible and interpretable in real time, this research could transform rehabilitation. The Year 3 agentic system would enable therapists and patients to receive feedback like "your deep flexor is only at 30% activation — focus on engaging it more" — specific, actionable guidance based on what is happening inside the body, not just external posture. This is especially valuable for stroke recovery, post-surgical hand rehabilitation, and neuromuscular disorders where muscle recruitment patterns are disrupted and external observation alone cannot distinguish productive from counterproductive movement strategies.

### Sports and Physical Training
Athletes and coaches currently rely on external observation. The agentic training system developed in Year 3 would enable real-time monitoring of muscle recruitment strategies during exercises, providing personalized guidance that identifies compensatory movement patterns at the internal level. This moves sports training from reactive (treat the injury) to proactive (detect the recruitment error that will cause the injury before it occurs). The system's ability to distinguish between externally identical movements with different internal strategies — the plank principle — opens an entirely new dimension of training optimization.

### Research Community
By releasing the UltraPose dataset (Year 1) and the multimodal reasoning benchmark (Year 2) as open resources, this work enables research at labs that have ultrasound hardware but lack the resources for data collection and annotation. The comprehensive ablation findings from Year 1 provide the field with empirical guidance on when and why to use ultrasound. Just as emg2pose unlocked EMG-based research at scale and MMTouch [4] catalyzed visual-tactile reasoning research, our benchmarks could catalyze a new generation of ultrasound-inclusive multimodal research.

---

## 9. References

[1] S. Uhlrich et al., "OpenCap: Human Movement Dynamics from Smartphone Videos," *PLOS Computational Biology*, 2023. https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1011462

[2] "A Comprehensive Review of sEMG-IMU Sensor Fusion for Upper Limb Movements," *Information Fusion*, 2025. https://www.sciencedirect.com/science/article/pii/S1566253525004956

[3] S. Salter et al., "emg2pose: A Large and Diverse Benchmark for Surface Electromyographic Hand Pose Estimation," *NeurIPS Datasets and Benchmarks*, 2024. https://arxiv.org/abs/2412.02725

[4] "MMTouch: A Multi-view Multi-tactile Benchmark for Human Dexterous Manipulation," *ECCV*, 2026 (under review).

[5] "Tracking of Wrist and Hand Kinematics With Ultra Low Power Wearable A-Mode Ultrasound" (WULPUS), *IEEE T-BioCAS*, 2024. https://ieeexplore.ieee.org/document/10685090/ | Open-source: https://github.com/pulp-bio/wulpus

[6] X. Gao et al., "A Wearable Echomyography System Based on a Single Transducer," *Nature Electronics*, 2024. https://www.nature.com/articles/s41928-024-01271-4

[7] B. Grandi Sgambato et al., "Virtual Reality Interactions via a User-Generic Ultrasound Human-Machine Interface for Wrist and Hand Tracking," *Nature Communications*, 2025. https://www.nature.com/articles/s41467-025-66001-6

[8] K. Bimbraw et al., "Simultaneous Estimation of Hand Configurations and Finger Joint Angles Using Forearm Ultrasound," *IEEE T-MRB*, 2023. https://ieeexplore.ieee.org/document/10020174

[9] "A deep learning framework for finger motion recognition using forearm ultrasound imaging," *Scientific Reports*, 2025. https://www.nature.com/articles/s41598-025-23348-6

[10] "Estimating continuous data of wrist joint angles using ultrasound images," *arXiv*, 2024. https://arxiv.org/html/2401.02152v1

[11] "From pretraining to privacy: federated ultrasound foundation model with self-supervised learning" (UltraFedFM), *npj Digital Medicine*, 2025. https://www.nature.com/articles/s41746-025-02085-0

[12] "Self-Supervised Temporal Ultrasound Reconstruction for Muscle Atrophy Evaluation," *Springer*, 2023. https://link.springer.com/chapter/10.1007/978-981-99-8546-3_22

---
