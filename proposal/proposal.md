# Ultrasound as the Missing Internal Modality for Understanding Human Physical Intelligence"

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
| Wearable forearm ultrasound | Internal muscle dynamics | B-mode imaging, ≥30 fps |
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

### 7.1 Vision-Based Hand Pose Estimation

Vision-based hand pose estimation has undergone remarkable progress in the past decade. Early work on multi-person pose estimation established real-time 2D keypoint detection using part affinity fields [13], which subsequent systems extended to the hand. MediaPipe Hands [14] brought real-time hand tracking to mobile devices, demonstrating that accurate 21-keypoint estimation could run on consumer hardware without specialized sensors. On the data side, InterHand2.6M [15] provided the community with 2.6 million frames of annotated interacting hand poses from multiple subjects, enabling training at a scale previously unavailable. Most recently, transformer-based architectures such as HaMeR [16] have pushed reconstruction accuracy further, leveraging attention mechanisms to estimate full 3D hand meshes from single RGB images. Collectively, these advances have made vision-based hand tracking fast, accessible, and increasingly accurate.

Yet vision-based approaches face a fundamental ceiling rooted in what cameras can observe. The first limitation is occlusion: when fingers occlude one another, when both hands interact, or when the hand grasps an object, critical keypoints become invisible. Occlusion-aware architectures such as HandOccNet [17] partially mitigate this through learned feature propagation, but they are estimating what they cannot see, not observing it. The deeper limitation, however, is not occlusion but *opacity*: even a perfectly unoccluded view of the hand reveals only its surface geometry — joint angles, skin deformation, fingertip positions — never the internal muscle dynamics that produced that configuration. OpenCap [1] illustrates this ceiling clearly: it achieves impressive biomechanical estimates from smartphone video, but must *infer* muscle activations from external kinematics through physics-based musculoskeletal simulation, producing estimates whose accuracy depends entirely on model assumptions. Two people producing an identical hand pose may engage entirely different forearm muscles — relying on different flexor digitorum profundus vs. superficialis recruitment, or compensating with wrist extensors — and no camera system, however advanced, can distinguish these strategies. Vision observes the effect of muscle action; it cannot observe the cause.

### 7.2 Surface EMG for Hand Pose and Gesture

Surface electromyography (sEMG) offers what vision cannot: a signal originating from within the body. By measuring the electrical potentials generated during muscle contraction, sEMG provides a window into motor intent that is temporally precise and independent of line-of-sight. The Ninapro database [18] established standardized evaluation for sEMG-based hand gesture recognition, enabling systematic comparison across algorithms and sparking a generation of deep learning approaches including transfer learning methods that reduce per-user calibration requirements [19]. More recently, the emg2pose benchmark [3] demonstrated unprecedented scale — 370 hours of sEMG data from 193 users — for continuous hand pose estimation, while Meta's CTRL-Labs neural interface [20] achieved generic, non-invasive decode of motor intent from a wrist-worn sEMG band, bringing sEMG-based interaction from the laboratory to a consumer-facing demonstration published in Nature. These advances position sEMG as a serious candidate for always-on neural interfaces.

Despite this momentum, sEMG faces fundamental physical limitations that no amount of algorithmic sophistication can fully overcome. A critical appraisal by Medved et al. [21] documents the core challenges: **cross-talk** between adjacent muscles — particularly severe in the forearm, where over twenty muscles are packed into a compact volume — means that surface electrodes inevitably capture blended signals from multiple sources. **Spatial resolution** is inherently low because the electrical field diffuses through tissue; sEMG cannot distinguish contributions from deep muscles (e.g., flexor digitorum profundus) versus superficial ones (e.g., flexor digitorum superficialis), yet these muscles serve different biomechanical roles. Additionally, signals are sensitive to electrode placement, skin impedance, and perspiration, introducing session-to-session variability that complicates longitudinal use [2]. Even high-density sEMG arrays, which increase electrode count, cannot resolve the depth ambiguity: they sample more points on the same surface but do not image deeper structures.

