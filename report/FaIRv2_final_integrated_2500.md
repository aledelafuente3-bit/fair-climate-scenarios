# FaIRv2 Summative Report
### Modelling Environmental Change

---

## 1. Introduction

CO₂ concentrations in the atmosphere have grown from approximately 278 ppm in the pre-industrial era to over 420 ppm as of 2023, primarily due to anthropogenic fossil fuel combustion and land use change (Friedlingstein et al., 2023). Radiative forcing associated with increasing greenhouse gas concentrations drives an increase in Global Mean Surface Temperature (GMST), a key metric for assessing compliance with international climate targets established in the Paris Agreement, under which nations committed to limiting warming to well below 2.0°C above pre-industrial levels, with efforts toward 1.5°C (UNFCCC, 2015; IPCC AR6, 2021). Projecting future GMST carries considerable uncertainty related to both the selected emission scenario and structural or parametric uncertainties embedded within climate models (Knutti et al., 2017).

Reduced-Complexity Climate Models (RCMs) represent computationally efficient alternatives to Full Earth System Models (ESMs) that enable large simulation ensembles for uncertainty quantification (Nicholls et al., 2020). FaIRv2 (Leach et al., 2021) has been employed for IPCC AR6-class assessments and replicates CMIP6 ESM behaviour at a fraction of the computational cost through its three-layer thermal structure and dynamic carbon cycle representation.

This study uses FaIRv2 to project GMST under SSP2-4.5 — a moderate mitigation pathway (Hausfather & Peters, 2020) — and investigates how uncertainty in thermal response parameters (q₁, q₂, q₃) and carbon cycle feedback parameters (rc, rt) propagates into end-of-century temperature and atmospheric CO₂ projections through a nine-member structured factorial ensemble, calibrated against the HadCRUT5 observational record (Morice et al., 2021) and Mauna Loa atmospheric CO₂ measurements (Friedlingstein et al., 2023).

---

## 2. Scientific Question

How does GMST evolve under SSP2-4.5 radiative forcing from 2024 through 2100, and how does uncertainty in FaIRv2's thermal response parameters (q₁, q₂, q₃) and carbon cycle feedback parameters (rc, rt) propagate into ensemble projections of surface temperature and atmospheric CO₂ concentration?

---

## 3. Critical Background

Full ESMs resolve atmospheric dynamics, oceanic circulation, and biogeochemical cycles at high spatial resolution, but their computational cost makes large-ensemble uncertainty quantification impractical (Eyring et al., 2016). RCMIP (Nicholls et al., 2020) demonstrated that RCMs can reproduce CMIP6 GMST trajectories with high fidelity when appropriately calibrated, validating their use for structured uncertainty analysis. A comparison of modelling frameworks is provided in Appendix A, Table 1.

The response of the carbon cycle to warming is a major source of projection uncertainty. Rising temperatures weaken terrestrial and marine carbon sinks, creating a positive feedback that accelerates atmospheric CO₂ accumulation (Friedlingstein et al., 2006). Arora et al. (2020) documented significant variability in carbon–climate feedbacks among CMIP6 models. Two feedbacks remain poorly constrained: the β feedback, describing how sink effectiveness declines with cumulative carbon uptake (represented by rc in FaIRv2), and the γ feedback, describing how sink effectiveness declines with warming (represented by rt). Jones et al. (2016) estimated that warming-induced sink weakening could contribute an additional 0.1–0.4°C by 2100 under moderate emissions pathways.

Equilibrium Climate Sensitivity (ECS) — the long-term GMST response to a sustained doubling of CO₂ — is another major uncertainty source (Gregory et al., 2004). Sherwood et al. (2020) constrained the likely ECS range to 2.5–4.0°C, while Zelinka et al. (2020) found that higher ECS values in some CMIP6 models arise from stronger shortwave cloud feedbacks. Unlike MAGICC7, where ECS is a direct input parameter (Meinshausen et al., 2011), ECS in FaIRv2 emerges diagnostically from the thermal response parameters q and d (Leach et al., 2021), providing a more physically grounded approach to sensitivity sampling. FaIRv2 was selected for its CMIP6 calibration, public availability, and established use in IPCC AR6 assessments.

---

## 4. Model Description and Experimental Design

