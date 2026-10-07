# Hongrui (Jack) Zhang — Resume Source Notes

This file is an internal source-of-truth companion to the Master Resume. It is not intended for employer submission.

## Contact and header decisions

- Use LinkedIn and `hongruizhang.com` in the header.
- Omit the public GitHub link for now because it does not yet strengthen the application.
- Re-add GitHub after at least 2–3 representative repositories are cleaned, documented, and pinned.
- Expected graduation: June 2028.
- Keep work authorization information in the application tracker, not on the resume unless a specific employer requests it.

## Primary target roles

1. GPU systems / CUDA / performance engineering
2. Research internship / research engineering
3. Database systems / GPU databases
4. ML systems / AI infrastructure
5. General software engineering
6. Game systems / engine or performance roles

Named target companies: NVIDIA, Qualcomm, Riot Games.

For game-development applications, emphasize C++, GPU architecture, profiling, irregular computation, performance analysis, and systems research. Do not claim direct experience with Unreal Engine, Unity, game engines, real-time rendering, multiplayer networking, or shipped games.

## Claims approved for use

### RTSpMSpM

- Hongrui led the design and implementation.
- Yunan Zhang did not implement a major system component, but remains a coauthor and must be credited in the publication.
- Hongrui implemented the GNN integration.
- Hongrui presented the work at ISCA 2025.
- Resume-ready results: up to 1.85x over cuSPARSE and more than 3x in GNN training.

### GPU database research

- TQP-style PyTorch plans exist for all 22 TPC-H queries.
- Correctness validation exists against canonical SQL outputs.
- TCUDB Q1, Q3, and Q4 patterns were reproduced.
- TCUDB-style sparse matrix joins were substituted into TQP plans.
- Profiling covers Q1–Q20 and Q22 at SF10, and Q21 at SF2.
- RTX 5090 empirical baselines: 63.029 TFLOP/s FP32 GEMM and 1.575 TB/s device bandwidth.
- The paired sparse-join benchmark found TQP faster in 13 of 13 valid comparisons because representation construction frequently dominated.
- Current matrix-native prototype is Python/PyTorch and correctness-validated; no current runtime improvement should be claimed yet.

### RTAttention

- Analysis-only project; no prototype was implemented.
- Targeted the matrix-multiplication portion of key/value-related attention computation.
- Sparsity and inference-performance analysis did not reveal sufficient useful sparsity for an RT-core implementation.

### RTBoost

- Hongrui designed the workload mapping, experimental methodology, dataset/model generation, training, profiling, and early implementation.
- Andy Li implemented the final OptiX algorithm component.
- Same-device evaluations ultimately remained slower than XGBoost, so do not claim a robust XGBoost speedup.
- It is acceptable to describe the project as a negative-result performance study and workload-suitability investigation.
- Synthetic model sweeps reached depth 12 and approximately 400 trees.
- SSMCR contained 110,204 three-dimensional points; SUSY-3D was also evaluated.

## RTBoost timing caveat

Do not use the apparent fast points from the early tree-count graphs as speedups. Meeting notes record that some low timings resulted from failed kernel launches. One previous graph used a computed batch size of 1,342,177, which exceeded the 1,048,560 launch limit for certain configurations. Revalidate any preliminary 1.20x geometric-mean improvement over the previous RTBoost version before using it in a submitted resume.

## Technical-skills positioning

The resume may list technologies that were genuinely used in research, but should not imply expert independent implementation ability.

Internal self-assessment:

- Python: can read and explain
- C++: can read and explain
- CUDA: needs substantial review
- SQL: needs substantial review
- PyTorch: can read and explain
- OptiX: can read and explain
- Git/Linux: can modify and debug

Recommended public wording:

- “Languages used in research” rather than “Expert programming languages.”
- “Research experience with CUDA, OptiX, PyTorch, and cuSPARSE” rather than “proficient in” or “expert in.”
- Emphasize algorithm design, profiling, correctness validation, experimental design, and performance analysis.

Do not currently present these as core hands-on skills:

- CUTLASS
- WMMA
- Triton
- TensorRT
- JAX
- TensorFlow
- MPI
- Slurm
- Multi-GPU programming
- Kubernetes

Do not claim hands-on Tensor Core implementation until an implementation using a relevant API/library is completed and explainable. “Tensor algebra” is accurate; “Tensor Core experience” is currently too strong.

## Interview-readiness risk

Every submitted bullet must be defensible at the code and systems level. Before interviews, review:

- The purpose and control flow of each major CUDA/OptiX component
- Memory layout and data structures
- The exact correctness methodology
- Benchmark boundaries and timing methodology
- Why each bottleneck occurred
- What was personally implemented versus designed, directed, generated, or analyzed

General SWE and game-development applications are likely to place greater weight on independent coding screens than research-oriented roles. Tailored resumes should not overstate software-engineering fluency.

## Teaching and mentoring facts

- CS 10A: Fall 2025, Winter 2026, Spring 2026; approximately 50 students in each lab section and more than 200 students in the overall course.
- CS 203: Fall 2025; approximately 30 students.
- Smart-glasses project: mentored two undergraduates in July–August 2026; working C++ prototype used eye tracking, blink confirmation, OCR, translation, and audio output.

## Current profile wording to avoid

Remove or revise these ideas from the old one-page resume:

- “Second-year PhD student” — becomes stale quickly.
- RTSpMSpM “September 2023–Present” — use September 2023–September 2025.
- “Research experience includes Tensor Cores” — not yet supported as hands-on implementation experience.
- “Passionate” — replace with concrete specialization and evidence.

## Suggested general headline

Computer Science Ph.D. Researcher | GPU Systems, Computer Architecture, and Data-Intensive Computing

## Suggested general summary

Computer Science Ph.D. researcher specializing in GPU systems and computer architecture, with research spanning RT-core sparse matrix multiplication, tree-based inference, and matrix-native GPU query processing. First author of an ISCA 2025 paper and experienced in algorithm–hardware mapping, correctness validation, GPU profiling, and end-to-end performance analysis across CUDA, OptiX, PyTorch, and database workloads.