The research community has begun to recognize these limitations. A recent review of sonomyography — the use of ultrasound imaging to decode muscle activity — explicitly frames it as an alternative that addresses sEMG's depth and spatial resolution deficits [22], noting that imaging-based approaches can visualize individual muscle deformations that electrical signals conflate. This emerging perspective suggests that the path forward for internal sensing may require moving beyond electrical measurement altogether — from detecting that muscles are active to *seeing* how they move.

### 7.3 Clinical Ultrasound and Muscle Imaging

B-mode ultrasound has served as the gold standard for non-invasive muscle architecture assessment for decades. Fukunaga et al. [23] established that ultrasound can measure pennation angle and fascicle length in contracting human muscles in vivo — the foundational demonstration that ultrasound reveals internal muscle geometry not just at rest but during active movement. Pillen et al. [24] showed that quantitative echointensity serves as a biomarker for neuromuscular disease, demonstrating that ultrasound captures clinically meaningful internal information — such as the replacement of muscle tissue by fat or fibrous tissue — that is entirely inaccessible to surface sensors. Sikdar et al. [25] articulated the broader vision of dynamic ultrasound imaging for real-time musculoskeletal function quantification, arguing that integrating continuous muscle and tendon measurements with conventional joint kinematics could yield novel insight into both normal function and pathophysiology.

Artificial intelligence is now accelerating clinical muscle ultrasound analysis. UltraFedFM [11] developed a federated foundation model for ultrasound that enables cross-institutional learning while preserving patient privacy, while self-supervised approaches [12] enable muscle atrophy evaluation from temporal ultrasound sequences without manual annotation. Yet clinical muscle imaging remains largely tethered to controlled settings with bulky equipment and expert interpretation — a gap that has motivated parallel efforts to bring ultrasound-based sensing out of the clinic and into wearable, real-time applications for gesture recognition (Section 7.4) and always-on monitoring (Section 7.5).

### 7.4 Ultrasound-Based Gesture and Movement Sensing

The use of ultrasound to decode motor intent from muscle deformation — termed "sonomyography" by Zheng et al. [26] — originated in the observation that B-mode ultrasound of the forearm can track morphological changes in muscles during wrist and hand movement, with sufficient fidelity to distinguish between different motor actions. Castellini et al. [27] subsequently demonstrated that ultrasound image features correlate linearly with finger metacarpophalangeal joint angles, establishing sonomyography as a viable human-machine interface for prosthetic control. EchoFlex [28] brought ultrasound-based gesture recognition into the HCI community, systematically comparing forearm mounting positions for a wearable ultrasonographic device and demonstrating robust classification across sessions.

Recent work has pushed sonomyography beyond discrete gesture classification toward continuous, multi-degree-of-freedom estimation and force sensing. Bimbraw et al. [8] simultaneously estimated hand configurations and individual finger joint angles from forearm ultrasound. Deep learning frameworks have achieved fine-grained finger motion recognition from ultrasound images [9], while continuous wrist joint angle estimation has been demonstrated from A-mode ultrasound signals [10]. Most notably, Jin et al. [29] extended sonomyography beyond kinematics altogether, using wearable A-mode ultrasound to estimate joint torque during dynamic activities including weightlifting and locomotion with less than 7.6% error — demonstrating that ultrasound can capture not just how the body moves but the forces it produces. This progression from discrete gesture labels to continuous kinematics to dynamics mirrors the trajectory the field needs: understanding physical intelligence requires knowing not just *what* the hand is doing but *how hard* and *with which muscles*.

### 7.5 Wearable Ultrasound Hardware

The clinical value of muscle ultrasound has driven rapid progress in miniaturizing ultrasound hardware for wearable use. Wang et al. [30] demonstrated bioadhesive ultrasound stickers — stamp-sized devices that adhere directly to skin and enable up to 48 hours of continuous organ imaging without manual operation (Science). Lin et al. [31] achieved a fully integrated wireless wearable ultrasound system capable of monitoring deep tissues in moving subjects, eliminating the tether to benchtop electronics that had confined ultrasound to clinical settings (Nature Biotechnology). On the miniaturized sensing side, Gao et al. [6] demonstrated echomyography from a single transducer element small enough for wrist-worn deployment (Nature Electronics), while WULPUS [5] achieved ultra-low-power wearable A-mode ultrasound suitable for battery-operated, always-on use.

