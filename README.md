# Awesome Compute–Power Coordination (算电协同) [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated review of **deployed projects, grid requirements, patents and open-source software** on coordinating computing workloads (data centers, AI/GPU clusters, computing-power networks) with the electric power system.

Most lists in this space collect papers. This one deliberately does not. It tracks what has been **built, required, claimed or released**: demonstration projects with measured numbers, the ramp-rate and ride-through limits grid operators are writing for large computational loads, patents, and code you can run.

> Last updated: **2026-11-16**. Contributions and corrections welcome — see [Contributing](#contributing).

**Related lists by the same maintainer** (entries there are not repeated here):
- [awesome-large-load-grid](https://github.com/Yuz2023/awesome-large-load-grid) — regulations, dockets and task forces on large-load interconnection (process, cost allocation, policy).
- [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling) — papers, datasets, simulators and patents on AI data center power modeling.
- [Awesome-MCP-for-Power-Engineering](https://github.com/Yuz2023/Awesome-MCP-for-Power-Engineering) — Model Context Protocol servers for power engineering research and applications.
- [awesome-PELS-open-source-ai-tools](https://github.com/Yuz2023/awesome-PELS-open-source-ai-tools) — open-source AI tools for power electronics.

## Contents

- [How to read the verification marks](#how-to-read-the-verification-marks)
- [What grid operators require of large computational loads](#what-grid-operators-require-of-large-computational-loads)
- [Projects, programs and products](#projects-programs-and-products)
- [Patents](#patents)
- [Open-source software and data](#open-source-software-and-data)
- [Leads not yet verified](#leads-not-yet-verified)
- [Contributing](#contributing)
- [License](#license)

---

## How to read the verification marks

Every row carries one of three marks. They describe how the entry was checked on the "last updated" date, nothing more.

| Mark | Meaning |
|---|---|
| **P** | Primary source opened; the number or claim was found in it. |
| **S** | Taken from a secondary source that quotes or summarizes the primary document. The primary document was not opened. |
| **R** | Official registry or API record checked (USPTO Patent Public Search for patents, GitHub API for repositories). |

Anything that could not be checked at all is kept out of the main tables and listed under [Leads not yet verified](#leads-not-yet-verified).

Legal status of patents was not checked beyond "granted" versus "published application". Draft and proposed grid rules change quickly; check the linked document before citing a number.

---

## What grid operators require of large computational loads

### Ramp rate and power variation limits

| Who | Document (date, status) | Limit as written | Stated rationale | Mark |
|---|---|---|---|---|
| ERCOT (Texas) | [Large Computational Load Power Variation Limit Discussion](https://www.ercot.com/files/docs/2026/06/19/ERCOT-LCL-Power-Variation-Limit-Discussion_fin.pdf) (2026-06-19, proposed wording) | Peak-to-peak active power variation, filtered to keep 0.1–55 Hz, "shall not exceed **10 MW over any rolling 5-second interval**" | "Oscillatory frequency range of concern: 0.1 Hz to 55 Hz" | P |
| ERCOT | [Interconnection and Grid Analysis Update](https://www.ercot.com/files/docs/2026/09/17/10-Interconnection-and-Grid-Analysis-Update-REVISED.pdf) (2026-09-17, board material) | Will recommend "10 MW per 5 seconds" for power variation in large loads. A draft NOGRR, "Large Load MW Variation Requirements", was planned for September or October; not yet in ERCOT's NOGRR list on 2026-11-16 | Fast fluctuation of AI training load can perturb synchronous generator shafts, with risk of fatigue or damage | P |
| ERCOT | [NPRR 1191](https://www.ercot.com/mktrules/issues/NPRR1191), ramp limits as quoted in a [2023 stakeholder comment](https://www.ercot.com/files/docs/2023/08/31/Galaxy%20comments%20on%201191NPRR.pdf) (2023 proposal; **withdrawn 2024**, never adopted) | Ramp **down**: lesser of 5% of peak demand or 20 MW/min. Ramp **up**: lesser of 2% of peak demand or 8 MW/min. Controllable load resources: 20% of registered peak per minute | Not stated in the comment | P (status), S (numbers) |
| CAISO | [Second Revised Draft Tariff Language, §25.7.1](https://stakeholdercenter.caiso.com/InitiativeDocuments/Second-Revised-Draft-Tariff-Language-Large-Loads-Order-to-Show-Cause-Oct-30-2026.docx) (2026-10-30, draft tariff, loads ≥50 MW; follows the [June straw proposal](https://stakeholdercenter.caiso.com/InitiativeDocuments/Large-Load-Technical-Requirements-Straw-Proposal-Jun-15-2026.pdf) and the [September draft final proposal](https://stakeholdercenter.caiso.com/InitiativeDocuments/Draft-Final-Proposal-Large-Load-Enhancements-Sep-24-26.pdf)) | "Average active power ramp rate, measured at the point of interconnection over a **rolling ten (10)-minute interval**, does not exceed **twenty (20) megawatts per minute**", up and down, including start-up, shutdown and post-outage restoration | Straw proposal: real-time **regulation reserve** procurement; keeping interconnection frequency within the **±0.036 Hz deadband** so primary frequency response is not triggered routinely. Tariff text responds to FERC's 2026-06-18 show-cause order (EL26-71) | P |
| IESO (Ontario) | [Technical Requirements for Large Computational Loads, v3.0](https://www.ieso.ca/-/media/Files/IESO/Document-Library/engage/large-computational-loads/TRLCL-20260903-IESO-Technical-Requirements-for-Large-Computational-Loads-Version-3-0.docx) (2026-09-03, published; projects >10 MW). Being moved into the Market Rules as [MR-00497](https://www.ieso.ca/-/media/Files/IESO/Document-Library/engage/large-computational-loads/TRLCL-20261119-Market-Rule-Amendment-Proposal-Form-MR-00497-R00.pdf) (draft 2026-11-12; target Q2 2027) | "Ramp rates not exceeding **20 MW per minute (maximum 5 MW over any 15-second period)**", same for up and down. Periodic oscillation in the sub-synchronous band not above "the lesser of **±2.5 MW or ±0.25%**" of nominal power. MR-00497 adds: no internal single point of failure that loses more than **600 MW**; a lower ramp rate or staggering may be required for synchronized groups | Prevent "depletion of the AGC fleet. This is a system-wide concern and is independent of connection location or voltage level". Oscillation limit: avoid sub-synchronous torsional and control interaction | P |
| AESO (Alberta) | [Guide to AESO Connection Requirements for Transmission-Connected Data Centres](https://www.aeso.ca/assets/Uploads/grid/Guide-to-AESO-Connection-Requirements-for-Transmission-Connected-Data-Centres.pdf) (2026-06-12, guide) | May be required to keep ramping within "a maximum rate of **10 MW/minute**", up and down, in normal operation and planned outages, measured at the point of connection by PMU. (The 2025-08 draft also had kW-level variability limits, dropped in the final guide) | "Based on the historical and current regulating reserve and TRM volume, 10 MW/minute is the maximum ramp up/down that can be accommodated" | P |
| ATC (Wisconsin) | [Planning Criteria V25, §9.1](http://www.atc10yearplan.com/wp-content/uploads/2026/11/ATC-Planning-Criteria-V25.pdf) (posted 2026-11) and [Load Interconnection Guide Rev 15](https://www.atcllc.com/wp-content/uploads/Load-Interconnection-Guide_Rev-15_Final_082225.pdf) (2025-08-22) | Repetitive changes "<ΔP2 [**25 MW**] for any period of time <T1 [**5**] seconds" in a sliding window. Any change ">P3 [**50**] MW should be limited to <R2 [**0.5**] MW/s", measured as a 1-second average. The guide gives "30 MW/min when connected to the 345-kV system" as an example | ΔP2/T1: "prevent damage to system equipment and … maintain acceptable system voltage and frequency". P3/R2: reserves, scheduling and real-time contingency analysis, so operators can react. Guide: shaft fatigue, inter-area damping | P |
| LIPA / PSEG Long Island | [Performance Requirements for Large Loads Connected to the LIPA System](https://www.nysrc.org/wp-content/uploads/2026/03/NYSRC-LLWG-3-Att.-3-PSEG-Paper.pdf) (issued 2026-02-18; copy filed with NYSRC; loads ≥20 MW) | Ramp ≤**20 MW/minute**, "measured as a change in active power over any 60 second period". Variation, 0-to-peak average over any two adjacent FFT bins: ≤**3.5 MW** in 5.0–55.0 Hz (10 s window); ≤**10.0 MW** in 0.1–5.0 Hz (60 s window); sum of all bins in 0.1–5.0 Hz ≤**20.0 MW** | Not stated beyond "shall not cause amplification" in 0.1–55.0 Hz | P |
| Southern Company | Quoted in the CAISO straw proposal above and in [arXiv:2601.12686](https://arxiv.org/abs/2601.12686). Primary: [Technical Requirements for TCLLs v1.3](https://www.oasis.oati.com/woa/docs/SOCO/SOCOdocs/SOCO_Technical_Requirements_for_TCLLs_-_v1.3_2026-05-01.pdf) (2026-05-01), not opened (certificate error) | ≤20 MW/min in normal operation (loads ≥50 MW, >40 kV); the 75th percentile of 1-minute average ramp also ≤20 MW/min; below 10 MW over a 4–6 s interval; frequency-domain limits per band (values not given) | Energization and step changes must meet rapid-voltage-change limits | S |
| AEP, Dominion, Ameren, PG&E | Summarized in [arXiv:2601.12686](https://arxiv.org/abs/2601.12686) | No numeric ramp limit. AEP: customer submits a load ramp schedule checked against flicker and rapid-voltage-change limits. Dominion: instantaneous voltage fluctuation at the point of interconnection ≤3%, site-specific staged reconnection. Ameren: 2.0% voltage dip at critical buses | Voltage step and flicker (IEEE 1453), not frequency | S |
| NERC | [Level 2 Alert: Large Load Interconnection, Study, Commissioning, and Operations](https://www.nerc.com/pa/rrm/bpsa/Alerts%20DL/NERC%20Alert%20Level%202%20%20Large%20Loads.pdf) (2025-09-09, recommendation) | No numbers. Recommends "operational load ramp limits … for normal and Emergency System states"; the questionnaire asks for limits in MW/min | Limit the load that can disconnect for a single credible contingency; oscillation interaction with system modes | P |
| NERC | [Level 3 Essential Action: Computational Load Modeling, Studies, Instrumentation, Commissioning, Operations, Protection, and Control](https://www.nerc.com/globalassets/programs/bpsa/alerts/level-3-computational-load-alert.pdf) (2026-05-04; reports due 2026-08-03; not a Reliability Standard) | No limit. Requires "Expected maximum ramp rate (MW/min) in down-ramp and up-ramp" as modeling data. Commissioning test of at least a 10% change from nominal voltage. Draft scope: loads 20 MW and greater, connected at 60 kV, with more than 1 MW of IT load | Entities "generally did not have sufficient processes"; aggregate loss "including customer-initiated load reductions" must be added to contingency files | P |
| NERC Large Loads Working Group | [Reliability Guideline: Risk Mitigation for Emerging Large Loads](https://www.nerc.com/globalassets/our-work/guidelines/reliability/RG_Risk-Mitigation-For-Emerging-Large-Loads.pdf) (2026-05, final, voluntary) | No limit. At a minimum, set "operational load ramp rate limits (e.g., MW/min) … in normal and post-disturbance scenarios". Keep the frequency zenith of customer-initiated load reduction events below **60.6 Hz**. Cycling in "0.1–2 Hz" risks forced oscillation; fluctuation in "five to 60 Hz" matters near large turbine generators | An "unpredictable 500 MW load surge or drop" causing ACE excursions; generator over-frequency trips; forced oscillation and sub-synchronous interaction | P |
| NERC Large Loads Task Force | [Characteristics and Risks of Emerging Large Loads](https://www.nerc.com/comm/RSTC_Reliability_Guidelines/Whitepaper%20Characteristics%20and%20Risks%20of%20Emerging%20Large%20Loads.pdf) (2025-07, white paper) | No limit. Measured: a 50 MW block of a 200 MW AI training site ramping at "1.9 p.u. per second for about 250 milliseconds" | "Large load ramp rates may cause issues with frequency regulation by outstripping the reserves held to regulate frequency" | P |
| Industry (Microsoft, OpenAI, NVIDIA and others) | [Power Stabilization for AI Training Datacenters, arXiv:2508.14318](https://arxiv.org/abs/2508.14318) | Describes the *structure* of utility specifications without naming a utility: ramp-up and ramp-down rate in MW/s, dynamic power range, and a frequency-domain cap, with example values "0.1–20 Hz" and "20% of total harmonic energy". Notes utilities compare planned and actual power over 5- to 15-minute scheduling intervals | Resonance with turbine-generator shafts and long lines | P |

### Ride-through and post-disturbance recovery

| Who | Document (date, status) | Requirement as written | Stated rationale | Mark |
|---|---|---|---|---|
| ERCOT | [NOGRR 282](https://www.ercot.com/mktrules/issues/NOGRR282) / [NPRR 1308](https://www.ercot.com/mktrules/issues/NPRR1308), Large Computational Load Ride-Through ([board item](https://www.ercot.com/files/docs/2025/12/01/6.2-NOGRR282-Large-Electronic-Load-Ride-Through-Requirements-and-NPRR1308.pdf), [2026-02 working-group slides](https://www.ercot.com/files/docs/2026/03/02/04_LEL-RT-Requirements_SPWG_Feb2026.pdf)). Approved by the Texas commission 2026-07-09, effective 2026-08-01. NOGRR 289 (pending) would give cooling load 365 days to comply | Applies to loads ≥75 MW with ≥50% computational load. Frequency: continuous 58.8–61.2 Hz; 299 s in 57.0–58.8 and 61.2–61.8 Hz. Voltage (per unit): continuous 0.90–1.10; 2.0 s at 0.80–0.90 and 1.10–1.20; 0.5 s at 0.50–0.80; 0.25 s at 0.20–0.50; 0.15 s below 0.20. Return to 90% of pre-disturbance consumption within 2 s of voltage recovering above 0.9 (an earlier 2025 draft said 1 s). Counting voltage sags to trigger transfer is prohibited | Several loads tripping in the same disturbance; 26 ride-through events identified since 2023; the counting ban cites "risk as seen in northern Virginia events" | P |
| CAISO | Draft tariff language §25.7.1 (as above) | Recover to ≥90% "within three (3) seconds" of voltage returning to 0.90 pu. Frequency: continuous 58.8–61.2 Hz, 299 s out to 57.0 / 61.8 Hz. Voltage (pu): 2.0 s at 1.1–1.2; 6.0 s at 0.7–0.9; 3.0 s at 0.5–0.7; 1.2 s at 0.25–0.5; 0.15 s below 0.25. No voltage tripping on measurements filtered over less than one cycle | — | P |
| PJM | [Manual 14B Attachment D-2, LCL ride-through, draft](https://www.pjm.com/-/media/DotCom/committees-groups/committees/pc/2026/20261006/20261006-item-07-b---1-lcl-ride-through-requirements-solution---presentation.pdf) (2026-10-06 Planning Committee; [September redline](https://www.pjm.com/-/media/DotCom/committees-groups/committees/pc/2026/20260915/20260915-item-03---2-lcl-ride-through-requirements-proposed-language---redline.pdf); for new projects from 2027-01-16) | Applies to facilities of 50 MW or more with 25 MW or more served through power electronics. Voltage (pu): 1.0 s at 1.10–1.20; 2.0 s at 0.80–0.90; 0.5 s at 0.50–0.80; 0.25 s below 0.50. Recover to ≥90% "within two (2) seconds". If a sag-counting transfer scheme is unavoidable it must withstand "a minimum of six (6) voltage sags or swells occurring within a 90-second period". Frequency 58.8–61.2 Hz continuous, 299 s outside. Ramp-rate requirements scheduled for 2027 | The 2026-07-22 Dominion-area event; "magnitude of load that could transfer or be lost during a disturbance" | P |
| SPP | [High Impact Large Load Ride-Through Requirements](https://www.spp.org/documents/74635/spp%20hill%20fault%20ride%20through%20requirements-v1.0-8-19-2025%20%28updated%20version%29.docx) (2025-08, v0.1 per the document; HILL process approved by FERC 2026-01-14) | Applies to ≥10 MW at ≤69 kV or ≥50 MW above 69 kV. Voltage (pu): 0.50 s at 1.10–1.20; continuous 0.90–1.10; 2.00 s at 0.80–0.90; 0.50 s at 0.50–0.80; 0.15 s below 0.50. Return to ≥90% "after **5 cycles** of voltage recovery (0.9 pu or greater)". Frequency 58.8–61.2 Hz continuous, 299 s out to 57.0 / 61.8 Hz. Constant current, not constant power, during disturbances | Uncontrolled load tripping "may cause or exacerbate cascading outages" | P |
| ATC | Planning Criteria V25, Table 9.2-1 (as above) | Voltage (pu): 1 s above 1.10; 3 s below 0.90; 2.5 s below 0.70; 1.2 s below 0.5; 0.15 s below 0.25. Must ride through 3 events within 10 s | — | P |
| LIPA / PSEG Long Island | Performance Requirements (as above) | Return to at least 90% of pre-disturbance consumption "within one second of voltage recovery to 0.90 per unit" | — | P |
| AESO | Connection guide (as above) | "The default active power recovery time is within one second." Rate of change of frequency withstand ≤5.0 Hz/s | — | P |
| ENTSO-E | [Position on the need for national connection requirements, Annex A: data centres](https://eepublicdownloads.blob.core.windows.net/public-cdn-container/clean-documents/Publications/Position%20papers%20and%20reports/2025/251211_SDC_Position_paper_on_CNC_2.0.pdf) (approved 2025-12-11; recommended minimum national requirements, not binding; data centres above 1 kV) | Continuous 0.9–1.1 pu (1–110 kV). Rate of change of frequency withstand ±4.0 Hz/s over 0.25 s, ±2.0 over 0.5 s, ±1.5 over 1 s, ±1.25 over 2 s. Recovery magnitude set by the system operator "within the range from 80% to 100%", time "from 0.5 seconds to 5 seconds". Oscillation limits over "0.01 Hz to 50 Hz". Under-frequency response: droop 2–12%, threshold 49.8 Hz (49.5 Hz in Ireland and the Nordics), response ≤0.5 s. Ramp: the operator "shall be able to specify both up and down ramp limits", no number | Island-mode switching during minor disturbances "may potentially remove several GW of load"; over-activation of frequency containment reserve; inter-area and torsional oscillation | P |
| IESO | Technical Requirements v3.0 (as above) | Default recovery to pre-disturbance level within 1 s; the ramp limit does not apply to this recovery. No automatic reconnection from backup generation without approval. Rate of change of frequency withstand ≤5.0 Hz/s | — | P |
| EirGrid / CRU (Ireland) | [Grid Code modification MPID 345](https://www.eirgrid.ie/sites/default/files/publications/MPID345-Grid-Code-Modification-Proposal-Form.pdf) (proposal 2025-11-17; regulator approval 2026-09-22 per [legal summary](https://www.arthurcox.com/insights/energy-update-cru-decision-on-new-requirements-for-demand-customers-fault-ride-through/)) | Return to at least 90% of pre-fault demand within 500 ms of voltage recovering to 90% (first draft said 95%). Withstand rate of change of frequency up to 1 Hz/s over a rolling 500 ms. Post-fault ramp-up rate "coordinated and agreed" with the system operator, no number | **Contingency size**: loss of a 500 MW interconnector export plus consequential data-centre load reduction could be "double the historic maximum imbalance"; island system | P (text), S (approval) |
| AEMC (Australia) | [Improving the NEM access standards – Package 2, final determination](https://www.aemc.gov.au/sites/default/files/2026-11/final_determination_-_rule_change.pdf) (rule in force from 2026-11-12, six-month grace period; [draft](https://www.aemc.gov.au/sites/default/files/2026-03/Draft%20determination%20-%20Package%202.pdf) 2026-03-12) | Large inverter-based load: "nameplate rating of 30 MW or more", clusters included. Automatic standard: return "to at least 90 per cent of the pre-disturbance level within 500 ms after the end of the disturbance". The minimum standard for active power recovery (1 s in the draft) is removed; recovery is negotiated below the automatic standard | 500 ms "aligns with the fastest achievable recovery"; the draft cited the cost of extra 1-second frequency control ancillary service | P |
| NERC | [Incident Review: Considering Simultaneous Voltage-Sensitive Load Reductions](https://nerc.com/pa/rrm/ea/Documents/Incident_Review_Large_Load_Loss.pdf) (event of 2024-07-10) | No limit. About 1,500 MW of data-centre load transferred off-grid by customer-side protection after six faults in 82 s on a 230 kV line. Recommends that operating agreements "include ramp rates when connecting/reconnecting large loads" | "Ramp rates for load connection are just as critical to system operations as generation ramping" | P |

### What the documents have in common

These observations summarize the rows above and nothing else.

- **Three separate time scales are being written as three separate limits.** Minute-scale ramp in MW/min (CAISO over a rolling 10 minutes, LIPA over 60 s, IESO with a 15-second sub-window, ATC as MW/s). Second-scale variation as MW in a rolling window (ERCOT 10 MW in 5 s, ATC 25 MW in 5 s). Frequency-domain limits per band in MW or percent (IESO, LIPA).
- **The minute-scale numbers converge on 20 MW/min** (CAISO, IESO, LIPA, Southern). AESO, at 10 MW/min, is the tighter outlier; ATC's 0.5 MW/s equals 30 MW/min.
- **None of the documents writes the ramp limit in 5- or 15-minute dispatch intervals.** Those intervals appear only as the window over which utilities compare scheduled and actual power.
- **Ramp limits are justified by regulation reserve, not by the largest contingency.** CAISO cites regulation reserve and the primary-response deadband, IESO depletion of the AGC fleet, AESO regulating reserve and transmission reliability margin, NERC reserves held to regulate frequency.
- **Contingency size justifies ride-through and recovery time instead.** EirGrid's case is the clearest: one interconnector fault plus consequential load loss. IESO's 600 MW single-point-of-failure cap and PJM's response to the July 2026 event follow the same logic.
- **Second-scale and frequency-domain limits are justified by generator shaft torsional stress and inter-area oscillation.**
- **Limits are stated in absolute MW, not as a share of site capacity.** The only percentage ramp found is ERCOT's withdrawn 2023 proposal, which is also the only one with different up and down rates.
- **Recovery times range from about 83 ms to 3 s, and system size does not explain the spread.** SPP: 5 cycles. Ireland and Australia: 500 ms. Ontario, Alberta, Long Island: 1 s. Texas and PJM: 2 s. California: 3 s. ENTSO-E leaves 0.5–5 s to each operator.
- **Draft rules are becoming tariff and market rules.** In 2026, ERCOT's ride-through took effect, Australia's rule commenced, CAISO and IESO moved their requirements into tariff and market-rule text, and PJM drafted manual language. Most of the US moves answer FERC's June 2026 show-cause orders.
- **Transmission owners with voltage-driven concerns give no MW/min number** and review a site-specific ramp schedule against flicker limits.
- **Ride-through windows are being written against sag-counting transfer schemes**: ERCOT prohibits counting, and PJM requires at least six sags or swells in 90 s, citing northern Virginia events.

Two inconsistencies between secondary sources, left unresolved: the CAISO straw proposal lists "ERCOT: 20 MW/min" as industry practice, while the survey in arXiv:2601.12686 says ERCOT defines no explicit step or ramp limit.

No numeric requirement was found for China, the United Kingdom, Singapore, MISO or NYISO. MISO filed large-load reliability requirements at FERC on 2026-08-28 (see leads). That is a gap in this search, not evidence that none exists.

---

## Projects, programs and products

### China

| Name | Who | Year | Type | What it does, with the scale the source states | Mark |
|---|---|---|---|---|---|
| [Notice on orderly development of green power direct connection (发改能源〔2025〕650号)](https://www.ndrc.gov.cn/xxgk/zcfb/tz/202505/t20250530_1398138.html) | NDRC, NEA | 2025 | Policy | Defines "green power direct connection": renewable generation supplies a single user over a dedicated line instead of the public grid, with physically traceable energy; grid-connected and off-grid variants | P |
| [Action plan on mutual empowerment of AI and energy (关于促进人工智能与能源双向赋能的行动方案)](https://www.ndrc.gov.cn/wsdwhfz/202605/t20260515_1405213.html) | NDRC, NEA, MIIT, National Data Administration | 2026 | Policy | Calls for a compute–power interaction mechanism and for computing facilities to take part in grid operation as adjustable demand-side resources. Scale not stated (official interpretation page read) | P |
| [Action plan for a new-type power system, 2024–2027 (发改能源〔2024〕1128号)](https://www.ndrc.gov.cn/xxgk/zcfb/tz/202408/t20240806_1392258.html) | NDRC, NEA, National Data Administration | 2024 | Policy | Nine special actions; the compute–power coordination clauses sit in the attachment, which was not read | P (title and issuing bodies only) |
| [Special action plan for green and low-carbon data centers (发改环资〔2024〕970号)](https://www.ndrc.gov.cn/fggz/fgzy/xmtjd/202407/t20240730_1392078.html) | NDRC and three other ministries | 2024 | Policy | Coordinates large wind and solar bases with national computing hub nodes (interpretation page read; quantitative targets not confirmed) | P (partly) |
| [Lingang intelligent computing center compute–power coordination project (临港智算中心算电协同项目)](https://www.stdaily.com/web/gdxw/2026-07/31/content_557249.html) | Shanghai Damao Technology | 2026 | Demonstration | Four demand-response rounds in July 2026. On 10 July it offered **23 MW** of peak reduction and delivered **22.84 MW** | P |
| [Shanghai concentrated dispatch of 16 data centers](https://paper.people.com.cn/zgnyb/pc/content/202607/20/content_30170410.html) | State Grid Shanghai with China Telecom Shanghai, GDS, INESA, Alibaba and others | 2026 | Demonstration | 16 data centers dispatched together; maximum load reduction of **97.8 MW (9.78万千瓦) within two hours**. Data centers on the Shanghai virtual-power-plant platform declared **162.1 MW** of adjustable capacity | P |
| [Qinghai green compute–power dispatch center (青海绿色算电调度中心)](https://paper.people.com.cn/zgnyb/pc/content/202607/27/content_30171890.html) | Qinghai Province | 2024 | Demonstration | Millisecond-level monitoring of 18,000 servers. A cross-province dispatch test moved about 2 PFLOPS of compute and added about 984 kWh of green-power consumption; adjustable load of one supercomputing center about 1 MW ([earlier report](https://www.chinanews.com.cn/cj/2026/05-20/10625413.shtml) said 17,000 servers) | P |
| [Yangzhou city-level compute–power coordination platform (扬州城市级算电协同平台)](https://www.stdaily.com/web/gdxw/2026-10/28/content_604230.html) | State Grid Yangzhou, Yangzhou Big Data Group | 2026 | Platform | In operation from 2026-10-28; links 24 compute pools (16,000 PFLOPS). Shifting adjustable tasks to midday green-power hours is reported to cut carbon by about 50% and energy cost by about 15%. MW not stated | P |
| [Horinger data-center cluster green-energy supply demonstration (和林格尔数据中心集群绿色能源供给示范项目)](https://www.news.cn/fortune/20260622/1de21d9921d242e4a551630eb8825b8a/c.html) | China Huadian | 2026 | Demonstration | Phase 1: **360 MW** of wind and solar with storage connected; **860 MW** planned by end-2026 for 48,000 P of compute, delivered over a 41 km dedicated line | P |
| [NEA: green-power direct connection for computing facilities](https://www.ncsti.gov.cn/kjdt/kjrd/202611/t20261104_261170.html) | National Energy Administration | 2026 | Policy status | By end-September 2026, 24 provinces had issued supporting rules and **12** computing-facility direct-connection projects were approved, over 10% of all approved direct-connection projects (People's Daily article, syndicated) | P |
| [Compute–power coordination pilot tasks (算电协同先行先试任务)](https://www.ndrc.gov.cn/xxgk/jianyitianfuwen/qgrddbjyfwgk/202511/t20251120_1401790.html) | National Data Administration | 2024 | Pilot program | Pilot tasks at the Beijing–Tianjin–Hebei, Yangtze River Delta, Inner Mongolia and Ningxia hub nodes on multi-source complementarity and source–load interaction. Scale not stated (NDRC reply to an NPC proposal; the original notice was not found) | P |
| [Compute–power coordination technology white paper (算电协同技术白皮书)](https://www.gfnds.com/uploads/20250818/63c414d3d2082ded22487edace5ca3ed.pdf) | BUPT, Purple Mountain Laboratories, with State Grid Shandong, CEPRI, China Unicom and others | 2025 | White paper | Architecture and scenarios. Cites an *estimate* that China's data centers could offer about 30 GW of flexibility, and Guangdong trading-center data of 450 GWh of spot trades by compute aggregators in H1 2025 | P |
| [Draft group standard: technical requirements for compute–power coordinated control in green data centers (绿色数据中心算电协同调控系统技术要求，征求意见稿)](https://www.ces.org.cn/res/ces/2411/c30a8c5eefbf2c5649d20871a8770dad.pdf) | China Electrotechnical Society; drafted by North China Electric Power University, Alibaba Cloud, State Grid units and others | 2024 | Standard (draft) | Scope: task scheduling and compute-resource management under compute–power coordination. No quantitative thresholds; no final publication found | P |
| [Datang Zhongwei cloud-base green power supply project (大唐中卫云基地数据中心绿电供应项目)](https://www.news.cn/20260510/a6e3c641477a4026a402a00d58eaa3b1/c.html) | China Datang | 2026 | Demonstration | 2 GW of renewables for a data-center cluster: 500 MW of solar connected, 1.5 GW of wind under construction; "physical direct supply plus bilateral trading" | P |
| [Green Computing Co-creation Alliance (绿色算力共创联盟)](https://finance.sina.com.cn/jjxw/2026-05-17/doc-inhyekzt3783490.shtml) | China Mobile Liaoning with regional generation companies and cloud providers | 2026 | Alliance | Founded 2026-05-15 to run computing when green power is plentiful and prices are low. Scale not stated (syndicated page read) | P |

### International

| Name | Who | Year | Type | What it does, with the scale the source states | Mark |
|---|---|---|---|---|---|
| [Carbon-intelligent computing platform](https://blog.google/inside-google/infrastructure/data-centers-work-harder-sun-shines-wind-blows/) | Google | 2020 | Internal platform | Shifts non-urgent compute tasks to hours with more wind and solar, first in time within a site. MW not stated | P |
| [Data center demand response](https://cloud.google.com/blog/products/infrastructure/using-demand-response-to-reduce-data-center-power-consumption) | Google with utilities in Europe, Taiwan and the US | 2022–2023 | Operator program | Moves non-urgent tasks away during grid stress; daily evening reductions in five European countries in winter 2022–23. MW not stated | P |
| [Demand response agreements for machine-learning workloads](https://blog.google/innovation-and-ai/infrastructure-and-cloud/global-network/how-were-making-data-centers-more-flexible-to-benefit-power-grids/) | Google, Indiana Michigan Power, TVA | 2025 | Operator program | Formal utility agreements covering ML workloads. MW not stated | P |
| [DCFlex](https://dcflex.epri.com/) | EPRI with utilities, system operators and hyperscalers | 2024 | Initiative | "Nine active demonstration sites"; five workstreams from flexible data-center design to interconnection practices | P |
| [Phoenix field demonstration of Emerald Conductor](https://blogs.nvidia.com/blog/ai-factories-flexible-power-use) | Emerald AI, NVIDIA, Oracle Cloud Infrastructure, Salt River Project, under EPRI DCFlex | 2025 | Demonstration | A cluster of **256 GPUs** cut power by **25% for three hours** on 3 May 2025 during peak demand | P |
| [London AI grid-flexibility trial](https://nationalgrid-newsroom.prgloo.com/news/uk-first-trial-of-ai-grid-technology-successfully-demonstrates-the-ability-of-data-centres-to-adjust-power-needs) | National Grid, Emerald AI, EPRI (DCFlex), Nebius, NVIDIA | 2025 | Demonstration | Five days in December 2025: more than 200 simulated grid events sent to a cluster of **96 GPUs**, cutting demand by **up to 40%** while critical workloads kept running | P |
| [Iceland grid-responsive AI pilot](https://www.emeraldai.co/blog/emeraldai-nvidia-nscale-demonstrate-grid-responsive-ai-demo-iceland) | Emerald AI, NVIDIA, Nscale | 2026 | Demonstration | Cut power of the racks under test by **about 25% for 30 minutes**, matching an EPRI Flex MOSAIC Class B event. GPU count and MW not stated | P |
| [Grid-interactive UPS at a Dublin datacenter](https://news.microsoft.com/source/?p=782) | Microsoft, Eaton, Enel X | 2022 | Demonstration | Datacenter UPS batteries offer fast frequency response in the Irish grid-services market through Enel X; proof of concept in Chicago in 2020. MW not stated | P |
| [Google–Voltus agreement](https://blog.google/company-news/outreach-and-initiatives/sustainability/voltus-agreement/) | Google, Voltus | 2026 | Operator program | Three-year agreement to "unlock up to 100 megawatts" of capacity in PJM through a virtual power plant | P |
| [AI Energy Management Alliance](https://blogs.nvidia.com/blog/ai-energy-management-alliance/) | Emerald AI, Google, NVIDIA and launch partners | 2026 | Alliance | Founded 2026-09 to build a common performance framework and interconnection practice for grid-responsive data centers. Scale not stated | P |
| [ERCOT: leveraging load flexibility](https://www.esig.energy/attachment/serve/ercot-operations-leveraging-load-flexibility-for-grid-reliability_update-06-18-2026) | ERCOT | 2026 | Operator program | Large loads can register as Controllable Load Resources (aggregations of sites each under 10 MW allowed); a curtailment manager for co-located large loads is in development. ERCOT tracks about **438 GW** of large-load requests, about 89% of them data centers. Registered CLR MW not stated | P |
| [Lancium Clean Campus, Abilene](https://www.esig.energy/wp-content/uploads/2025/05/ESIG_LLTF_PresentationLancium.pdf) | Lancium | 2025 | Flexible campus | **1,200 MW** campus approved by AEP and ERCOT, with a planned 360 MW gas plant and a **1,000 MW / 4,000 MWh** battery. Lancium says it delivered the first load-only Controllable Load Resource | P |
| [Soluna Project Dorothy](https://www.solunacomputing.com/projects/project-dorothy/) | Soluna | 2023 | Flexible campus | **100 MW** data center at a Texas wind farm (50 MW live, 50 MW under construction per the project page); software curtails load for the grid | P |
| [Colossus 2 battery storage](https://www.canarymedia.com/articles/batteries/xai-massive-battery-memphis-data-center) | xAI, Tesla | 2026 | Behind-the-meter storage | Satellite count of 720 Megapacks, estimated by the reporter at 2.8 GWh and 720–1,400 MW; an xAI representative told the TVA board 3.3 GWh. No official disclosure | S |
| [CRU decision on data-centre connections (CRU2025236)](https://www.williamfry.com/knowledge/cru-publishes-long-awaited-final-policy-on-data-centre-connections/) | CRU, applied by EirGrid | 2025 | Policy | Data centres above 1 MVA must bring dispatchable on-site or nearby generation or storage (1–10 MVA: sized to 100% of import capacity, de-rated); 80% of annual demand from additional Irish renewables. Compliant sites are exempt from mandatory demand curtailment (law-firm summary; decision not opened) | S |
| [PJM board decision on integrating large loads](https://insidelines.pjm.com/pjm-board-outlines-plans-to-integrate-large-loads-reliably/) | PJM | 2026 | Operator program | 2026-01-16: new large loads may bring their own new generation or accept a "connect and manage" framework with earlier curtailment | P |
| [FERC order on PJM large loads, ER26-3515](https://www.pjm.com/pjmfiles/directory/etariff/FercOrders/9207/20261009-er26-3515-000.pdf) | FERC, PJM | 2026 | Regulatory decision | 2026-10-09: accepted a Large Load definition and Large Load Registry effective 2026-10-12, with a compliance filing due in 30 days. Which parts of the January plan were rejected was not checked in the order | P |
| [Software Carbon Intensity, ISO/IEC 21031:2024](https://greensoftware.foundation/articles/sci-specification-achieves-iso-standard-status/) | Green Software Foundation | 2024 | Standard | Method for computing the carbon intensity of software; excludes offsets | P |

### Observations

- Outside China, the trials that publish numbers are rack- or cluster-scale: 256 GPUs in Phoenix, 96 GPUs in London, unstated rack count in Iceland. They report the depth of reduction (25–40%) and its duration, but not MW.
- The largest measured load-side result found is in China: 97.8 MW across 16 Shanghai data centers in two hours. The 23 MW Lingang result is one site.
- China's published activity is still weighted to the supply side: direct green-power supply at hundreds of MW to GW scale, and 12 approved direct-connection projects for computing facilities.
- Outside China, flexibility at hundreds of MW is so far *capacity on paper*: a 1,000 MW battery planned at Lancium's campus, estimated battery capacity at Colossus 2, 100 MW in the Google–Voltus agreement. None has published a dispatch record.
- Operator rules increasingly trade flexibility or self-supply for faster connection: PJM's connect-and-manage option, Ireland's on-site generation condition, ERCOT's Controllable Load Resources.

---

## Patents

Grouped by what is claimed. Year is the earliest priority found, or the filing year where marked "(filed)". US rows are **R**: number, title and assignee were checked against USPTO Patent Public Search or the USPTO front-page PDF. Chinese rows are in [their own subsection](#chinese-patents) and are **P**: the Google Patents page of each document was opened.

Not repeated here because they are already in [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling#patents): US11966273B2, US12562573B2, US20260118930A1, US20250338456A1, US20260141222A1, US20260079555A1, US20250190042A1 and eight others on power smoothing and capping.

### Grid- and carbon-aware workload scheduling

- **[US11644804B2](https://patents.google.com/patent/US11644804B2)** — Compute load shaping using virtual capacity and preferential location real time scheduling. Google, 2019, granted. Sets hourly "virtual capacity" limits per cluster from load forecasts and power models, moving deferrable tasks in time or location.
- **[US9886316B2](https://patents.google.com/patent/US9886316B2)** — Data center system that accommodates episodic computation. Microsoft, 2010, granted. Moves data and computation between data centers as renewable and grid supply vary.
- **[US9063738B2](https://patents.google.com/patent/US9063738B2)** — Dynamically placing computing jobs. Microsoft, 2010, granted. Places jobs across data centers by electricity cost.
- **[US10928845B2](https://patents.google.com/patent/US10928845B2)** — Scheduling a computational task for performance by a server computing device in a data center. Microsoft, 2010, granted. Schedules tasks from a forecast of renewable generation.
- **[US12136001B2](https://patents.google.com/patent/US12136001B2)** — Distributed computing with variable energy source availability. Microsoft, 2021, granted.
- **[US12086650B2](https://patents.google.com/patent/US12086650B2)** — Workload placement based on carbon emissions. Pure Storage, 2021 (filed), granted.
- **[US20250060996A1](https://patents.google.com/patent/US20250060996A1)** — Dynamic load scheduling using carbon intensity decomposition. IBM, 2023 (filed), application.
- **[US12608718B2](https://patents.google.com/patent/US12608718B2)** — Steering compute workloads based on carbon costs. Hewlett Packard Enterprise, 2023 (filed), granted 2026. Computes a carbon-cost metric for each server and labels container-platform nodes, so that workloads migrate when the carbon cost falls below a threshold.
- **[US12657073B2](https://patents.google.com/patent/US12657073B2)** — Workload management among candidate distributed computing environments based on governance policies. Accenture, 2023 (filed), granted 2026. Recommends where to run a workload from the carbon intensity of each candidate environment.
- **[US20260030636A1](https://patents.google.com/patent/US20260030636A1)** — Renewable-aware preliminary data center combination selection and application relocation method. Hitachi Vantara, 2024 (filed), application. Pairs data centers whose past renewable supply complements each other, then places replicas and migrates workloads between them.
- **[US20260219943A1](https://patents.google.com/patent/US20260219943A1)** — System and method for energy-aware orchestration of distributed artificial intelligence compute using energy telemetry. Solyx AI, 2025, application. Sets where, when and how hard AI workloads run from real-time and forecast energy mix, price, carbon intensity, storage and grid signals.

### Data center as a flexible grid resource

- **[US9003216B2](https://patents.google.com/patent/US9003216B2)** — Power regulation of power grid via datacenter. Microsoft, 2011, granted. Raises or lowers data-center consumption to follow grid supply and demand.
- **[US11036250B2](https://patents.google.com/patent/US11036250B2)** — Datacenter stabilization of regional power grids. Microsoft, 2019, granted. Controls data-center batteries from regulation signals and market conditions.
- **[US20230367653A1](https://patents.google.com/patent/US20230367653A1)** — Systems and methods for grid interactive datacenters. Microsoft, 2022, application.
- **[US9691112B2](https://patents.google.com/patent/US9691112B2)** — Grid-friendly data center. IBM and Universiti Brunei Darussalam, 2013, granted. Computes a power budget from grid state and price forecasts.
- **[US20130035795A1](https://patents.google.com/patent/US20130035795A1)** — System and method for using data centers as virtual power plants. 2012 (filed), application.
- **[US20240186823A1](https://patents.google.com/patent/US20240186823A1)** — Electrical grid primary frequency response via a flexible data center. US Data Mining Group, 2023 (filed), application.
- **[US10608433B1](https://patents.google.com/patent/US10608433B1)** — Adjusting power consumption based on a fixed-duration power option agreement. Lancium, 2019, granted.
- **[US11016456B2](https://patents.google.com/patent/US11016456B2)** — Dynamic power delivery to a flexible datacenter using unutilized energy sources. Lancium, 2018, granted.
- **[US20230061162A1](https://patents.google.com/patent/US20230061162A1)** — Data center load supervisor. NVIDIA, 2021 (filed), application. Adjusts component operating parameters to available grid capacity.
- **[US20260244484A1](https://patents.google.com/patent/US20260244484A1)** — Flexible computing rack for interruptible artificial intelligence computing in data centers. HammerheadAI, 2026 (filed), application.
- **[US12482012B2](https://patents.google.com/patent/US12482012B2)** — Robust dispatch method for flexibility resources of large-scale data center microgrid cluster. Shenzhen Polytechnic University, 2023, granted.

### Power capping along the power-delivery hierarchy

- **[US9880599B1](https://patents.google.com/patent/US9880599B1)** — Priority-aware power capping for hierarchical power distribution networks. IBM, 2016 (filed), granted.
- **[US12072749B2](https://patents.google.com/patent/US12072749B2)** — Machine learning-based power capping and virtual machine placement in cloud platforms. Microsoft, 2019, granted.
- **[US11971774B2](https://patents.google.com/patent/US11971774B2)** — Programmable power balancing in a datacenter. NVIDIA, 2020 (filed), granted.
- **[US10277523B2](https://patents.google.com/patent/US10277523B2)** — Dynamically adapting to demand for server computing resources. Facebook, 2016 (filed), granted.

### Ramp and swing mitigation

- **[US10216245B2](https://patents.google.com/patent/US10216245B2)** — Application ramp rate control in large installations. Cray, 2015, granted. Coordinates processors to remove power swings at job start and stop.
- **[US11868106B2](https://patents.google.com/patent/US11868106B2)** — Granular power ramping. Lancium, 2019, granted. Steps an interruptible computing load up and down in stages.

### Workload placement across the power hierarchy

- **[US10528115B2](https://patents.google.com/patent/US10528115B2)** — Obtaining smoother power profile and improved peak-time throughput in datacenters. Facebook, 2017, granted. Scores how asynchronous servers' power patterns are and places services with offset peaks under the same power node.
- **[US11561815B1](https://patents.google.com/patent/US11561815B1)** — Power aware load placement. Amazon, 2020, granted. Places virtual machine instances by the utilization of each power line-up.
- **[US12386409B2](https://patents.google.com/patent/US12386409B2)** — Power-aware scheduling in data centers. NVIDIA, 2023 (filed), granted. Places a process on the rack with the most available power capacity.

### Storage and backup systems tied to workload

- **[US11868191B1](https://patents.google.com/patent/US11868191B1)** — Battery mitigated datacenter power usage. Amazon, 2020 (filed), granted.
- **[US11327549B2](https://patents.google.com/patent/US11327549B2)** — Improving power management by controlling operations of an uninterruptible power supply in a data center. Dell, 2019, granted.

### Chinese patents

Title in English translation, with the Chinese title as filed. Year is the filing date shown on Google Patents. B = granted, A = published application.

- **[CN120691373B](https://patents.google.com/patent/CN120691373B/zh)** — Compute–power coordination system and method (一种算电协同系统及方法). 湖北邮电规划设计有限公司, 2025, granted. Forecasts power supply, including renewables, and compute demand, matches the two, and shifts tasks in time and location.
- **[CN120672091B](https://patents.google.com/patent/CN120672091B/zh)** — Information interaction method and system for coordinated compute and power scheduling in data centers (一种数据中心算力与电力协同调度的信息交互方法及系统). 中国科学院大学, 2025, granted. Co-optimizes compute, power and heat with reinforcement learning plus mixed-integer programming, and records carbon footprint and green-power certificates on a blockchain.
- **[CN120073810B](https://patents.google.com/patent/CN120073810B/zh)** — Compute-load smoothing and energy-saving management system based on flywheel storage (基于飞轮储能系统的算力负荷平抑和节能管理系统). 微控飞轮（沈阳）技术开发有限公司, 2025, granted. Predicts compute power demand from cluster current harmonics and rack vibration, then modulates a flywheel to cancel bus voltage harmonics and smooth peaks.
- **[CN121055283A](https://patents.google.com/patent/CN121055283A/zh)** — Compute task scheduling based on renewable-energy absorption (基于新能源消纳的算力任务调度方法、装置和存储介质). 清华大学, 2025, application. Predicts the spare output of distributed renewable nodes and schedules compute tasks to use it on site.
- **[CN117374933A](https://patents.google.com/patent/CN117374933A/zh)** — Data-center demand-response scheduling by spatiotemporal shifting of computing load (基于计算负载时空转移的数据中心需求响应优化调度方法). 东南大学 with 国网江苏省电力有限公司, 2023, application. Minimizes electricity cost by shifting load across time and sites, using a per-server energy model.
- **[CN121979665A](https://patents.google.com/patent/CN121979665A/zh)** — Integrated power–compute coordination management based on a virtual power plant (一种基于虚拟电厂的电算协同一体化管理方法及系统). 国网新疆电力有限公司信息通信公司, 2025, application. Tags batch tasks with time window, mobility and priority, and decides when and where they run against cost and carbon ("compute follows power" or "power follows compute").
- **[CN121364938A](https://patents.google.com/patent/CN121364938A/zh)** — Resource control for intelligent computing centers based on compute–power coordination (一种基于算电协同的智算中心资源管控方法、系统及设备). 联通青海绿电智算科技有限公司 and 中国联通, 2025, application. Allocates compute, microgrid output and storage charging against time-of-use prices to minimize total electricity cost.
- **[CN121710173A](https://patents.google.com/patent/CN121710173A/zh)** — Compute–power coordinated regulation method (算电协同调控方法、装置、设备、可读存储介质和程序产品). 中国电信, 2025, application. Predicts grid-side and compute-side states, chooses the lowest-cost compute regulation strategy, and maximizes grid power use per node.
- **[CN118860630A](https://patents.google.com/patent/CN118860630A/zh)** — Compute scheduling method (一种算力调度方法、装置、设备、存储介质及程序产品). 中国移动 and 中国移动研究院, 2024, application. Ranks compute nodes by surplus electric energy and low-carbon priority and routes tasks along the best path.
- **[CN120434159A](https://patents.google.com/patent/CN120434159A/zh)** — Compute-network resource scheduling method (一种算力网络资源调度方法). Listed on Google Patents as State Grid Information & Telecommunication Group, 2025, application. Remaps tasks using node compute, status and energy-index data with link-congestion prediction. Energy is one input among several.
- **[CN116862126A](https://patents.google.com/patent/CN116862126A/zh)** — Compute allocation under the fusion of energy and computing networks (一种能源网络与算力网络融合下的算力分配方法与装置). 中国科学院计算机网络信息中心 with 国家电投集团科学技术研究院, 2022, application. Selects nodes for each request by green-electricity share and remaining capacity.
- **[CN119809034A](https://patents.google.com/patent/CN119809034A/zh)** — Scheduling optimization for green data centers under compute–power coupling (算力电力耦合下绿色数据中心调度优化方法). 北京科技大学 with 华北电力大学, 2024, application. Splits load into shiftable, curtailable and rigid parts and trades electricity cost against renewable matching on a Pareto front.
- **[CN121689043A](https://patents.google.com/patent/CN121689043A/zh)** — Compute–power coordinated grid planning based on reliability and economy (基于可靠性与经济性的算电协同电网规划方法及系统). 国网上海市电力公司, 2025, application. Bi-level planning: grid life-cycle cost above, load loss minimized by shifting or curtailing flexible compute load below.

### Observations

- In the United States the filers are cloud and chip companies. Microsoft's filings span the longest period, from renewable-following scheduling in 2010 to AI training power smoothing in 2023–2024.
- Lancium holds a dense family around behind-the-meter flexible data centers.
- No patent was found on coordinating grid-fault ride-through with the computing workload, in either country. This reflects a limited search.
- Chinese filings titled with 算电协同 cluster in 2025, and come from telecom operators, grid companies and universities rather than cloud companies. Most claim cost- or carbon-optimal scheduling. One, CN121689043A, uses flexible compute load in grid *planning*. One, CN120073810B, does hardware smoothing.

---

## Open-source software and data

All rows are **R**: repository existence, license and description were read from the GitHub API on the "last updated" date.

Not repeated here because they are already in [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling#tools--simulators): Zeus, Vessim, ExaDigiT/RAPS, Google cluster-data and the OpenG2G paper.

### Grid-signal-aware scheduling

- **[Green-Software-Foundation/carbon-aware-sdk](https://github.com/Green-Software-Foundation/carbon-aware-sdk)** — MIT. API and command-line tool that returns the best time and region to run a workload from carbon-intensity data.
- **[Azure/carbon-aware-keda-operator](https://github.com/Azure/carbon-aware-keda-operator)** — MIT. Kubernetes operator that caps autoscaling when carbon intensity is high.
- **[bluehands/Carbon-Aware-Computing](https://github.com/bluehands/Carbon-Aware-Computing)** — MIT. Schedules tasks at the forecast point of lowest grid carbon intensity.
- **[thegreenwebfoundation/grid-intensity-go](https://github.com/thegreenwebfoundation/grid-intensity-go)** — Apache-2.0. Go library and exporter for factoring carbon intensity into where and when to run jobs.
- **[sustainable-computing-io/peaks](https://github.com/sustainable-computing-io/peaks)** — Apache-2.0. Power-efficiency-aware Kubernetes scheduler.
- **[kube-green/kube-green](https://github.com/kube-green/kube-green)** — MIT. Kubernetes operator that shuts down workloads on a schedule.
- **[aashanm/arboric](https://github.com/aashanm/arboric)** — MIT. Defers flexible AI jobs by spot electricity price and marginal emission rate.
- **[sufirehman/carbon-aware-ml-scheduler](https://github.com/sufirehman/carbon-aware-ml-scheduler)** — MIT. Schedules ML training from real-time UK grid carbon-intensity data.
- **[sustainable-computing-io/susql-operator](https://github.com/sustainable-computing-io/susql-operator)** — Apache-2.0. Kubernetes operator that aggregates energy and CO2 data for tagged resources.

### Power measurement and control on the compute side

- **[sustainable-computing-io/kepler](https://github.com/sustainable-computing-io/kepler)** — Apache-2.0. Prometheus exporter for per-workload energy on Kubernetes.
- **[hubblo-org/scaphandre](https://github.com/hubblo-org/scaphandre)** — Apache-2.0. Host and process-level energy metrology agent.
- **[geopm/geopm](https://github.com/geopm/geopm)** — BSD-3-Clause. Global Extensible Open Power Manager: job-level power management for HPC systems.
- **[llnl/variorum](https://github.com/llnl/variorum)** — MIT. Vendor-neutral library exposing power caps and power telemetry across architectures.
- **[flux-framework/flux-power-monitor](https://github.com/flux-framework/flux-power-monitor)** — LGPL-3.0. Power monitoring and management modules for the Flux resource manager.

### Coupled compute–grid simulation

- **[gpu2grid/openg2g](https://github.com/gpu2grid/openg2g)** — Apache-2.0. Simulation library for AI data-center and distribution-grid interaction: trace-replay or live-GPU data-center backend, OpenDSS grid model, and controllers such as batch-size control for voltage regulation.
- **[gpu2grid/live](https://github.com/gpu2grid/live)** — No license. Injects H100 LLM inference and training power profiles into the IEEE 13-bus feeder and solves with OpenDSS; built on openg2g.
- **[dos-group/lets-wait-awhile](https://github.com/dos-group/lets-wait-awhile)** — No license. Simulator and datasets for carbon-aware temporal workload shifting.
- **[atlarge-research/opendc](https://github.com/atlarge-research/opendc)** — MIT. Data-center simulator with power and energy models.
- **[HewlettPackard/dc-rl](https://github.com/HewlettPackard/dc-rl)** — MIT. SustainDC: multi-agent reinforcement-learning environments for workload shifting, cooling and battery control.
- **[facebookresearch/CarbonExplorer](https://github.com/facebookresearch/CarbonExplorer)** — Evaluates combinations of renewables, storage and load shifting for running data centers on renewable energy.
- **[microsoft/vidur](https://github.com/microsoft/vidur)** — MIT. Large-scale simulator for LLM inference systems; **[ozcanmiraay/vidur-energy](https://github.com/ozcanmiraay/vidur-energy)** (MIT) adds energy and carbon accounting.

### Grid data feeds

- **[electricitymaps/electricitymaps-contrib](https://github.com/electricitymaps/electricitymaps-contrib)** — AGPL-3.0. Parsers behind the Electricity Maps carbon-intensity data.
- **[gridstatus/gridstatus](https://github.com/gridstatus/gridstatus)** — BSD-3-Clause. Uniform Python access to data from US system operators.

### Cluster traces with job-to-machine records

Useful for studying how jobs map onto machines, and from there onto power domains.

- **[alibaba/clusterdata](https://github.com/alibaba/clusterdata)** — Production cluster traces, including GPU cluster releases.
- **[Azure/AzurePublicDataset](https://github.com/Azure/AzurePublicDataset)** — CC-BY-4.0. Azure VM, function and LLM inference traces.
- **[msr-fiddle/philly-traces](https://github.com/msr-fiddle/philly-traces)** — CC-BY-4.0. Deep-learning training job traces from a Microsoft cluster.

---

## Leads not yet verified

Seen only in search results or search-index records. The source pages could not be opened when this list was compiled. Listed so that others can check them; **do not cite from here**.

**Patents.** Seen only in search snippets.
- WO2026102424A1 — AI-enabled energy storage appliances; grid frequency regulation for predicted workload swings
- WO2026096027A1 — Filtering data-center power transients caused by AI workloads

**Projects and programs.**
- Registered Controllable Load Resource MW in ERCOT, and the reported PUCT approval of PGRR145 / NPRR1325 (2026-06-18)
- AI Energy Management Alliance launch-partner list (reported as 18 partners in secondary sources)
- 达卯科技 expectation that adjustable resources pass GW scale (signed basis) in Q1 2027 — a forecast

**Grid requirements.**
- Southern Company Technical Requirements for TCLLs v1.3 (2026-05-01): primary link known, not opened
- MISO large-load reliability requirements filed at FERC 2026-08-28 (accession 20260828-5278): reported thresholds >50 MW and ≥25 MW of IT load; a 30 MW/min figure appears only in a pre-filing summary
- CAISO Board approval (2026-10-28) and FERC filing ER27-506 of the large-load tariff: listed in CAISO's own status table, not checked
- FERC show-cause orders EL26-67 to EL26-72 (2026-06-18) and their response schedule
- CRU decision approving EirGrid MPID 345 (2026-09-22): only the law-firm summary was read
- Size of the 2026-07-22 load-loss event in the Dominion area (reported as nearly 4,000 MW)

---

## Contributing

Corrections matter more than additions. If you can open a source that is marked **S** or listed under leads, please open an issue or pull request with the link and the exact sentence.

For new entries: one row or line per entry, a link to the primary source, the number and unit exactly as the source writes them, and the verification mark. Papers belong in the related lists above.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainer has waived all copyright and related rights to this list.