### 4.1 Model Description

FaIRv2 (Leach et al., 2021) represents the global climate system through three sequentially coupled modules, implemented here in its Excel configuration.

**Carbon Cycle.** Anthropogenic CO₂ emissions are partitioned between the atmosphere, terrestrial biosphere, and oceans through a multi-box impulse response framework. The airborne fraction is governed by the integrated impulse response function over 100 years (iIRF100), which evolves dynamically with two feedback parameters. The parameter rc represents how much iIRF100 changes with cumulative carbon uptake — larger rc values result in greater atmospheric CO₂ retention. The parameter rt represents how much iIRF100 changes with temperature — larger rt values cause greater sink weakening through increased soil respiration and decreased ocean solubility (Jones et al., 2016).

**Radiative Forcing.** CO₂ concentrations are converted to radiative forcing (RF, W m⁻²) using the logarithmic relationship of Myhre et al. (1998): RF = α · ln(C/C₀), where C₀ ≈ 278 ppm and α ≈ 5.35 W m⁻². Radiative forcing from other greenhouse gases, aerosols, and natural processes under SSP2-4.5 are included in the total forcing calculation.

**Thermal Response.** GMST anomaly is calculated as a convolution of radiative forcing with three exponentially decaying functions governed by thermal response coefficients q₁, q₂, q₃ (°C per W m⁻²) and timescales d₁, d₂, d₃ (years). The q parameters scale the warming magnitude in each ocean layer; the d parameters govern equilibration timescales. ECS is not specified directly but emerges from q and d parameters (Leach et al., 2021).

### 4.2 Emissions Scenario and State Variables

All simulations use SSP2-4.5, with radiative forcing stabilising at approximately 4.5 W m⁻² by 2100 (Riahi et al., 2017). Emissions are fixed across all ensemble members, so parametric uncertainty is the sole source of projection spread. The primary state variable is GMST anomaly relative to the 1850–1900 pre-industrial baseline; atmospheric CO₂ concentration (ppm) is the secondary state variable (IPCC AR6, 2021).

### 4.3 Experimental Design

Two parameter groups are varied: (1) thermal response parameters (q₁, q₂, q₃) and (2) carbon cycle feedback parameters (rc, rt). Thermal timescales (d₁, d₂, d₃) and baseline carbon uptake (r₀) are fixed at calibrated defaults. All parameter ranges are drawn from Leach et al.'s (2021) CMIP6-calibrated FaIRv2 distributions, spanning physically plausible values consistent with the CMIP6 ESM range (Table 2).

A nine-member 3×3 factorial ensemble combines low, central, and high values for each parameter group (Table 3). This design enables independent examination of each group's contribution by analysing subsets where only one group varies. Member 5 is the calibrated baseline. Each member simulates 2024–2100 under SSP2-4.5 forcing following a 1750–2024 historical spin-up using Member 5 parameters. ECS is diagnosed for each member via a supplementary CO₂-doubling simulation run to equilibrium; results are reported in Appendix A, Table A1.

---

## 5. Calibration

### 5.1 Observational Datasets

HadCRUT5 (Morice et al., 2021) provides global mean surface temperature anomalies since 1850, constructed from land surface air temperature (CRUTEM5) and sea surface temperature (HadSST4) datasets, re-baselined to 1850–1900 consistent with IPCC AR6 convention. It is chosen for its long record and frequent use in evaluating reduced-complexity models (Nicholls et al., 2020). Mauna Loa atmospheric CO₂ measurements (Keeling et al., 1958 onwards), extended to pre-industrial periods via the Law Dome ice core composite (Etheridge et al., 1996), provide the second observational constraint.

### 5.2 Calibration Procedure

Member 5 calibration is assessed against two quantitative metrics: (1) modelled warming between 1850–1900 and 2011–2020 must reproduce the observed ~1.1°C to within ±0.1°C; and (2) modelled atmospheric CO₂ in 2020 must approximate the observed Mauna Loa value of ~415 ppm (Friedlingstein et al., 2023). Decadal means are used rather than annual values to emphasise the long-term forced response and minimise the influence of interannual variability — such as ENSO and volcanic forcing anomalies — not represented in FaIRv2's standard forcing framework.

---

## 6. Results