Most recently, this hardware trajectory has converged with the gesture and movement sensing goals described above. Grandi Sgambato et al. [7] achieved user-generic wrist and hand tracking for virtual reality from wearable ultrasound — critically, without requiring per-user calibration — demonstrating that ultrasound-based interfaces can generalize across individuals (Nature Communications). Lu et al. [32] demonstrated a fully integrated, wireless ultrasound imaging wristband that continuously tracks 22 degrees of freedom across all five fingers and the palm in real time with less than 120 milliseconds of latency, enabling control of a robotic hand with sufficient dexterity for piano playing (Nature Electronics). This trajectory — from bulky clinical probes to smartwatch-sized wearable imaging systems — positions ultrasound as a practical modality for the always-on internal sensing that this proposal requires.

### 7.6 Multimodal Sensing, Benchmarks, and Reasoning for Human Movement

Multimodal datasets for hand and body understanding have grown steadily in scale and sophistication. GRAB [33] captured whole-body grasping of 51 objects with full 3D body, hand, and face pose via motion capture. ARCTIC [34] extended this to bimanual manipulation of articulated objects across 2.1 million frames. On the sensing side, sEMG-IMU fusion [2] and emg2pose [3] demonstrated that combining modalities improves pose estimation over any single sensor, while MMTouch [4] introduced multimodal visual-tactile reasoning for dexterous manipulation. Yet a consistent pattern emerges across these efforts: all combine *external* modalities — cameras, inertial sensors, surface electrodes, tactile arrays — and none includes an internal imaging modality that reveals the muscle dynamics producing the observed movement.

This gap matters for reasoning, not just sensing. PhysBench [35] benchmarked 75 vision-language models on physical world understanding and found systematic failures in reasoning about dynamics, forces, and material properties — capabilities that require information beyond what images convey. The Touch-Vision-Language dataset [36] demonstrated that adding tactile sensing to vision-language models improves physical property classification by 29% over vision alone, establishing that non-visual modalities provide critical signal for physical reasoning. If adding touch — a surface contact modality — yields such gains, adding ultrasound — which images the internal mechanics of movement — may similarly transform reasoning about human physical intelligence. No existing multimodal benchmark provides this internal view, and our proposed work (Years 1–2) is designed to fill precisely this gap.

### 7.7 AI for Physical Training and Rehabilitation

Computational approaches for exercise quality assessment have progressed from rule-based systems to deep learning. The KIMORE dataset [37] established benchmark evaluation for rehabilitation exercises, providing clinician-scored movement data from 78 subjects including patients with stroke and Parkinson's disease. Liao et al. [38] developed deep temporal architectures that automatically score rehabilitation exercises from skeleton sequences, while Parmar et al. [39] extended quality assessment to the fitness domain with Fitness-AQA, using self-supervised representations to evaluate workout form at scale (ECCV). These systems demonstrate that AI can meaningfully assess movement quality — but all operate exclusively on external kinematics derived from cameras or inertial sensors.

A scoping review of AI-driven virtual rehabilitation in npj Digital Medicine [40] surveyed the field and found that every system relies on external observation: camera-based pose estimation, wearable IMUs, or depth sensors. No system assesses internal muscle activation quality. Current AI can detect that a patient's squat deviates from a reference trajectory, but it cannot determine *why* — whether the deviation reflects weak gluteal activation, quadriceps dominance, or compensatory hip flexor engagement. This is the gap our Year 3 system addresses: by incorporating ultrasound alongside EMG and vision, we move from coaching based on what movement *looks like* to coaching based on how movement is *produced*.

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

[13] Z. Cao, G. Hidalgo, T. Simon, S.-E. Wei, and Y. Sheikh, "OpenPose: Realtime Multi-Person 2D Pose Estimation Using Part Affinity Fields," *IEEE TPAMI*, vol. 43, no. 1, pp. 172–186, 2021. https://arxiv.org/abs/1812.08008

