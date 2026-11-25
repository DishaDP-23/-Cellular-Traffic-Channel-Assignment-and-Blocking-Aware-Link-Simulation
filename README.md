# Cellular Traffic, Channel Assignment and Blocking-Aware Link Simulation

**Wireless Communication and Computing – Group 13 | Question 13**

A MATLAB-based simulation study of cellular traffic management, channel assignment, wireless propagation, QPSK transmission and reception, and blocking-aware network performance.

---

## 1. Project Overview

This project investigates the performance of cellular wireless networks under different traffic loads and channel assignment strategies.

The simulation compares **Fixed Channel Assignment (FCA)** and **Dynamic Channel Assignment (DCA)** across a seven-cell cellular network. It evaluates how channel allocation, propagation losses, shadowing, co-channel interference and receiver performance affect communication reliability and overall network capacity.

The project is divided into four interconnected parts:

- **Part A – Traffic Generation and Channel Assignment:** Models call arrivals, holding times, channel allocation and QPSK frame generation.
- **Part B – Channel and Propagation Modelling:** Evaluates path loss, shadowing, interference, AWGN and received SINR.
- **Part C – Receiver Design and Link Reliability:** Implements QPSK demodulation, BER/PER evaluation and receiver-based session classification.
- **Part D – Performance Analysis and Engineering Decision:** Integrates the results and compares blocking probability, radio failures and qualified carried traffic.

The objective is to understand the trade-offs between spectrum utilization, traffic capacity and wireless link reliability.

---
## 2. Project Files and Downloads

The complete MATLAB project package and supporting documentation are available under the repository's **Releases** section.

[Download Complete MATLAB Project](../../releases/latest)

The release package includes the project source files, simulation outputs and supporting documentation.

---

## 3. Project Objectives

- Simulate cellular traffic using stochastic call arrival and holding-time models.
- Implement and compare FCA and DCA channel assignment strategies.
- Analyse cellular network geometry and channel reuse.
- Model wireless propagation using free-space path loss and log-distance path loss with log-normal shadowing.
- Evaluate co-channel interference and Additive White Gaussian Noise (AWGN).
- Implement Gray-coded QPSK transmission and reception.
- Calculate Signal-to-Interference-plus-Noise Ratio (SINR), Bit Error Rate (BER) and Packet Error Rate (PER).
- Evaluate call blocking, radio failures and carried traffic.
- Identify the trade-offs between network capacity and communication reliability.

---

## 4. Technologies and Tools

| Technology | Purpose |
|---|---|
| MATLAB | Simulation and performance analysis |
| MATLAB Base Functions | Mathematical modelling, signal processing and visualisation |
| QPSK | Digital modulation and demodulation |
| AWGN | Wireless noise modelling |
| CSV | Simulation data and performance summaries |
| MAT | MATLAB simulation data storage |

The implementation uses MATLAB Base functions and does not require Communications Toolbox functions.

---

## 5. System Configuration

The simulation uses the following configuration:

| Parameter | Value |
|---|---:|
| Number of cells | 7 |
| Total available channels | 21 |
| Cell radius | 500 m |
| Mobile transmit power | 23 dBm |
| Mean call holding time | 120 seconds |
| Simulation duration | 1800 seconds |
| Offered traffic | 2, 5 and 8 Erlangs/cell |
| QPSK payload | 256 bits |
| Preamble | 8 bits |
| Number of Part A replications | 10 |

### Channel Assignment Strategies

**Fixed Channel Assignment (FCA)**

The available channels are statically partitioned among cells according to the configured reuse groups. Each cell operates with its assigned channel subset.

**Dynamic Channel Assignment (DCA)**

Channels are allocated dynamically from a shared channel pool. The simulation applies reuse-conflict distance constraints to prevent conflicting simultaneous transmissions.

Both strategies are evaluated using the same total channel pool.

---

## 6. Project Architecture

The project follows a sequential simulation and analysis architecture.

```text
             Cellular Network Configuration
                         |
                         v
              PART A: TRAFFIC GENERATION
                         |
              Poisson Call Arrivals
              Exponential Holding Times
              FCA / DCA Channel Assignment
              QPSK Frame Generation
                         |
                         v
               PART B: CHANNEL MODEL
                         |
              Free-Space Path Loss
              Log-Distance Path Loss
              Log-Normal Shadowing
              Co-Channel Interference
              AWGN and SINR Evaluation
                         |
                         v
              PART C: RECEIVER DESIGN
                         |
              QPSK Demodulation
              BER / PER Evaluation
              Link Target Classification
              Session Failure Analysis
                         |
                         v
             PART D: SYSTEM PERFORMANCE
                         |
              Blocking Probability
              Radio Failure Rate
              Qualified Carried Traffic
              Capacity Comparison
                         |
                         v
                 FINAL RESULTS
```

