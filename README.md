# Awesome Compute–Power Coordination (算电协同) [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated review of **deployed projects, grid requirements, patents and open-source software** on coordinating computing workloads (data centers, AI/GPU clusters, computing-power networks) with the electric power system.

Most lists in this space collect papers. This one deliberately does not. It tracks what has been **built, required, claimed or released**: demonstration projects with measured numbers, the ramp-rate and ride-through limits grid operators are writing for large computational loads, patents, and code you can run.

> Last updated: **2026-10-07**. Contributions and corrections welcome — see [Contributing](#contributing).

**Related lists by the same maintainer** (entries there are not repeated here):
- [awesome-large-load-grid](https://github.com/Yuz2023/awesome-large-load-grid) — regulations, dockets and task forces on large-load interconnection (process, cost allocation, policy).
- [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling) — papers, datasets, simulators and patents on AI data center power modeling.

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
| ERCOT | [Interconnection and Grid Analysis Update](https://www.ercot.com/files/docs/2026/09/17/10-Interconnection-and-Grid-Analysis-Update-REVISED.pdf) (2026-09-17, board material) | Will recommend "10 MW per 5 seconds" for power variation in large loads | Fast fluctuation of AI training load can perturb synchronous generator shafts, with risk of fatigue or damage | P |
| ERCOT | NPRR 1191, proposed "Large Load Ramp Rate Limitations", as quoted in a [2023 stakeholder comment](https://www.ercot.com/files/docs/2023/08/31/Galaxy%20comments%20on%201191NPRR.pdf) (2023 proposal; final outcome not checked) | Ramp **down**: lesser of 5% of peak demand or 20 MW/min. Ramp **up**: lesser of 2% of peak demand or 8 MW/min. Controllable load resources: 20% of registered peak per minute | Not stated in the comment | S |
| CAISO and California transmission owners | [Large Load Technical Requirements Straw Proposal](https://stakeholdercenter.caiso.com/InitiativeDocuments/Large-Load-Technical-Requirements-Straw-Proposal-Jun-15-2026.pdf) (2026-06-15, straw proposal) | "Average active power ramp rate … measured over a **rolling 10-minute interval**, shall not exceed **20 MW/min**". Applies to normal operation and post-outage restoration, not to fault response. Low- and high-frequency cycling limits: to be determined | Real-time **regulation reserve** procurement; keeping interconnection frequency within the **±0.036 Hz deadband** so primary frequency response is not triggered routinely | P |
| IESO (Ontario) | [Technical Requirements for Large Computational Loads, v3.0](https://www.ieso.ca/-/media/Files/IESO/Document-Library/engage/large-computational-loads/TRLCL-20260903-IESO-Technical-Requirements-for-Large-Computational-Loads-Version-3-0.docx) (2026-09-03, published; projects >10 MW) | "Ramp rates not exceeding **20 MW per minute (maximum 5 MW over any 15-second period)**", same for up and down. Periodic oscillation in the sub-synchronous band not above "the lesser of **±2.5 MW or ±0.25%**" of nominal power | Prevent "depletion of the AGC fleet. This is a system-wide concern and is independent of connection location or voltage level". Oscillation limit: avoid sub-synchronous torsional and control interaction | P |
| Southern Company | Quoted in the CAISO straw proposal above and in [arXiv:2601.12686](https://arxiv.org/abs/2601.12686) | ≤20 MW/min in normal operation (loads ≥50 MW, >40 kV); the 75th percentile of 1-minute average ramp also ≤20 MW/min; below 10 MW over a 4–6 s interval; frequency-domain limits per band (values not given) | Energization and step changes must meet rapid-voltage-change limits | S |
| ATC (Wisconsin) | Quoted in the CAISO straw proposal | Any active power change above 50 MW limited to under 0.5 MW/s (30 MW/min); below 25 MW over a 5 s interval (attributed to ATC and SPP) | Not given in the quotation | S |
| LIPA / PSEG Long Island | Quoted in the CAISO straw proposal | Frequency-domain content below 10 MW in 0.1–5 Hz and below 3.5 MW in 5–55 Hz | Not given in the quotation | S |
| AESO (Alberta) | Quoted in the CAISO straw proposal | 10 MW/min | Not given in the quotation | S |
| AEP, Dominion, Ameren, PG&E | Summarized in [arXiv:2601.12686](https://arxiv.org/abs/2601.12686) | No numeric ramp limit. AEP: customer submits a load ramp schedule checked against flicker and rapid-voltage-change limits. Dominion: instantaneous voltage fluctuation at the point of interconnection ≤3%, site-specific staged reconnection. Ameren: 2.0% voltage dip at critical buses | Voltage step and flicker (IEEE 1453), not frequency | S |
| NERC | [Level 2 Alert: Large Load Interconnection, Study, Commissioning, and Operations](https://www.nerc.com/pa/rrm/bpsa/Alerts%20DL/NERC%20Alert%20Level%202%20%20Large%20Loads.pdf) (2025-09-09, recommendation) | No numbers. Recommends "operational load ramp limits … for normal and Emergency System states"; the questionnaire asks for limits in MW/min | Limit the load that can disconnect for a single credible contingency; oscillation interaction with system modes | P |
| NERC Large Loads Task Force | [Characteristics and Risks of Emerging Large Loads](https://www.nerc.com/comm/RSTC_Reliability_Guidelines/Whitepaper%20Characteristics%20and%20Risks%20of%20Emerging%20Large%20Loads.pdf) (2025-07, white paper) | No limit. Measured: a 50 MW block of a 200 MW AI training site ramping at "1.9 p.u. per second for about 250 milliseconds" | "Large load ramp rates may cause issues with frequency regulation by outstripping the reserves held to regulate frequency" | P |
| Industry (Microsoft, OpenAI, NVIDIA and others) | [Power Stabilization for AI Training Datacenters, arXiv:2508.14318](https://arxiv.org/abs/2508.14318) | Describes the *structure* of utility specifications without naming a utility: ramp-up and ramp-down rate in MW/s, dynamic power range, and a frequency-domain cap, with example values "0.1–20 Hz" and "20% of total harmonic energy". Notes utilities compare planned and actual power over 5- to 15-minute scheduling intervals | Resonance with turbine-generator shafts and long lines | P |

### Ride-through and post-disturbance recovery

| Who | Document (date, status) | Requirement as written | Stated rationale | Mark |
|---|---|---|---|---|
| ERCOT | NOGRR 282 / NPRR 1308, Large Electronic Load Ride-Through ([board item](https://www.ercot.com/files/docs/2025/12/01/6.2-NOGRR282-Large-Electronic-Load-Ride-Through-Requirements-and-NPRR1308.pdf), [2026-02 working-group slides](https://www.ercot.com/files/docs/2026/03/02/04_LEL-RT-Requirements_SPWG_Feb2026.pdf)). Approval by the Texas commission in July 2026 and effect from 2026-08-01 are reported by secondary sources | Applies to loads ≥75 MW with ≥50% computational load. Frequency: continuous 58.8–61.2 Hz; 299 s in 57.0–58.8 and 61.2–61.8 Hz. Voltage (per unit): continuous 0.90–1.10; 2.0 s at 0.80–0.90 and 1.10–1.20; 0.5 s at 0.50–0.80; 0.25 s at 0.20–0.50; 0.15 s below 0.20. Return to 90% of pre-disturbance consumption within 2 s of voltage recovering above 0.9 (an earlier 2025 draft said 1 s). Counting voltage sags to trigger transfer is prohibited | Several loads tripping in the same disturbance; 26 ride-through events identified since 2023; the counting ban cites "risk as seen in northern Virginia events" | P (text), S (approval dates) |
| CAISO | Straw proposal (as above) | Recover to ≥90% within 3 s of voltage returning to 0.9 pu. Frequency: continuous 58.8–61.2 Hz, 299 s either side. Voltage: 2.0 s above 1.1; 6.0 s below 0.9; 3.0 s below 0.7; 1.2 s below 0.5; 0.15 s below 0.25 | — | P |
| IESO | Technical Requirements v3.0 (as above) | Default recovery to pre-disturbance level within 1 s; the ramp limit does not apply to this recovery. No automatic reconnection from backup generation without approval. Rate of change of frequency withstand ≤5.0 Hz/s | — | P |
| EirGrid / CRU (Ireland) | [Grid Code modification MPID 345](https://www.eirgrid.ie/sites/default/files/publications/MPID345-Grid-Code-Modification-Proposal-Form.pdf) (proposal 2025-11-17; regulator approval 2026-09-22 per [legal summary](https://www.arthurcox.com/insights/energy-update-cru-decision-on-new-requirements-for-demand-customers-fault-ride-through/)) | Return to at least 90% of pre-fault demand within 500 ms of voltage recovering to 90% (first draft said 95%). Withstand rate of change of frequency up to 1 Hz/s over a rolling 500 ms. Post-fault ramp-up rate "coordinated and agreed" with the system operator, no number | **Contingency size**: loss of a 500 MW interconnector export plus consequential data-centre load reduction could be "double the historic maximum imbalance"; island system | P (text), S (approval) |
| AEMC (Australia) | [Improving the NEM access standards – Package 2, draft determination](https://www.aemc.gov.au/sites/default/files/2026-03/Draft%20determination%20-%20Package%202.pdf) (2026-03-12, draft) | Large inverter-based load threshold raised to 30 MW. Recover to 90–110% of pre-disturbance active power within 500 ms (automatic standard) or 1 s (minimum standard) | Slower recovery would require more 1-second frequency control ancillary service | P |
| SPP | High Impact Large Load process (approved by FERC 2026-01-14), ride-through values as summarized in [arXiv:2601.12686](https://arxiv.org/abs/2601.12686) | Applies above 50 MW. Continuous 0.90–1.10 pu; brief operation down to about 0.50 pu; 58.8–61.2 Hz continuous. Constant current rather than constant power during disturbances | — | S |
| NERC | [Incident Review: Considering Simultaneous Voltage-Sensitive Load Reductions](https://nerc.com/pa/rrm/ea/Documents/Incident_Review_Large_Load_Loss.pdf) (event of 2024-07-10) | No limit. About 1,500 MW of data-centre load transferred off-grid by customer-side protection after six faults in 82 s on a 230 kV line. Recommends that operating agreements "include ramp rates when connecting/reconnecting large loads" | "Ramp rates for load connection are just as critical to system operations as generation ramping" | P |

### What the documents have in common

These observations summarize the rows above and nothing else.

- **Three separate time scales are being written as three separate limits.** Minute-scale ramp in MW/min (CAISO over a rolling 10 minutes, IESO with a 15-second sub-window). Second-scale variation as peak-to-peak MW in a rolling window (ERCOT 10 MW in 5 s). Frequency-domain limits per band in MW or percent (IESO, and the quoted LIPA values).
- **None of the documents writes the ramp limit in 5- or 15-minute dispatch intervals.** Those intervals appear only as the window over which utilities compare scheduled and actual power.
- **Ramp limits are justified by regulation reserve, not by the largest contingency.** CAISO cites regulation reserve and the primary-response deadband, IESO cites depletion of the AGC fleet, NERC cites reserves held to regulate frequency.
- **Contingency size justifies ride-through and recovery time instead.** EirGrid's case is the clearest: one interconnector fault plus consequential load loss.
- **Second-scale and frequency-domain limits are justified by generator shaft torsional stress and inter-area oscillation.**
- **Limits are stated in absolute MW, not as a share of site capacity.** The only percentage form found is ERCOT's 2023 proposal, which is also the only one with different up and down rates.
- **Smaller or weaker systems ask for faster recovery**: 500 ms in Ireland and Australia, 1 s in Ontario, 2 s in Texas, 3 s in California.
- **Transmission owners with voltage-driven concerns give no MW/min number** and review a site-specific ramp schedule against flicker limits.

Two inconsistencies between secondary sources, left unresolved: the CAISO document lists "ERCOT: 20 MW/min" as industry practice, while the survey in arXiv:2601.12686 says ERCOT defines no explicit step or ramp limit.

No numeric requirement was found for China, the United Kingdom, Singapore, PJM, MISO or NYISO. That is a gap in this search, not evidence that none exists.

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
| [Qinghai green compute–power dispatch center (青海绿色算电调度中心)](https://www.chinanews.com.cn/cj/2026/05-20/10625413.shtml) | Qinghai Province | 2024 | Demonstration | Monitors 17,000 servers in real time. Adjustable capacity not stated | P |
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
| [PJM board decision on integrating large loads](https://insidelines.pjm.com/pjm-board-outlines-plans-to-integrate-large-loads-reliably/) | PJM | 2026 | Operator program | 2026-01-16: new large loads may bring their own new generation or accept a "connect and manage" framework with earlier curtailment | P |
| [Software Carbon Intensity, ISO/IEC 21031:2024](https://greensoftware.foundation/articles/sci-specification-achieves-iso-standard-status/) | Green Software Foundation | 2024 | Standard | Method for computing the carbon intensity of software; excludes offsets | P |

### Observations

- The flexible-load trials that publish numbers are small: 256 GPUs in Phoenix, 23 MW in Shanghai. Google's agreements do not disclose MW.
- China's published activity is mostly on the supply side: direct green-power supply and co-located generation at gigawatt scale. Only one load-side result with a measured number was found.
- Outside China the published activity is mostly bilateral agreements between a company and a utility, and operator rules that trade flexibility for faster connection.

---

## Patents

Grouped by what is claimed. Year is the earliest priority found, or the filing year where marked "(filed)". All rows in this section are **R**: number, title and assignee were checked against USPTO Patent Public Search.

Not repeated here because they are already in [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling#patents): US11966273B2, US12562573B2, US20260118930A1, US20250338456A1, US20260141222A1 and eight others on power smoothing and capping.

### Grid- and carbon-aware workload scheduling

- **[US11644804B2](https://patents.google.com/patent/US11644804B2)** — Compute load shaping using virtual capacity and preferential location real time scheduling. Google, 2019, granted. Sets hourly "virtual capacity" limits per cluster from load forecasts and power models, moving deferrable tasks in time or location.
- **[US9886316B2](https://patents.google.com/patent/US9886316B2)** — Data center system that accommodates episodic computation. Microsoft, 2010, granted. Moves data and computation between data centers as renewable and grid supply vary.
- **[US9063738B2](https://patents.google.com/patent/US9063738B2)** — Dynamically placing computing jobs. Microsoft, 2010, granted. Places jobs across data centers by electricity cost.
- **[US10928845B2](https://patents.google.com/patent/US10928845B2)** — Scheduling a computational task for performance by a server computing device in a data center. Microsoft, 2010, granted. Schedules tasks from a forecast of renewable generation.
- **[US12136001B2](https://patents.google.com/patent/US12136001B2)** — Distributed computing with variable energy source availability. Microsoft, 2021, granted.
- **[US12086650B2](https://patents.google.com/patent/US12086650B2)** — Workload placement based on carbon emissions. Pure Storage, 2021 (filed), granted.
- **[US20250060996A1](https://patents.google.com/patent/US20250060996A1)** — Dynamic load scheduling using carbon intensity decomposition. IBM, 2023 (filed), application.

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

### Observations

- In the United States the filers are cloud and chip companies. Microsoft's filings span the longest period, from renewable-following scheduling in 2010 to AI training power smoothing in 2023–2024.
- Lancium holds a dense family around behind-the-meter flexible data centers.
- No patent was found on coordinating grid-fault ride-through with the computing workload. This reflects a limited search.
- Chinese filings titled with 算电协同 cluster in 2024–2026; see the next section for why they are not in the tables above.

---

## Open-source software and data

All rows are **R**: repository existence, license and description were read from the GitHub API on the "last updated" date.

Not repeated here because they are already in [awesome-aidc-modeling](https://github.com/Yuz2023/awesome-aidc-modeling#tools--simulators): Zeus, Vessim and the OpenG2G paper.

### Grid-signal-aware scheduling

- **[Green-Software-Foundation/carbon-aware-sdk](https://github.com/Green-Software-Foundation/carbon-aware-sdk)** — MIT. API and command-line tool that returns the best time and region to run a workload from carbon-intensity data.
- **[Azure/carbon-aware-keda-operator](https://github.com/Azure/carbon-aware-keda-operator)** — MIT. Kubernetes operator that caps autoscaling when carbon intensity is high.
- **[bluehands/Carbon-Aware-Computing](https://github.com/bluehands/Carbon-Aware-Computing)** — MIT. Schedules tasks at the forecast point of lowest grid carbon intensity.
- **[thegreenwebfoundation/grid-intensity-go](https://github.com/thegreenwebfoundation/grid-intensity-go)** — Apache-2.0. Go library and exporter for factoring carbon intensity into where and when to run jobs.
- **[sustainable-computing-io/peaks](https://github.com/sustainable-computing-io/peaks)** — Apache-2.0. Power-efficiency-aware Kubernetes scheduler.
- **[kube-green/kube-green](https://github.com/kube-green/kube-green)** — MIT. Kubernetes operator that shuts down workloads on a schedule.

### Power measurement and control on the compute side

- **[sustainable-computing-io/kepler](https://github.com/sustainable-computing-io/kepler)** — Apache-2.0. Prometheus exporter for per-workload energy on Kubernetes.
- **[hubblo-org/scaphandre](https://github.com/hubblo-org/scaphandre)** — Apache-2.0. Host and process-level energy metrology agent.
- **[geopm/geopm](https://github.com/geopm/geopm)** — BSD-3-Clause. Global Extensible Open Power Manager: job-level power management for HPC systems.
- **[llnl/variorum](https://github.com/llnl/variorum)** — MIT. Vendor-neutral library exposing power caps and power telemetry across architectures.
- **[flux-framework/flux-power-monitor](https://github.com/flux-framework/flux-power-monitor)** — LGPL-3.0. Power monitoring and management modules for the Flux resource manager.

### Coupled compute–grid simulation

- **[gpu2grid/openg2g](https://github.com/gpu2grid/openg2g)** — Apache-2.0. Simulation library for AI data-center and distribution-grid interaction: trace-replay or live-GPU data-center backend, OpenDSS grid model, and controllers such as batch-size control for voltage regulation.
- **[ExaDigiT/RAPS](https://github.com/ExaDigiT/RAPS)** — Apache-2.0. Replays or models supercomputer workloads and predicts the resulting facility power.
- **[atlarge-research/opendc](https://github.com/atlarge-research/opendc)** — MIT. Data-center simulator with power and energy models.
- **[HewlettPackard/dc-rl](https://github.com/HewlettPackard/dc-rl)** — MIT. SustainDC: multi-agent reinforcement-learning environments for workload shifting, cooling and battery control.
- **[facebookresearch/CarbonExplorer](https://github.com/facebookresearch/CarbonExplorer)** — Evaluates combinations of renewables, storage and load shifting for running data centers on renewable energy.
- **[microsoft/vidur](https://github.com/microsoft/vidur)** — MIT. Large-scale simulator for LLM inference systems; **[ozcanmiraay/vidur-energy](https://github.com/ozcanmiraay/vidur-energy)** (MIT) adds energy and carbon accounting.

### Grid data feeds

- **[electricitymaps/electricitymaps-contrib](https://github.com/electricitymaps/electricitymaps-contrib)** — AGPL-3.0. Parsers behind the Electricity Maps carbon-intensity data.
- **[gridstatus/gridstatus](https://github.com/gridstatus/gridstatus)** — BSD-3-Clause. Uniform Python access to data from US system operators.

### Cluster traces with job-to-machine records

Useful for studying how jobs map onto machines, and from there onto power domains.

- **[google/cluster-data](https://github.com/google/cluster-data)** — Borg cluster traces, including a power-data release.
- **[alibaba/clusterdata](https://github.com/alibaba/clusterdata)** — Production cluster traces, including GPU cluster releases.
- **[Azure/AzurePublicDataset](https://github.com/Azure/AzurePublicDataset)** — CC-BY-4.0. Azure VM, function and LLM inference traces.
- **[msr-fiddle/philly-traces](https://github.com/msr-fiddle/philly-traces)** — CC-BY-4.0. Deep-learning training job traces from a Microsoft cluster.

---

## Leads not yet verified

Seen only in search results or search-index records. The source pages could not be opened when this list was compiled. Listed so that others can check them; **do not cite from here**.

**Chinese patents.** Number, title and applicant come from search-index records; the patent pages were not opened.
- CN120691373B 一种算电协同系统及方法 — 湖北邮电规划设计有限公司
- CN120672091B 一种数据中心算力与电力协同调度的信息交互方法及系统 — 中国科学院大学
- CN121055283A 基于新能源消纳的算力任务调度方法、装置和存储介质 — 清华大学
- CN117374933A 基于计算负载时空转移的数据中心需求响应优化调度方法 — 东南大学
- CN121979665A 一种基于虚拟电厂的电算协同一体化管理方法及系统 — 国网新疆电力有限公司信息通信公司
- CN120073810B 基于飞轮储能系统的算力负荷平抑和节能管理系统 — 微控飞轮（沈阳）技术开发有限公司
- CN121364938A 一种基于算电协同的智算中心资源管控方法、系统及设备 — 中国联通
- CN121710173A 算电协同调控方法、装置、设备、可读存储介质和程序产品 — 中国电信
- CN118860630A 一种算力调度方法、装置、设备、存储介质及程序产品 — 中国移动研究院
- CN120434159A 一种算力网络资源调度方法 — 国家电网信息通信分公司
- CN116862126A 一种能源网络与算力网络融合下的算力分配方法与装置 — 国家电投集团科学技术研究院
- CN119809034A 算力电力耦合下绿色数据中心调度优化方法 — 华北电力大学
- CN121689043A 基于可靠性与经济性的算电协同电网规划方法及系统 — 国网上海市电力公司

**Projects and programs.**
- UK trial of AI data-center grid flexibility — National Grid, Emerald AI, EPRI, Nebius, NVIDIA (2025)
- ERCOT Large Flexible Load Task Force and controllable load resource registration
- EirGrid data-centre connection offer policy and flexible-demand arrangements
- Grid-interactive UPS providing fast frequency response in Dublin — Microsoft, Eaton, Enel X (2022)
- Battery storage at the xAI Colossus site, Memphis
- Lancium Clean Campus and Soluna Project Dorothy, Texas (curtailment-following compute)
- Hohhot Horinger data-center cluster green-energy supply demonstration (和林格尔)
- Compute–power coordination pilot tasks of China's National Data Administration (2024)
- 《算电协同技术白皮书》 and the draft group standard 《绿色数据中心算电协同调控系统技术要求》

**Grid requirements.**
- NERC Level 3 Essential Action Alert on computational loads (2026-05) and the Reliability Guideline on risk mitigation for emerging large loads (2026-05): original documents not opened
- ENTSO-E position on national connection requirements for data centres (2025-12)
- Original utility documents behind the secondary quotations for Southern Company, ATC, LIPA / PSEG Long Island, AESO and SPP

---

## Contributing

Corrections matter more than additions. If you can open a source that is marked **S** or listed under leads, please open an issue or pull request with the link and the exact sentence.

For new entries: one row or line per entry, a link to the primary source, the number and unit exactly as the source writes them, and the verification mark. Papers belong in the related lists above.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the maintainer has waived all copyright and related rights to this list.