[14] F. Zhang, V. Bazarevsky, A. Vakunov, A. Tkachenka, G. Sung, C.-L. Chang, and M. Grundmann, "MediaPipe Hands: On-device Real-time Hand Tracking," *CV4ARVR Workshop*, 2020. https://arxiv.org/abs/2006.10214

[15] G. Moon, S.-I. Yu, H. Wen, T. Shiratori, and K. M. Lee, "InterHand2.6M: A Dataset and Baseline for 3D Interacting Hand Pose Estimation from a Single RGB Image," *ECCV*, 2020. https://arxiv.org/abs/2008.09309

[16] G. Pavlakos, D. Shan, I. Radosavovic, A. Kanazawa, D. Fouhey, and J. Malik, "Reconstructing Hands in 3D with Transformers," *CVPR*, 2024. https://arxiv.org/abs/2312.05251

[17] J. Park, Y. Oh, G. Moon, H. Choi, and K. M. Lee, "HandOccNet: Occlusion-Robust 3D Hand Mesh Estimation Network," *CVPR*, 2022. https://openaccess.thecvf.com/content/CVPR2022/html/Park_HandOccNet_Occlusion-Robust_3D_Hand_Mesh_Estimation_Network_CVPR_2022_paper.html

[18] M. Atzori, A. Gijsberts, C. Castellini, et al., "Electromyography data for non-invasive naturally-controlled robotic hand prostheses," *Scientific Data*, vol. 1, 140053, 2014. https://doi.org/10.1038/sdata.2014.53

[19] U. Cote-Allard, C. L. Fall, A. Drouin, et al., "Deep Learning for Electromyographic Hand Gesture Signal Classification Using Transfer Learning," *IEEE TNSRE*, vol. 27, no. 4, pp. 760–771, 2019. https://doi.org/10.1109/TNSRE.2019.2896269

[20] P. Kaifosh, T. R. Reardon, et al. (CTRL-labs at Reality Labs), "A generic non-invasive neuromotor interface for human-computer interaction," *Nature*, vol. 645, pp. 702–711, 2025. https://www.nature.com/articles/s41586-025-09255-w

[21] V. Medved, S. Medved, and I. Kovač, "Critical Appraisal of Surface Electromyography (sEMG) as a Taught Subject and Clinical Tool in Medicine and Kinesiology," *Frontiers in Neurology*, vol. 11, 560363, 2020. https://doi.org/10.3389/fneur.2020.560363

[22] V. Nazari and Y. P. Zheng, "Controlling Upper Limb Prostheses Using Sonomyography (SMG): A Review," *Sensors*, vol. 23, no. 4, 1885, 2023. https://doi.org/10.3390/s23041885

[23] T. Fukunaga, Y. Ichinose, M. Ito, Y. Kawakami, and S. Fukashiro, "Determination of fascicle length and pennation in a contracting human muscle in vivo," *Journal of Applied Physiology*, vol. 82, no. 1, pp. 354–358, 1997. https://doi.org/10.1152/jappl.1997.82.1.354

[24] S. Pillen, I. M. P. Arts, and M. J. Zwarts, "Muscle ultrasound in neuromuscular disorders," *Muscle & Nerve*, vol. 37, no. 6, pp. 679–693, 2008. https://doi.org/10.1002/mus.21015

[25] S. Sikdar, Q. Wei, and N. Cortes, "Dynamic ultrasound imaging applications to quantify musculoskeletal function," *Exercise and Sport Sciences Reviews*, vol. 42, no. 3, pp. 126–135, 2014. https://doi.org/10.1249/JES.0000000000000015

[26] Y. P. Zheng, M. M. F. Chan, J. Shi, X. Chen, and Q. H. Huang, "Sonomyography: Monitoring morphological changes of forearm muscles in actions with the feasibility for the control of powered prosthesis," *Medical Engineering & Physics*, vol. 28, no. 5, pp. 405–415, 2006. https://doi.org/10.1016/j.medengphy.2005.07.012

[27] C. Castellini, G. Passig, and E. Zarka, "Using ultrasound images of the forearm to predict finger positions," *IEEE TNSRE*, vol. 20, no. 6, pp. 788–797, 2012. https://doi.org/10.1109/TNSRE.2012.2207916