---

## 7. Implementation Details

### Part A – Traffic Generation and Channel Assignment

**Main file:** `partA_transmitter.m`

This module generates cellular traffic and assigns channels to incoming sessions.

Implementation includes:

- Poisson-distributed call arrivals.
- Exponentially distributed call holding times.
- Seven-cell cellular network geometry.
- FCA and DCA channel allocation.
- Channel occupancy and active transmitter tracking.
- Reproducible payload and preamble generation.
- Gray-coded unit-energy QPSK modulation.
- Multiple independent simulation replications.

**Outputs:**
- Channel occupancy plots.
- Cellular network geometry.
- QPSK constellation.
- Session-level logs.
- Blocking and traffic summaries.
- MATLAB handoff data for subsequent modules.

### Part B – Channel and Propagation Modelling

**Main file:** `partB_channel.m`

This module evaluates the wireless propagation environment and its effect on active communication links.

Implementation includes:

- Free-Space Path Loss (FSPL).
- Log-distance path loss.
- Log-normal shadowing.
- Co-channel interference under spatial reuse.
- Thermal noise and receiver noise figure.
- AWGN-based QPSK reception.
- SINR and theoretical BER/PER evaluation.

The propagation model uses a path-loss exponent of 3.0 and shadowing standard deviation of 6 dB.

**Outputs:**
- Received power comparisons.
- Network interference visualisations.
- SINR comparisons across traffic loads.
- FCA and DCA channel snapshots.
- QPSK constellation and waveform plots.
- Channel and link performance CSV/MAT files.

### Part C – Receiver Design and Link Reliability

**Main file:** `partC_receiver.m`

This module evaluates the receiver's ability to recover transmitted QPSK frames under the simulated channel conditions.

Implementation includes:

- Loading admitted sessions and transmitted QPSK frames.
- Validating transmitter and receiver bit mapping.
- Adding equivalent complex AWGN based on session SINR.
- Hard-decision QPSK demodulation.
- Measured and theoretical BER/PER calculation.
- Receiver target evaluation.
- Classification of blocked and radio-failed sessions.
- Carried traffic and link reliability analysis.

The receiver uses the following configurable engineering targets:

| Parameter | Target |
|---|---:|
| Minimum SINR | 5 dB |
| Maximum BER | 1 × 10⁻³ |
| Maximum PER | 0.10 |

A session passes the theoretical link target only when all three conditions are satisfied.

**Outputs:**
- Receiver constellation plots.
- SINR and BER distributions.
- BER/PER target comparisons.
- Session-level receiver results.
- Controller status visualisations.
- Link performance summaries.

### Part D – Performance Analysis and Engineering Decision

**Main file:** `partD_analysis.m`

This module integrates the traffic and receiver results to evaluate overall cellular network performance.

Implementation includes:

- Blocking probability calculation.
- Radio failure rate calculation.
- Overall unsuccessful session analysis.
- Target-qualified carried traffic calculation.
- FCA and DCA capacity comparison.
- Validation of session counts across simulation modules.
- Engineering recommendations based on performance targets.

The system-level analysis uses the following assumed targets:

| Metric | Target |
|---|---:|
| Blocking probability | ≤ 5% |
| Radio failure rate | ≤ 5% of admitted sessions |

These are illustrative engineering assumptions, not prescribed assignment limits.

**Outputs:**
- Blocking probability comparison.
- Radio failure comparison.
- Qualified carried traffic comparison.
- Total unsuccessful session comparison.
- Capacity comparison.
- Final engineering recommendation.

---

## 8. Simulation Results

The simulation evaluates FCA and DCA at three offered traffic levels: 2, 5 and 8 Erlangs per cell.

### Blocking Probability

| Offered Traffic | FCA | DCA |
|---|---:|---:|
| 2 Erlangs/cell | 21.70% | 0.00% |
| 5 Erlangs/cell | 48.74% | 4.60% |
| 8 Erlangs/cell | 68.14% | 21.05% |

DCA demonstrates lower blocking probability across all three traffic levels because it dynamically allocates channels from the shared pool.

### Mean SINR