### 6.1 Calibration Outcomes

Member 5 shows good correspondence with the HadCRUT5 historical warming record (Figure 1). The 10-year running mean GMST increased by 1.10°C between the 1850–1900 baseline and the 2011–2020 decade, satisfying calibration criterion 1. Modelled atmospheric CO₂ in 2020 was 423.96 ppm against the observed Mauna Loa value of 414.21 ppm (Figure 2), a positive bias of ~9.75 ppm (~2.4%). Given the satisfactory thermal response calibration, Member 5 is retained as the reference member, with the CO₂ bias addressed mechanistically in Section 7.

### 6.2 Ensemble GMST Projections

Under identical SSP2-4.5 forcing, the nine members exhibit substantial divergence in projected GMST trajectories (Figure 3). By 2100, warming ranges from 2.00°C (Member 1, Low–Low) to 4.02°C (Member 9, High–High), with Member 5 projecting 2.80°C — a total spread of ~2.02°C. Threshold-crossing years differ considerably: the 1.5°C threshold is crossed between 2048 (Member 1) and 2012 (Member 9), and the 2.0°C threshold between 2100 (Member 1) and 2024 (Member 9). Member 5 crosses 1.5°C in 2024 and 2.0°C in 2046.

### 6.3 Ensemble CO₂ Projections

By 2100, atmospheric CO₂ ranges from 535.12 ppm (Member 1) to 671.39 ppm (Member 9), with Member 5 projecting 574.88 ppm — a total spread of ~136.27 ppm (Figure 4). Varying rc and rt while fixing thermal-response parameters produces a CO₂ spread of ~99.30 ppm, whereas varying thermal-response parameters while fixing carbon cycle parameters produces only ~9.36 ppm. End-of-century CO₂ is therefore primarily governed by carbon cycle feedback parameters, consistent with model structure (Leach et al., 2021).

### 6.4 Ensemble Summary and Comparison with AR6

The complete ensemble summary is provided in Table 4. Most ensemble members lie within or close to the IPCC AR6 likely range for SSP2-4.5 (~2.0–3.5°C; Figure 5). Member 9, at ~4.02°C, exceeds the upper bound. The central member at ~2.80°C is close to the AR6 central estimate of ~2.7°C (IPCC AR6, 2021). Diagnosed ECS values span ~2.56°C (Members 1–3) to ~4.38°C (Members 7–9), encompassing the Sherwood et al. (2020) likely range of 2.5–4.0°C (Appendix A, Table A1).

### 6.5 Sensitivity Decomposition

Thermal-response uncertainty drives the majority of GMST projection spread throughout the full projection period (Figure 6). Varying q₁, q₂, q₃ alone while holding carbon cycle parameters at central values (Members 2, 5, 8) produces a GMST spread of ~1.37°C at 2100. Varying rc and rt alone while holding thermal-response parameters at central values (Members 4, 5, 6) produces a spread of ~0.55°C — meaning thermal-response uncertainty contributes approximately 2.5 times more to end-of-century GMST spread. This relationship holds throughout the projection period, not only at 2100. The reverse is true for atmospheric CO₂: the rc/rt-only CO₂ spread of ~99.30 ppm far exceeds the q-only spread of ~9.36 ppm.

---

## 7. Discussion

The ensemble range of 2.00–4.02°C is broadly consistent with the IPCC AR6 likely range for SSP2-4.5, and the central member at 2.80°C closely matches the AR6 central estimate of ~2.7°C (IPCC AR6, 2021). The CO₂ spread of 535–671 ppm is consistent with the substantial carbon–concentration and carbon–climate feedback uncertainty documented across CMIP6 models (Arora et al., 2020). While the dominance of thermal-response uncertainty in GMST projections is a well-established finding in the literature (Sherwood et al., 2020; Zelinka et al., 2020), the structured factorial design employed here adds interpretive value beyond reporting a composite range: by independently varying each parameter group, it cleanly quantifies the relative contribution of each uncertainty source — something not possible from a single model run or non-factorial ensemble (Leach et al., 2021).