[28] J. McIntosh, A. Marzo, M. Fraser, and C. Phillips, "EchoFlex: Hand Gesture Recognition using Ultrasound Imaging," *ACM CHI*, pp. 1923–1934, 2017. https://doi.org/10.1145/3025453.3025807

[29] Y. Jin, J. T. Alvarez, E. L. Suitor, et al., "Estimation of joint torque in dynamic activities using wearable A-mode ultrasound," *Nature Communications*, vol. 15, 5756, 2024. https://doi.org/10.1038/s41467-024-50038-0

[30] C. Wang, X. Chen, L. Wang, M. Makihata, H.-C. Liu, T. Zhou, and X. Zhao, "Bioadhesive ultrasound for long-term continuous imaging of diverse organs," *Science*, vol. 377, no. 6605, pp. 517–523, 2022. https://doi.org/10.1126/science.abo2542

[31] M. Lin, Z. Zhang, X. Gao, Y. Bian, R. S. Wu, et al., "A fully integrated wearable ultrasound system to monitor deep tissues in moving subjects," *Nature Biotechnology*, vol. 42, no. 3, pp. 448–457, 2024. https://doi.org/10.1038/s41587-023-01800-0

[32] G. Lu, S. Kim, X. Chen, Y. Zeng, D. Li, S. Wang, et al., "Hand tracking using wearable wrist imaging," *Nature Electronics*, 2026. https://doi.org/10.1038/s41928-026-01594-4

[33] O. Taheri, N. Ghorbani, M. J. Black, and D. Tzionas, "GRAB: A Dataset of Whole-Body Human Grasping of Objects," *ECCV*, 2020. https://doi.org/10.1007/978-3-030-58548-8_34

[34] Z. Fan, O. Taheri, D. Tzionas, M. Kocabas, M. Kaufmann, M. J. Black, and O. Hilliges, "ARCTIC: A Dataset for Dexterous Bimanual Hand-Object Manipulation," *CVPR*, 2023. https://doi.org/10.1109/CVPR52729.2023.01244

[35] W. Chow, J. Mao, B. Li, D. Seita, V. Guizilini, and Y. Wang, "PhysBench: Benchmarking and Enhancing Vision-Language Models for Physical World Understanding," *ICLR*, 2025. https://arxiv.org/abs/2501.16411

[36] L. Fu, G. Datta, H. Huang, W. C.-H. Panitch, J. Drake, J. Ortiz, M. Mukadam, M. Lambeta, R. Calandra, and K. Goldberg, "A Touch, Vision, and Language Dataset for Multimodal Alignment," *ICML*, PMLR 235:14080–14101, 2024. https://proceedings.mlr.press/v235/fu24b.html

[37] M. Capecci, M. G. Ceravolo, F. Ferracuti, S. Iarlori, A. Monteriu, L. Romeo, and F. Verdini, "The KIMORE Dataset: KInematic Assessment of MOvement and Clinical Scores for Remote Monitoring of Physical REhabilitation," *IEEE TNSRE*, vol. 27, no. 7, pp. 1436–1448, 2019. https://doi.org/10.1109/TNSRE.2019.2923060

[38] Y. Liao, A. Vakanski, and M. Xian, "A Deep Learning Framework for Assessing Physical Rehabilitation Exercises," *IEEE TNSRE*, vol. 28, no. 2, pp. 468–477, 2020. https://doi.org/10.1109/TNSRE.2020.2966249

[39] P. Parmar, A. Gharat, and H. Rhodin, "Domain Knowledge-Informed Self-Supervised Representations for Workout Form Assessment," *ECCV*, pp. 105–123, 2022. https://doi.org/10.1007/978-3-031-19839-7_7

[40] A. Abedi, T. J. F. Colella, M. Pakosh, and S. S. Khan, "Artificial intelligence-driven virtual rehabilitation for people living in the community: A scoping review," *npj Digital Medicine*, vol. 7, 25, 2024. https://doi.org/10.1038/s41746-024-00998-w

---