| Offered Traffic | FCA | DCA |
|---|---:|---:|
| 2 Erlangs/cell | 28.44 dB | 22.83 dB |
| 5 Erlangs/cell | 26.35 dB | 21.98 dB |
| 8 Erlangs/cell | 27.33 dB | 19.53 dB |

FCA provides higher mean SINR in these simulations, reflecting the different channel reuse and interference conditions.

### Target-Qualified Carried Traffic

| Offered Traffic | FCA | DCA |
|---|---:|---:|
| 2 Erlangs/cell | 10.798 E | 11.944 E |
| 5 Erlangs/cell | 15.975 E | 26.009 E |
| 8 Erlangs/cell | 17.796 E | 34.133 E |

DCA carries more target-qualified traffic at all three offered loads in the simulated scenarios.

### Overall Observation

The results demonstrate a trade-off between channel allocation efficiency and link reliability.

- DCA provides lower blocking and higher target-qualified carried traffic.
- FCA provides higher mean SINR and lower radio failure rates.
- Neither strategy satisfies both assumed system-level targets simultaneously at any of the tested traffic loads.

The results highlight the importance of considering both traffic capacity and physical-layer reliability when designing cellular networks.

---

## 9. Running the Project

The complete project can be executed using the master MATLAB script.

### Requirements

- MATLAB.
- The complete project directory with its original folder structure.

No additional MATLAB toolboxes are required by the implementation.

### Execution

1. Download and extract the complete project ZIP.
2. Open MATLAB.
3. Set the extracted `WCC_G13_Q13_PROJECT_codes` directory as the Current Folder.
4. Open `final.m`.
5. Run the script.

Alternatively, execute the following command in the MATLAB Command Window:

```matlab
final
```

The master script executes all four parts sequentially:

```text
Part A → Part B → Part C → Part D
```

The generated outputs are saved in their respective output directories.

**Important:** Keep the original folder structure and filenames intact because the simulation modules use relative paths to exchange data.

---

## 10. Repository Structure

```text
WCC_G13_Q13/
│
├── WCC_G13_Q13_PROJECT_codes/
│   │
│   ├── final.m
│   ├── final_summary.csv
│   ├── final_run_validation.txt
│   │
│   ├── partA_transmitter.m
│   ├── README_PartA.md
│   ├── partA_output/
│   │
│   ├── partB_channel.m
│   ├── README_PartB.md
│   ├── partB_output/
│   │
│   ├── partC_receiver.m
│   ├── README_PartC.md
│   ├── partC_output/
│   │
│   ├── partD_analysis.m
│   ├── README_PartD.md
│   └── partD_output/
│
└── WCC_G13_Q13_PROJECT_RESULT_IMAGES/
    │
    ├── NETWORK_SURVEY_APP_IMAGES/
    ├── PART_A_IMAGES/
    ├── PART_B_IMAGES/
    ├── PART_C_IMAGES/
    └── PART_D_IMAGES/
```

Each output directory contains the corresponding simulation data, CSV summaries, MATLAB data files and visualisations.

---

## 11. Validation and Limitations

The final project includes integration checks to verify consistency between the simulation modules.

The recorded validation confirms:

- All four MATLAB part scripts executed successfully in the validated run.
- Six FCA/DCA and traffic-load combinations were evaluated.
- Offered, admitted and blocked session counts were consistent across Parts A and C.
- Part B evaluated every admitted Part A QPSK frame.
- Receiver transmitter-mapping checks passed.
- Session accounting and failure-count consistency checks passed.

### Model Limitations

The following limitations should be considered when interpreting the results:

- Each admitted communication link is evaluated using a representative SINR sample at the session holding-time midpoint.
- Co-channel interference uses a cell-centre reuse-distance approximation.
- Adjacent-channel leakage is not modelled.
- Aggregate interference is approximated as Gaussian noise.
- The numerical BER/PER and blocking targets are assumed engineering thresholds.
- Target-qualified carried traffic is an estimated service metric, not a direct end-to-end throughput measurement.
- Measured AWGN frame-error results may vary when the receiver simulation is rerun.

The simulation results should therefore be interpreted within the configured network model and assumptions.

---


## 12. Conclusion

This project demonstrates an integrated approach to cellular traffic modelling, channel assignment, wireless propagation analysis and receiver performance evaluation.

By comparing FCA and DCA under different offered traffic conditions, the simulation illustrates how channel allocation strategies influence blocking probability, interference, link reliability and qualified carried traffic.

The combined analysis of traffic-level and physical-layer performance provides a basis for evaluating cellular network capacity and identifying possible improvements through interference-aware channel allocation, additional spectrum and admission or power control strategies.