The physical basis for thermal-response dominance is important to understand. The q parameters directly scale the magnitude of warming per unit of radiative forcing applied across the entire 76-year projection period — even small differences in q values therefore compound significantly over time. In contrast, rc and rt affect GMST only indirectly through a chain: carbon cycle parameters → airborne fraction → atmospheric CO₂ → radiative forcing via the logarithmic Myhre relationship → temperature. The logarithmic form is the critical damping step: a ~136 ppm spread in atmospheric CO₂ by 2100 translates to only ~0.7 W m⁻² of additional radiative forcing spread, which in turn produces a comparatively small GMST spread. This result independently supports the conclusion of Sherwood et al. (2020) and Zelinka et al. (2020) that constraining ECS and climate feedback strength is the primary lever for reducing long-term warming projection uncertainty, more so than improved carbon cycle constraints.

The ~9.75 ppm positive CO₂ bias in Member 5 arises from the interaction between the fixed r₀ parameter — the baseline carbon uptake rate — and the calibrated rc and rt values. Because r₀ is held constant, the iIRF100 trajectory over the historical period does not fully capture observed variability in global sink efficiency, producing slightly elevated atmospheric CO₂ retention. This is a known structural characteristic of simplified impulse response carbon cycle representations in RCMs (Leach et al., 2021; Friedlingstein et al., 2023) and does not invalidate the thermal response calibration, which remains the primary target for the GMST projection.

---

## 8. Limitations and Future Directions

Several structural limitations should be acknowledged. FaIRv2 operates as a global average model and cannot resolve regional climate variability, ocean circulation, or spatially differentiated land–atmosphere feedbacks relevant to impact assessment (Leach et al., 2021). Its three-layer thermal structure does not fully characterise deep ocean heat uptake feedbacks at multi-centennial timescales. Fixing d₁, d₂, d₃ and r₀ at default values means uncertainty in thermal timescales and baseline carbon uptake is unquantified — these represent additional projection uncertainty sources not accounted for here. Confining the analysis to SSP2-4.5 means scenario uncertainty, which can exceed parametric uncertainty at longer timescales, is entirely absent. Critically, the nine-member factorial design is not a probabilistic ensemble — it is not possible to assign likelihoods to outcomes or conclude that 2.80°C is the most likely end-of-century result, only that it represents the central parameter case. This distinction matters for policy interpretation.

Future work could address these limitations through a probabilistic ensemble drawing from full CMIP6 posterior parameter distributions (Leach et al., 2021), enabling formal confidence intervals. Multi-scenario comparison across SSP1-1.9, SSP2-4.5, and SSP5-8.5 would disentangle parametric and scenario uncertainty. Freeing the d parameters would complete the thermal-response uncertainty characterisation. Coupling FaIRv2 outputs to impact models — such as sea-level rise or agricultural yield projections — would extend the policy relevance of the sensitivity decomposition beyond global temperature.

---

## 9. Conclusion

This study applied FaIRv2 to project GMST under SSP2-4.5 between 2024 and 2100, investigating how uncertainty in thermal-response (q₁, q₂, q₃) and carbon cycle (rc, rt) parameters propagates through a nine-member factorial ensemble. The central member reproduced historical warming of 1.10°C (1850–1900 to 2011–2020), satisfying the calibration criterion, though atmospheric CO₂ in 2020 was overestimated by ~9.75 ppm due to the interaction between the fixed r₀ baseline uptake rate and the calibrated carbon cycle feedback parameters.

Projected GMST in 2100 ranged from 2.00°C to 4.02°C (central: 2.80°C), and atmospheric CO₂ from 535.12 to 671.39 ppm (central: 574.88 ppm). Most members fall within the IPCC AR6 likely range for SSP2-4.5, while the highest member exceeds the upper bound. Thermal-response uncertainty dominated GMST spread (q-only: ~1.37°C; rc/rt-only: ~0.55°C), reflecting the direct role of q parameters in scaling the warming response per unit of forcing across the full projection period. Carbon cycle uncertainty governed atmospheric CO₂ spread instead.

These results demonstrate that under a single moderate emissions pathway, parametric uncertainty alone generates a ~2°C spread in end-of-century warming — a range spanning the difference between difficult adaptation and catastrophic risk. This underscores why constraining ECS and climate feedback strength (Sherwood et al., 2020; Zelinka et al., 2020) represents a greater priority for reducing GMST projection uncertainty than improved carbon cycle constraints alone.
