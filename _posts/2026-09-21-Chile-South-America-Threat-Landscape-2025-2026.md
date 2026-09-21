---
layout: default
title: "Chile / South America Threat Landscape 2025–2026"
lang: en
---

## Executive Summary

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/1.png' | relative_url }}"
    alt="Image 1"
    loading="lazy"
  >
  <figcaption><a href="https://www.infobae.com/tecno/2025/12/11/latinoamerica-fue-la-region-con-mas-ciberataques-en-2025-estos-fueron-los-cinco-paises-mas-afectados/" target="_blank" rel="noopener noreferrer">https://www.infobae.com/tecno/2025/12/11/latinoamerica-fue-la-region-con-mas-ciberataques-en-2025-estos-fueron-los-cinco-paises-mas-afectados/</a></figcaption>
</figure>

Between 2025 and 2026, ransomware in South America did not decline structurally; it changed form. 2025 was marked by disruptions, the shutdown of established brands, and unprecedented fragmentation across the Ransomware-as-a-Service ecosystem. Affiliates, however, did not disappear with those brands. They redistributed, migrated to more stable operations, or launched new leak sites. Qilin was one of the main beneficiaries of that process. In 2026, the market partially reconcentrated around operators capable of providing infrastructure, negotiation, tooling, and reputation, even as the total number of active groups continued to grow. [S01][S02][S03][S04][S05]

For South America, the most consistent finding remains that Brazil accounts for the largest observable volume of ransomware activity and financially motivated cybercrime, followed at some distance by Argentina and Colombia. Chile does not have the highest absolute number of publicly identified victims, but 2026 shows a clear increase in local visibility: a higher density of claims, different actors targeting Chilean organizations, incidents confirmed by affected entities, leaks corroborated by third parties, and a national reporting system that is bringing into view activity that previously remained outside the public record. [S01][S06][S11][S16]

The central thesis of this report is that a ransomware incident begins before the ransomware. Across the region, credentials stolen by infostealers—as repeatedly seen in cases involving ENTEL in Chile and Telefónica—along with phishing, identity compromise, VPN access, exposed appliances, Initial Access Brokers, and legitimate remote administration tooling form an access economy. That economy supplies affiliates capable of turning a valid account or an edge vulnerability into control over Active Directory, backups, virtualization, data, and critical services. Microsoft observed 5,606 Chilean devices affected by Lumma Stealer between March and May 2025—and that figure covers Lumma alone, while many other stealers operate in the ecosystem. CrowdStrike recovered more than one billion credentials associated with LATAM users and organizations from stealer logs and data leaks, and in 2026 ANCI reported unauthorized access involving valid credentials likely obtained through previous leaks or infostealers. [S09][S10][S13]

For management, the implication is direct: risk should not be modeled as the “probability that Qilin.exe appears,” but as a loss of business capability when an identity compromise reaches the control planes. For a SOC, Red Team, or Threat Intelligence function, the unit of analysis is the full chain: initial access → identity → privileges → discovery → lateral movement → defense degradation → exfiltration → backup/virtualization → extortion and/or encryption. In sectors with little tolerance for downtime—manufacturing, mining, food production, logistics, healthcare, government, and financial services—that chain can cause operational impact long before a ransom note appears.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/2.png' | relative_url }}"
    alt="Image 2"
    loading="lazy"
  >
  <figcaption><a href="https://www.infostealers.com/article/telefonica-breach-infostealer-malware-opens-door-for-social-engineering-tactics/" target="_blank" rel="noopener noreferrer">https://www.infostealers.com/article/telefonica-breach-infostealer-malware-opens-door-for-social-engineering-tactics/</a></figcaption>
</figure>

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/3.png' | relative_url }}"
    alt="Image 3"
    loading="lazy"
  >
  <figcaption><a href="https://www.24horas.cl/actualidad/nacional/pdi-investiga-posible-espionaje-a-entel-movistar-telmex-hackeo" target="_blank" rel="noopener noreferrer">https://www.24horas.cl/actualidad/nacional/pdi-investiga-posible-espionaje-a-entel-movistar-telmex-hackeo</a></figcaption>
</figure>

### Key Facts and Judgments

| **Judgment** | **Confidence** | **Basis** |
| --- | --- | --- |
| Ransomware pressure on South America will remain elevated over the next 6–12 months. | High | Historically high global volume, resilience of the affiliate model, and continued activity by Qilin, The Gentlemen, Akira, LockBit 5.0, and other operators. |
| 2025 was a year of fragmentation; 2026 combines reconcentration around strong brands with growth in the number of active groups. | High | Q3 2025 reached 85 active groups; Q1 2026 fell to 71, with the top ten accounting for 71%; Q2 returned to 93 groups. |
| Brazil will remain South America's main hub by volume and diversity of cybercrime. | High | It leads regional ransomware datasets and also concentrates financial fraud, banking malware, and domestic criminal infrastructure. |
| Chile faces greater observable pressure in 2026 than in 2025, although that does not make it the most targeted country in South America. | High | Higher density of listings, public incidents, corroborated leaks, and stronger reporting institutions. |
| Qilin is particularly relevant to Chile, but The Gentlemen and other actors make it impossible to reduce the risk to a single brand. | High | Qilin appears repeatedly in 2026; The Gentlemen has targeted several Chilean organizations since February and is growing globally. |
| Identity and remote access will remain the highest-return preventive surface. | High | Public incidents, infostealers, valid accounts, VPN access, edge exploitation, and the tradecraft of leading RaaS operations all converge on this surface. |
| Infostealers and leaked credentials will continue to supply corporate access. | High | Telemetry from Microsoft, CrowdStrike, and ANCI converges on the role of valid credentials and stealer logs. |
| AD, backups, vCenter/ESXi, and other control planes will continue to concentrate impact. | High | Qilin, Akira, and other actors demonstrate sustained targeting of virtualization, backups, and privileged administration. |
| EDR evasion through BYOVD and EDR killers will continue to become normalized. | Medium-High | ESET documents more than 100 EDR killers in use; Qilin and other groups integrate these capabilities. |
| AI will reduce the cost and time required for criminal development and operations, but it will not replace human affiliates in the near term. | Medium-High | The Gentlemen used coding assistants to accelerate development of its panel; available evidence points to augmentation rather than broad autonomy. |

> **EXECUTIVE TAKEAWAY**  
> **Ransomware is not an isolated “malware category.” It is a monetization model built on the same attack surface that enables fraud, credential theft, espionage, exfiltration, and third-party abuse. If identity, remote access, Active Directory, backup, and virtualization controls are weak, changing EDR products or buying another tool does not address the underlying risk.**

## 1. Methodology: What Does “Victim” Really Mean?

The first challenge in any threat landscape is methodological. A Data Leak Site is not a forensic database, and a tracker is not a CSIRT. Criminal actors publish victims as leverage, trackers aggregate those posts, vendors combine proprietary sources with DLS data, and affected organizations may confirm the incident, deny it, or simply remain silent—as most do in Chile and Latin America. If these categories are mixed, the analysis can produce apparently precise figures that actually compare different things.

From my operational experience in CTI, there is also an inverse error: treating every claim as noise until a corporate statement exists. That position does not reflect how intelligence works either. **A significant share of listings from mature operations ultimately corresponds to real compromises, even when the victim provides no details or confirms only “a cybersecurity incident.” At the same time, duplicates, partial access, recycled material, false attribution, and groups that inflate their reputation all exist. The analytical value lies precisely in distinguishing among those states.**

| **Status** | **Operational definition** | **What it supports** |
| --- | --- | --- |
| CONFIRMED | The affected organization, an authority, a CSIRT/CERT, direct forensic evidence, or several robust independent sources confirm the incident. | The incident occurred; attribution to the actor may still carry a separate confidence level. |
| CORROBORATED | A claim is accompanied by consistent independent evidence: visible disruption, data samples, published documents, related communications, or investigative reporting that inspected the material. | Real evidence exists beyond the claim; this does not necessarily confirm encryption, the initial vector, or the full scope. |
| CLAIMED | The actor publishes the organization on its DLS, or a tracker reproduces the listing. | The actor made the assertion; by itself, this does not prove access, encryption, data volume, or impact. |
| DISPUTED / FALSE POSITIVE | Reasonable evidence indicates duplication, recycled material, mistaken identification, nonexistent access, or a denial supported by evidence. | The listing should not be counted as a victim without qualification, or it may be excluded from the dataset. |

The second dimension is confidence. A case may carry high confidence that a listing exists and medium confidence that an intrusion occurred. It may carry high confidence that a leak occurred and low confidence that systems were encrypted. In this document, “high confidence” means that primary sources or multiple consistent independent sources exist; “medium” means that the evidence is strong but incomplete; and “low” is reserved for claims or secondary information without sufficient corroboration.

Incompatible metrics are also kept separate. Recorded Future reports publicly known victims named on ransomware blogs; Check Point measures DLS postings; ESET combines public sources such as ransomware.live with its own telemetry; Kaspersky reports attempts blocked on endpoints; and Microsoft reports devices affected by specific families. None of these metrics should be added together as if they all represented “attacks.” A detection is not a victim, a victim listed on a DLS is not confirmed encryption, and a confirmed incident does not necessarily include public attribution.

## 2. 2025: Fragmentation, Disruption, and Affiliate Redistribution

2025 is the starting point because it explains the composition of the 2026 market. Disruptions against major brands did not eliminate the ecosystem; they changed its distribution. RansomHub ceased operations in April 2025, and other prominent brands reduced or stopped posting. In Q2, Check Point observed the disappearance or inactivity of RansomHub, BianLian, 8Base, Cactus, Hunters International, and other operations. The result was not a structural decline in offensive capacity, but a market with more mid-sized actors and “orphaned” affiliates looking for new infrastructure. [S02]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/4.webp' | relative_url }}"
    alt="Image 4"
    loading="lazy"
  >
  <figcaption><a href="https://thehackernews.com/2025/04/ransomhub-went-dark-april-1-affiliates.html" target="_blank" rel="noopener noreferrer">https://thehackernews.com/2025/04/ransomhub-went-dark-april-1-affiliates.html</a></figcaption>
</figure>

Qilin capitalized on that vacuum. Check Point estimated that it grew from approximately 35 monthly victims in Q1 2025 to nearly 70 in Q2. In Q3, the number of active groups reached 85—the highest observed at that point—and the top ten accounted for only 56% of postings. Qilin averaged approximately 75 victims per month and became the period's leading RaaS hub. [S02][S03]

The most important point is not that one brand replaced another. It is affiliate mobility. RaaS infrastructure—panels, encryptors, negotiation, leak sites, and support—can disappear, while the actors who obtain access, steal credentials, deploy tools, and move laterally retain their experience, relationships, and inventory of access. Law-enforcement pressure against administrators and infrastructure creates friction and cost, but it does not automatically remove intrusion operators from the market.

Recorded Future documented 452 ransomware incidents/victims in Latin America and the Caribbean during 2025, slightly more than 6% of the global total of 7,346 observed postings. The five countries with the highest regional volume were Brazil (128), Mexico (78), Argentina (63), Colombia (51), and Peru (27). When the scope is limited to South America, Brazil was clearly the largest observable market, followed by Argentina, Colombia, and Peru. [S01]

| **Country / region** | **2025 public metric** | **Assessment** |
| --- | --- | --- |
| Brazil | 128 postings in Recorded Future (130 in its risk assessment) | Highest regional volume; also concentrates banking malware, fraud, and local criminal ecosystems. |
| Argentina | 63 | Second-largest South American market in the 2025 dataset, with exposure across financial, government, and corporate targets. |
| Colombia | 51 | High volume and growing interest in financial services, government, and service providers. |
| Peru | 27 | Lower volume than Brazil, Argentina, and Colombia, but persistent activity and corporate exposure. |
| Chile | Not in Recorded Future's regional top five | Lower absolute volume in that dataset; absence from the ranking does not imply low exposure or no incidents. |
| LAC total | 452 of 7,346 globally | Slightly more than 6% of global postings in 2025. |

The most affected sectors in LAC during 2025 were manufacturing (49), healthcare (36), government (28), information technology (21), and education (20). Qilin had the highest number of regional attacks/postings in Recorded Future's dataset, with 54, followed by LockBit (29), SafePay (27), The Gentlemen (22), and Kazu (21). [S01]

> **ANALYTICAL JUDGMENT**  
> **2025 was not the year ransomware “weakened.” It was the year criminal infrastructure became more fungible. A brand can disappear while the affiliate, stolen credential, sold access, and operational knowledge survive.**

## 3. 2026: Partial Consolidation at Historically High Scale

Q1 2026 showed the opposite movement. Check Point monitored more than 70 leak sites and recorded 2,122 newly published victims. The top ten groups again accounted for 71% of listings, and Qilin led for a third consecutive quarter with 338. The Gentlemen climbed to 166 from 40 in Q4 2025, while LockBit 5.0 reached 163. The fragmentation of 2025 had produced too many small brands; the market began to reconcentrate around operators capable of attracting affiliates and maintaining reliable infrastructure. [S04]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/5.avif' | relative_url }}"
    alt="Image 5"
    loading="lazy"
  >
  <figcaption><a href="https://www.zerofox.com/intelligence/flash-report-qilin-claims-record-number-of-monthly-attacks-for-2026/" target="_blank" rel="noopener noreferrer">https://www.zerofox.com/intelligence/flash-report-qilin-claims-record-number-of-monthly-attacks-for-2026/</a></figcaption>
</figure>

Q2 2026 introduced an apparent contradiction that actually describes the ecosystem well: volume remained stable at 2,139 postings, while the number of active groups rose to 93. Qilin retained the quarterly lead with 279, while The Gentlemen reached 269 and surpassed it during June. Ransomware is reconcentrating by volume while simultaneously fragmenting by brand count: dominant hubs coexist with a long tail of short-lived groups. [S05]

Using ransomware.live data, ESET counted 4,699 records during H1 2026, 16.5% more than in H1 2025. Qilin (722), The Gentlemen (nearly 550), and Akira (more than 300) accounted for 33.5% of the total, while DragonForce approached 300. In Latin America, Brazil exceeded 100 victims during H1, Argentina reached 39, and Colombia 33; Mexico, used here only as a LAC comparator, approached 80. ESET also reported that Qilin was the family with the most detections in Chile, peaking at 19 in January. [S06]

It is worth pausing on the word “confirmed” used in some reports. When the source dataset is ransomware.live, the record confirms that the victim was published or collected by the tracker, not necessarily that the organization issued a statement or that forensic evidence of encryption exists. This landscape preserves that distinction to avoid turning DLS volume into a census of intrusions.

| **Dimension** | **2025** | **2026 through September** | **Assessment** |
| --- | --- | --- | --- |
| RaaS structure | Record fragmentation, 85 active groups in Q3 | Q1 reconcentration, renewed expansion to 93 groups in Q2 | Dominant hubs plus a long tail of small brands. |
| Leading actor | Qilin grows after RansomHub's collapse | Qilin remains first; The Gentlemen closes the gap and leads in June | Competition for affiliates and access stockpiles. |
| Extortion | Greater emphasis on data theft and pressure tactics | Data theft, regulatory pressure, and selective encryption become normalized | “Ransomware” describes only part of the operation. |
| Defensive controls | Growing use of BYOVD/EDR killing | More numerous and specialized EDR killers | The defensive sensor is itself a target. |
| Virtualization/backup | ESXi and Veeam already relevant | Control planes and recovery remain central to impact | Service concentration increases blast radius. |
| Chile | Sustained activity but lower public volume | Higher density of claims, incidents, and corroborated leaks | Observable pressure is rising; reporting is also improving. |

## 4. Chile: Why 2026 Feels Different

Chile did not suddenly become South America's leader by absolute victim count. The available evidence does not support that conclusion. What changed is the combination of visible volume, actor diversity, the criticality of some affected organizations, and institutional maturity in reporting. In other words, 2026 feels different because there is more observable activity and because a larger share of that activity is leaving public traces.

ANCI ended 2025 with 3,258 institutions registered on its reporting portal and more than 400 incident reports. In the first stage, 915 Operators of Vital Importance were designated; in July 2026, the second stage raised the total to 1,154 OIVs. This changes the observability environment: incidents that could once remain confined to the organization, a provider, or an insurer now carry more explicit reporting, coordination, and continuity obligations. [S11][S12]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/6.png' | relative_url }}"
    alt="Image 6"
    loading="lazy"
  >
  <figcaption><a href="https://www.diariooficial.interior.gob.cl/publicaciones/2026/07/24/44507/01/2842835.pdf" target="_blank" rel="noopener noreferrer">https://www.diariooficial.interior.gob.cl/publicaciones/2026/07/24/44507/01/2842835.pdf</a></figcaption>
</figure>

At an AmCham seminar held in 2026, data attributed to ANCI indicated that 161 of the 410 reports received in 2025 involved incidents with significant impact, and that more than 60% of those serious cases began with stolen passwords or exposed vulnerabilities. The same presentation stated that Qilin may have been behind three of five incidents that cost the State nearly CLP 850 million in recovery during 2025. Because this is an aggregate attribution shared by a third party rather than a set of public incident reports identifying the organizations and artifacts involved, this document treats it as a risk signal, not as a basis for naming three institutions. [S27]

The methodological implication is important: growth in visible incidents in Chile during 2026 may simultaneously reflect more adversarial activity, broader leak-site coverage, better tracking by the CTI community, and stronger institutional capacity to detect and report. Rather than selecting a single explanation, the analysis should preserve all four.

## 5. Chilean Threat Landscape 2025–2026: A Selected Timeline

As of the cutoff date, ransomware.live/ransomwatch maintains dozens of historical records associated with Chile and shows a particularly visible concentration during 2026. The tracker's raw count should not be interpreted as confirmed incidents: it includes claims, cases covered by the press, possible duplicates, and historical records. Its value lies in observing actors, sequence, and sectors. [S16]

| **Date** | **Entity / event** | **Actor / status** | **CTI assessment** |
| --- | --- | --- | --- |
| Jan. 2025 | Garces Fruit | Akira – claimed | Agro-export sector; continued ransomware interest in production and food. |
| Feb.–Jun. 2025 | Emin, CMSG, Megacentro, Emotrans, University of Chile, Petroquim | Akira, RansomHub, Hunters, NightSpire, Lynx – claimed | Diversity of actors and sectors; there is no single “Chile ransomware.” |
| Sep.–Dec. 2025 | Nubox/SumaSaaS, Liceo Francés, OfficePro, Pangea, Clínica Dávila | AlphaLocker, The Gentlemen, Qilin, Devman – mix of claims | The Gentlemen was already present in 2025, Qilin gained visibility, and Devman exposed healthcare risk. |
| Jan. 28, 2026 | Unidentified strategic OIV/PSE entity | Qilin – reported/attributed | Alert AIC26-00002: brute force against WatchGuard, with inadequate MFA/lockout controls. [S14] |
| Jan.–Feb. 2026 | Valbifrut, INDH, Pucobre, Ducasse, Conectados, Graneles, ISESA, and others | Qilin / The Gentlemen / INC / LockBit – mostly claimed | Early-year cluster spanning agriculture, government, mining, commerce, and technology. |
| Mar.–Apr. 2026 | NOI Hotels, Corporación Colina, SAAM Towage, Frutícola Olmué | Qilin / The Gentlemen – claims; SAAM leak corroborated by press | Greater visibility across hospitality, local government/public sector, transportation, and production. |
| Jun. 2026 | Clínica Maitenes | Incident confirmed by the clinic; separate Qilin claim | A backup system was affected; the organization notified ANCI and maintained continuity. [S15] |
| Jul.–Aug. 2026 | Las Cenizas, CONTAC, AGUNSA, ESPAC, Layher, Difor, Incolur | The Gentlemen / Qilin – claimed | Production, mining, transportation, construction, and technology sectors. |
| Aug. 30, 2026 | Hospital Clínico Universidad de Chile | DireWolf – claimed | Potentially high-impact healthcare claim, without sufficient independent confirmation as of the cutoff date. [S28] |
| Sep. 2–4, 2026 | Tanner | Qilin – claim plus leak corroborated by press | Qilin lists Tanner; Interferencia accesses leaked internal files and describes specific content. [S17] |
| Sep. 7, 2026 | S&A Chile | The Gentlemen – claimed | IT provider/integrator: a reminder of the potential blast radius concentrated in third parties and MSPs. |

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/7.png' | relative_url }}"
    alt="Image 7"
    loading="lazy"
  >
  <figcaption><a href="https://socradar.io/free-tools/ransomware-intelligence/countries/chile" target="_blank" rel="noopener noreferrer">https://socradar.io/free-tools/ransomware-intelligence/countries/chile</a></figcaption>
</figure>

## 6. Tanner: When a Claim Stops Being Just a Claim

Tanner is a particularly useful case for explaining why a binary “confirmed/unconfirmed” taxonomy can fall short. Qilin listed the Chilean financial institution in early September 2026. At that point, the verifiable fact was the listing: a known ransomware/extortion actor claimed to have compromised Tanner. Some trackers, appropriately, continued to classify it as an unverified claim. Today, anyone with basic CTI knowledge and sufficient curiosity can locate the documents leaked in this case. [S16]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/8.png' | relative_url }}"
    alt="Image 8"
    loading="lazy"
  >
  <figcaption><a href="https://www.ransomware.live/id/VGFubmVyQHFpbGlu" target="_blank" rel="noopener noreferrer">https://www.ransomware.live/id/VGFubmVyQHFpbGlu</a></figcaption>
</figure>

On September 17, Interferencia published an investigation based on internal files leaked by Qilin to which the outlet had gained access. The report describes collection files, title searches, corporate records, certificates of title and encumbrances, internal legal documentation, and folders tied to specific clients and transactions. The outlet did more than repeat the leak-site claim: it inspected the material, described documents, and checked portions of their content against public records and court filings. [S17]

That changes the analytical status. Following that publication, the existence of an internal information leak no longer depends solely on the actor's word. For this landscape, Tanner moves to **CORROBORATED** for compromise/exfiltration/publication of information, with high confidence that Qilin conducted the extortion and published the data. What remains publicly unproven is the access vector, whether production systems were encrypted, dwell time, the exact scope of the intrusion, the extortion amount, and the recovery process. Saying only “it is unconfirmed” would be too passive; saying “we know exactly how the ransomware incident occurred” would be excessive. Useful CTI operates between those extremes.

> **WHY TANNER MATTERS**  
> **The case demonstrates that a DLS is the beginning of the assessment, not the end. A claim can evolve into corroboration when real data, operational evidence, or independent investigation emerges. The discipline lies in updating the confidence level without filling in technical gaps that remain unknown.**

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/9.png' | relative_url }}"
    alt="Image 9"
    loading="lazy"
  >
  <figcaption><a href="https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup" target="_blank" rel="noopener noreferrer">https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup</a></figcaption>
</figure>

From a management perspective, the impact is not limited to “stolen files.” A financial institution holds legal, credit, asset, and relationship data that can enable fraud, social engineering, secondary extortion, and targeted campaigns against clients or third parties. Publishing internal documents turns a technical incident into reputational, privacy, regulatory, and business risk. Exfiltrated data takes on a second life once it leaves the perimeter: it can be searched, resold, correlated, and reused by other actors.

From a technical perspective, Tanner also requires us to avoid a convenient inference: that every Qilin case in Chile necessarily followed the same vector observed in the OIV/PSE incident or in global investigations. The ransomware brand does not identify the affiliate or prove that the same vulnerability was reused. Until logs, artifacts, a ransom note, EDR telemetry, or a technical disclosure become available, initial access must remain an intelligence gap.

## 7. Other Chilean Cases That Help Explain the Risk

### 7.1 OIV/PSE Entity: Remote Access, Authentication, and a National Alert

Alert AIC26-00002, publicly reproduced from Chile's National CSIRT, described an incident with significant impact at a strategic OIV/PSE entity in late January—many readers will already know which organization is involved—and identified Qilin early in the response. Access reportedly began with brute-force attempts against a WatchGuard firewall in an environment without MFA or adequate lockout and geographic restriction mechanisms. [S14]

The most useful detail is not the firewall brand. It is the risk class: an exposed remote service, insufficient authentication, and a subsequent path to internal assets. Changing vendors without addressing MFA, lifecycle management, lockout, risk-based authentication, management-plane exposure, and segmentation preserves the same logical attack surface.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/10.png' | relative_url }}"
    alt="Image 10"
    loading="lazy"
  >
  <figcaption><a href="https://x.com/ANCIChile/status/2016609735160496194" target="_blank" rel="noopener noreferrer">https://x.com/ANCIChile/status/2016609735160496194</a></figcaption>
</figure>

### 7.2 Clínica Maitenes: Confirmed Incident, Separate Attribution

On June 13, 2026, Clínica Maitenes publicly confirmed that it had detected a cybersecurity incident affecting one of its backup systems, activated containment, notified ANCI, and opened an internal investigation. The clinic stated that patient care was not interrupted. Separately, Qilin had listed the organization on June 2. [S15]

There are two solid facts here and one relationship that must be handled carefully: the incident is confirmed, the Qilin listing is confirmed, and the clinic's statement does not publicly attribute the incident to Qilin. It is a clear example of why the “existence of an incident” must be separated from “attribution.” It is also a reminder that backup is not merely a recovery measure; it is a direct target and a privileged plane within an attack.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/11.png' | relative_url }}"
    alt="Image 11"
    loading="lazy"
  >
  <figcaption><a href="https://www.ransomware.live/id/Q2xpbmljYSBNYWl0ZW5lc0BxaWxpbg" target="_blank" rel="noopener noreferrer">https://www.ransomware.live/id/Q2xpbmljYSBNYWl0ZW5lc0BxaWxpbg</a></figcaption>
</figure>

### 7.3 SAAM Towage: Transportation, Contracts, and Operational Sensitivity

SAAM Towage was listed by Qilin in April, and the Chilean press later reported gaining access to thousands of leaked private documents, including contracts, payroll records, compensation data, and operational protocols. Although technical disclosure of the incident remains limited, the case again demonstrates the importance of separating a claim, corroboration of leaked data, and forensic detail. [S29]

In transportation and logistics, stolen information has value beyond privacy. Contracts, protocols, suppliers, routes, and business relationships can become useful intelligence for fraud, social engineering, reputational pressure, or follow-on attacks. For an extortion actor, the value of the dataset is part of the weapon.

## 8. The Actors Defining 2026

### 8.1 Qilin: The Affiliate Hub That Survived Fragmentation

Qilin should not be understood as a homogeneous group that conducts exactly the same intrusion every time. MITRE tracks it as ransomware/RaaS with Go and Rust variants for Windows, Linux, and VMware ESXi, and separately identifies Water Galura / GOLD FEATHER as the service operator. Affiliates may determine how to obtain access, which tooling to use, and how long to remain in the environment. [S24]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/12.jpg' | relative_url }}"
    alt="Image 12"
    loading="lazy"
  >
  <figcaption><a href="https://es.vectra.ai/modern-attack/threat-actors/qilin" target="_blank" rel="noopener noreferrer">https://es.vectra.ai/modern-attack/threat-actors/qilin</a></figcaption>
</figure>

Its regional importance is explained by three factors: scale, its ability to absorb displaced affiliates, and the breadth of impact it can produce. Qilin appears across manufacturing, finance, healthcare, logistics, and technology organizations, and it has sustained activity even when specific components of its ecosystem have been disrupted. In Chile, its recurrence during 2026—Valbifrut, Ducasse, Conectados, Graneles, NOI, SAAM, Maitenes, AGUNSA, Difor, Tanner, and other listings—makes it a standing intelligence requirement, although each case must be validated individually.

Technically, the defensive value lies in its recurring operational objectives: valid accounts and remote access, Active Directory, credentials, remote administration, exfiltration, EDR degradation, backups, and virtualization. MITRE documents PowerShell, GPOs, scheduled tasks, Mimikatz/token manipulation, host discovery, SMB/SSH, service stopping, recovery inhibition, and ESXi. An encryptor signature is late-stage evidence. [S24]

### 8.2 The Gentlemen: From Experienced Affiliate to Major Actor

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/13.webp' | relative_url }}"
    alt="Image 13"
    loading="lazy"
  >
  <figcaption><a href="https://healthexec.com/topics/health-it/cybersecurity/gentlemen-ransomware-gang-takes-over-hospital-facebook-after-cyberattack" target="_blank" rel="noopener noreferrer">https://healthexec.com/topics/health-it/cybersecurity/gentlemen-ransomware-gang-takes-over-hospital-facebook-after-cyberattack</a></figcaption>
</figure>

The Gentlemen went from no postings in August 2025 to 166 victims in Q1 2026 and 269 in Q2. Check Point links its origins to a former Qilin affiliate and an inventory of previously compromised access. An internal leak from the group itself exposed a core of approximately nine operators, several affiliates, and access procedures involving Fortinet/Cisco vulnerabilities, NTLM relay, and OWA/M365. [S04][S05][S25]

The leak also showed the use of coding assistants to build part of its ransomware administration panel in approximately three days. This is more relevant than narratives about “autonomous ransomware”: primary evidence shows AI reducing development time and enabling experienced actors to produce tooling faster. Humans still select victims, access paths, and objectives; AI compresses implementation cost.

In Chile, The Gentlemen appears in records associated with INDH, Corporación Colina, Las Cenizas, CONTAC, ESPAC, Layher, Incolur, and S&A Chile, among others. Not all are corroborated. The relevant signal is that the country is already part of the group's geographic distribution and that the operation is interested in government, mining, technology, construction, and integrators.

### 8.3 Akira: Operational Consistency and Pressure on Industry

Akira remains one of the highest-volume operations, particularly in manufacturing and industrial services. Dragos ranked it among the most active actors targeting industrial organizations in Q1 and Q2 2026. Its publicly documented patterns include abuse of VPNs—including the pattern seen in Chile in late 2023—and legacy accounts, credential theft, exfiltration through legitimate services, and destruction of backups before encryption. [S07][S08]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/14.jpg' | relative_url }}"
    alt="Image 14"
    loading="lazy"
  >
  <figcaption><a href="https://www.trellix.com/blogs/research/akira-ransomware/" target="_blank" rel="noopener noreferrer">https://www.trellix.com/blogs/research/akira-ransomware/</a></figcaption>
</figure>

Akira matters to South America because the model does not require a “regional” campaign. The same combination of VPN access, legacy accounts, virtualization, file servers, and intense pressure from downtime exists in agribusiness, manufacturing, mining, logistics, and services. Chile already had Akira listings in 2025, and its access model remains applicable even if another actor dominates locally in 2026.

### 8.4 LockBit 5.0, DragonForce, and the Long Tail

LockBit 5.0 returned in 2025 and reached 163 postings in Q1 2026. DragonForce, meanwhile, seeks to operate as infrastructure—a cartel—for other operators and has promoted stolen-data analysis services intended to improve extortion. The correct assessment is not that these brands will necessarily dominate Chile, but that the barrier to entry for affiliates continues to fall: they can choose among multiple platforms, reuse tooling, and migrate when a program collapses. [S03][S04][S06]

## 9. South America Does Not Have a Single Threat Landscape

### 9.1 Brazil: Scale, Banking Malware, and Specialized Financial Crime

Brazil is the leading South American market in virtually every comparable dataset. Recorded Future documented 128 ransomware postings in 2025, and ESET observed more than 100 victims during H1 2026. But ransomware is only part of the picture. Brazil has a mature ecosystem of banking malware, payment fraud, mobile trojans, and groups developing tooling adapted to Pix, boletos, banking software, and local user behavior. [S01][S06]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/15.png' | relative_url }}"
    alt="Image 15"
    loading="lazy"
  >
  <figcaption><a href="https://www.zscaler.com/blogs/security-research/clickfix-campaign-generated-ai-delivers-smartrat" target="_blank" rel="noopener noreferrer">https://www.zscaler.com/blogs/security-research/clickfix-campaign-generated-ai-delivers-smartrat</a></figcaption>
</figure>

In September 2026, Google Threat Intelligence Group/Mandiant published its analysis of BREEZE COMET, a financially motivated actor that has compromised Brazilian financial services, retail, and e-commerce organizations since 2024 to manipulate payment systems and banking software. This type of operation is a reminder that “more ransomware” does not automatically mean “more financial risk”: in banking, transactional fraud and account takeover may be more direct threats. [S18]

During 2026, Brazil's CTIR published specific recommendations on ClickFix, phishing campaigns, vulnerability exploitation, identity compromise, and abuse of .gov.br subdomains to distribute information-stealing and remote-control malware. This access chain aligns directly with the ransomware model: credential → session → privilege → lateral movement → monetization. [S19][S20]

### 9.2 Argentina: High Regional Exposure and High-Value Targets

Argentina ranked second among South American countries in Recorded Future's 2025 dataset, with 63 postings, and ESET counted 39 victims in H1 2026. Its digital economy, financial sector, healthcare, government, and service companies keep it within the regional target surface. Recorded Future also observed FamousSparrow/TAG-141 targeting entities in Mexico, Argentina, and Chile, illustrating that Argentina shares the region's exposure to both financially motivated crime and espionage activity. [S01][S06]

Qilin's July 2026 listing of the Argentine Army should be treated as a claim unless sufficient additional public evidence emerges. Even so, the inclusion of state and military organizations on RaaS leak sites demonstrates that traditional boundaries between “criminal targets” and “strategically relevant targets” are not always reflected in affiliate target selection.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/16.png' | relative_url }}"
    alt="Image 16"
    loading="lazy"
  >
  <figcaption><a href="https://www.dexpose.io/qilin-ransomware-group-targets-ejercito-argentino/" target="_blank" rel="noopener noreferrer">https://www.dexpose.io/qilin-ransomware-group-targets-ejercito-argentino/</a></figcaption>
</figure>

### 9.3 Colombia: Ransomware With Confirmed Government Impact

Colombia recorded 51 postings in 2025 and 33 in H1 2026 across the regional sources reviewed. Unlike many listings, Colombia's Ministry of Justice confirmed on August 3, 2026, that part of its technology infrastructure had been compromised by ransomware, affecting service availability. COLCERT secured evidence and logs and began forensic analysis, while the Ministry activated alternative channels; weeks later, some systems remained temporarily unavailable. [S21][S30]

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/17.png' | relative_url }}"
    alt="Image 17"
    loading="lazy"
  >
  <figcaption><a href="https://www.vanguardia.com/colombia/2026/08/03/atencion-ministerio-de-justicia-confirma-ataque-cibernetico-con-ransomware/" target="_blank" rel="noopener noreferrer">https://www.vanguardia.com/colombia/2026/08/03/atencion-ministerio-de-justicia-confirma-ataque-cibernetico-con-ransomware/</a></figcaption>
</figure>

The management significance of this case lies in recovery time: a ransomware incident can become a suspension of deadlines, alternative service channels, administrative contingency, and a need to coordinate with national and international teams. Real impact is measured in the ability to deliver services, not in the number of encrypted endpoints.

### 9.4 Peru, Ecuador, Bolivia, Paraguay, and Uruguay: Less Granularity Does Not Mean Less Risk

Recorded Future documented 27 postings in Peru during 2025. Numerous listings exist in trackers for 2026, but no equivalent H1 source applies the same methodology across every South American country. Ecuador appeared in Qilin-related financial cases during 2025 and retains significant exposure to fraud and malware; Bolivia, Paraguay, and Uruguay show lower volumes and uneven reporting. [S01]

The absence of a comparable figure is an intelligence gap, not evidence of lower activity. In smaller markets, a single incident affecting a telecommunications operator, government body, healthcare provider, or energy company can have a national consequence disproportionate to its statistical volume.

## 10. The Sector Landscape: Where the Same Technique Produces Different Consequences

Victimology should not be used only to ask “which sector appears most often.” Sector risk emerges at the intersection of exposure, technological dependence, and operational consequence. The same attack produces different outcomes in a factory, a bank, a hospital, or a ministry.

| **Sector** | **Recurring surface** | **Primary consequence** | **2025–2026 assessment** |
| --- | --- | --- | --- |
| Banking / financial services | Identity, OWA/M365, VPN, VDI, APIs, privileged endpoints, third parties | Fraud, data leakage, unavailability, secondary abuse of data | Ransomware competes with financial fraud and account takeover; Tanner demonstrates the extortion value of internal data. |
| Government / essential services | Legacy remote access, AD, providers, portals, citizen data | Service disruption, public crisis, data exposure, reporting obligations | ANCI, INDH claims, the Chilean OIV/PSE case, and Colombia's Ministry of Justice raise the priority. |
| Manufacturing / production | VPN, remote plants, ERP, AD, VMware, file servers, IT/OT dependencies | Production downtime, logistics disruption, and loss of traceability | Most affected sector in LAC in 2025; manufacturing represented 65% of Dragos's Q2 2026 industrial dataset. |
| Mining / energy | Contractors, remote access, IT/OT bridges, engineering systems, virtualization | Operational disruption and indirect physical safety risk | High consequence even without touching a PLC; Las Cenizas/Pucobre illustrate visible interest in Chile. |
| Healthcare | AD, clinical systems, backups, PII/PHI, providers | Care availability, privacy, clinical continuity | Clínica Maitenes and Hospital Clínico claims; healthcare remains under pressure globally. |
| Transportation / logistics | ERP/EDI, ports, vendor access, VMware, providers | Supply-chain paralysis, contract exposure, operational disruption | SAAM/AGUNSA and Dragos trends reflect pressure on continuity. |
| Technology / MSP | RMM, tenants, privileged credentials, multi-client tooling | Cross-customer blast radius and downstream compromise | S&A Chile and CONTAC appear in listings; risk stems from multi-tenant authority. |
| Education | Broad identity populations, heterogeneous endpoints, legacy systems, research | Academic disruption and data leakage | Universities appear repeatedly in regional trackers. |

### 10.1 Productive Sectors: An Attacker Does Not Need to Compromise a PLC to Stop a Plant

Manufacturing was the sector with the most victims in LAC during 2025 in Recorded Future's dataset. Across Dragos's industrial universe, Q1 2026 recorded 1,020 incidents/postings and Q2 recorded 1,140; manufacturing accounted for 633 and 747 respectively, approximately 62–65% of the total. Qilin, Akira, and The Gentlemen were among the highest-volume actors. [S01][S07][S08]

The implication for Chile is clear. A salmon producer, mining company, food processor, logistics company, or manufacturer can be halted without an attacker executing a single instruction on a PLC. If ERP, Active Directory, file servers, virtualization, quality systems, planning, dispatch, or traceability become unavailable, operations may still degrade. The IT/OT boundary does not eliminate the operational dependence between both environments.

### 10.2 Banking and Finance: Ransomware Is a Threat, but Not the Only Path to Monetization

The financial sector concentrates sensitive data and payment capacity, but an adversary in South America does not need encryption to monetize access. BREEZE COMET in Brazil, Grandoreiro, Mispadu, Astaroth, Coyote, and other families demonstrate an ecosystem focused on credentials, sessions, and transactional fraud. Recorded Future documents continued banking-trojan activity in 2025 and the evolution of variants during 2026. [S01][S18]

Tanner adds another dimension: internal legal and financial information can be used as extortion leverage even when the public has no evidence of encryption. At a bank or financial institution, confidentiality loss can be as monetizable as availability loss.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/18.png' | relative_url }}"
    alt="Image 18"
    loading="lazy"
  >
  <figcaption><a href="https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil" target="_blank" rel="noopener noreferrer">https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil</a></figcaption>
</figure>

### 10.3 Government: Impact Is Measured in Public Service

The Colombian Ministry of Justice case and Chile's OIV/PSE incident demonstrate that ransomware in government cannot be evaluated using the same criteria as a corporate endpoint. Suspended procedures, alternative channels, administrative deadlines, public communications, and national coordination are all part of the impact. Technology recovery becomes an institutional continuity problem.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/19.png' | relative_url }}"
    alt="Image 19"
    loading="lazy"
  >
  <figcaption><a href="https://therecord.media/china-hackers-latin-america-espionage" target="_blank" rel="noopener noreferrer">https://therecord.media/china-hackers-latin-america-espionage</a></figcaption>
</figure>

### 10.4 Healthcare: Availability and Confidentiality Intersect

Healthcare ranked among the region's most targeted sectors in 2025 and remains on the lists of major actors. A hospital may maintain clinical care during an incident, as Clínica Maitenes reported, but compromise of backups, laboratory systems, identity, or medical records can create cumulative impact and privacy risk. The priority is not only to “prevent encryption,” but to preserve the ability to operate safely.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/20.png' | relative_url }}"
    alt="Image 20"
    loading="lazy"
  >
  <figcaption><a href="https://thehackernews.com/2026/07/china-nexus-jadeprox-uses-new-triback.html" target="_blank" rel="noopener noreferrer">https://thehackernews.com/2026/07/china-nexus-jadeprox-uses-new-triback.html</a></figcaption>
</figure>

## 11. Before Ransomware: The Access Economy

The thread connecting nearly the entire landscape is the access economy. Microsoft considers credential theft one of Latin America's primary concerns. Between March 16 and May 16, 2025, it recorded 21,137 Brazilian devices affected by Lumma Stealer, 10,486 in Argentina, 8,303 in Colombia, 6,618 in Peru, and 5,606 in Chile. [S09]

In 2024, CrowdStrike observed 107 access brokers advertising access to 428 LATAM entities and recovered more than one billion regional credentials associated with data leaks and stealer logs. The average price of initial access fell 60% compared with 2023. The economic interpretation is straightforward: when the supply of credentials and access increases, a ransomware affiliate does not need to develop every stage from scratch. It can buy or reuse an entry point that someone else already obtained. [S10]

ANCI added local evidence in May 2026. While investigating leaks, it reported no evidence of direct attacks against infrastructure in several cases, but did identify unauthorized access using valid credentials likely obtained from previous leaks or infostealer malware. [S13]

> **MONETIZATION CHAIN**  
> **Infostealer / phishing / leak → valid credential → broker or affiliate → VPN / IdP / OWA / remote access → Active Directory / cloud → exfiltration → backup / virtualization → extortion and/or encryption.**

This model explains why ransomware prevention cannot be isolated from the identity program. Incomplete MFA coverage, vendor accounts, persistent sessions, unmanaged devices, service accounts, browser credentials, and legacy access paths can become the first link in an incident whose ultimate impact appears days or weeks later under a ransomware brand.

## 12. From Access to Impact: The Recurring Technical Pattern

### 12.1 Initial Access: Identity, Edge Devices, and Social Engineering

The leading actors of 2025–2026 converge on a limited set of access classes: valid credentials, VPNs and remote services, vulnerable edge appliances, phishing/social engineering, access acquired from third parties, and RMM tools. What has changed is not the novelty of these techniques, but the speed at which they are operationalized and the availability of access stockpiles.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/21.webp' | relative_url }}"
    alt="Image 21"
    loading="lazy"
  >
  <figcaption><a href="https://cyberhoot.com/es/cybrary/initial-access-broker-iab/" target="_blank" rel="noopener noreferrer">https://cyberhoot.com/es/cybrary/initial-access-broker-iab/</a></figcaption>
</figure>

Brazil offers a useful indicator of change in social engineering. CTIR.Gov warned about ClickFix targeting .gov.br domains and campaigns combining phishing, vulnerability exploitation, identity compromise, and exfiltration. ESET observed that ClickFix detections more than doubled between H2 2025 and H1 2026, while quishing reached record levels in its telemetry. [S19][S20][S23]

### 12.2 Credential Access and Active Directory: Turning an Account Into Authority

A valid credential is valuable only if it can be converted into reach. In modern intrusions, the objective is to identify groups, privileged accounts, Domain Controllers, GPOs, administrative paths, backups, and virtualization systems. Qilin has been documented using Mimikatz/token manipulation, PowerShell, GPOs, and discovery; The Gentlemen uses credentials, relay attacks, and corporate services; Akira steals credentials before destroying backups. [S24][S25][S08]

The problem is not limited to Domain Admin. Tier 0 should be understood as the set of identities and assets whose compromise grants systemic control: Domain Controllers, GPO/SYSVOL, PKI, PAM, backup identities, vCenter, and privileged jump hosts. If they share administrative paths or reused credentials, the segmentation shown in a diagram may not exist operationally.

### 12.3 Discovery and Lateral Movement: LOLBins, Legitimate Administration, and Context

RDP, SMB/admin shares, PsExec, PowerShell, WMI, scanners, RMM, SSH, and commercial tools appear repeatedly because they already exist in corporate environments. The defensive opportunity does not lie in declaring a process malicious by name, but in observing who runs it, from which segment, after what authentication event, and against what volume of hosts.

An east-west RDP session from an authorized PAW during maintenance does not carry the same meaning as a burst of RDP/SMB activity from a workstation that has just authenticated through the VPN. Temporal correlation across identity, endpoint, and network telemetry remains stronger than detecting an isolated tool.

### 12.4 Defense Evasion: When EDR Becomes the Target

ESET reports more than 100 EDR killers observed in the wild, with new samples appearing regularly. Qilin has used BYOVD and specialized components to interfere with security tooling; other RaaS operations follow the same logic. The defensive control becomes an explicit target. [S23]

This changes an operational rule for the SOC: a coordinated loss of agent heartbeat should not be treated solely as a health issue. If it occurs after privileged activity, anomalous driver loading, service stopping, or remote administration, it may be an attack signal. The organization needs independent telemetry that survives endpoint impairment: firewalls, NDR, IdP, Windows Event Forwarding, SIEM, vCenter, Veeam, and appliances.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/22.jpg' | relative_url }}"
    alt="Image 22"
    loading="lazy"
  >
  <figcaption><a href="https://blog.talosintelligence.com/qilin-edr-killer/" target="_blank" rel="noopener noreferrer">https://blog.talosintelligence.com/qilin-edr-killer/</a></figcaption>
</figure>

### 12.5 Exfiltration First: Impact Can Exist Without Encryption

The shift from encryption-first operations toward data theft and pressure-first extortion consolidated during 2025 and continues in 2026. Exfiltration removes some of the operational complexity of encryption and creates regulatory, reputational, and commercial pressure. Qilin has even promoted assistance in identifying regulatory consequences to increase pressure on victims. [S02]

Tanner is a local manifestation of this model: once internal documents are published, harm no longer depends on whether a server was encrypted. The dataset can generate headlines, fraud, spearphishing, and exposure of business relationships. Availability and confidentiality are different levers within the same extortion business.

### 12.6 Backup, Veeam, vCenter, and ESXi: Attacking Recovery to Multiply Pressure

The most important step before encryption is often reducing the victim's ability to recover. Actors target VSS, backup repositories, Veeam, hypervisors, snapshots, and privileged credentials. Qilin supports ESXi and has been observed moving toward vCenter/ESXi; Akira maintains patterns of backup destruction and hypervisor access. [S24][S08]

Technology concentration amplifies risk. Dozens of services may depend on the same vCenter and backup platform. If AD, backup, and virtualization share the same trust plane, the actor can turn an identity compromise into widespread unavailability. The mature question is not “do we have backups?” but “can the same compromised administrator destroy the backups and shut down the VMs?”

## 13. The Malware Around Ransomware: Infostealers, Banking Trojans, Loaders, and RATs

If this regional analysis were limited to ransomware, it would miss half the problem. Infostealers supply credentials, loaders deliver payloads, RATs maintain access, banking trojans monetize accounts directly, and phishing or ClickFix campaigns create newly compromised devices that may end up in stealer logs or in the hands of brokers.

During 2025, Recorded Future observed significant activity involving Grandoreiro, Crocodilus, Mispadu, Astaroth, SORVEPOTEL, Casbaneiro, BBTok, Coyote, and other banking-malware families. Several campaigns rely on WhatsApp, PDF/LNK files, PowerShell, compromised cloud infrastructure, or mobile applications. The boundary between “banking malware” and “corporate initial access” may be defined more by the monetization objective than by technique. [S01]

Kaspersky recorded more than 1.1 million ransomware attempts in Latin America between August 2024 and June 2025. Chile ranked third with approximately 43,000 detections, behind Brazil and Mexico. That figure does not contradict Chile's lower DLS volume: it measures attempts blocked on endpoints, not victimized organizations. [S26]

The difference among these datasets is analytically useful. One country may have many malware detections and fewer leak-site postings; another may have less endpoint telemetry but high-impact corporate incidents. A threat landscape should preserve the units of measurement instead of forcing them into a single table.

## 14. Not Everything Is Cybercrime: APT Activity and Converging Tradecraft

Ransomware is primarily a criminal economy, but South American organizations are also targets of espionage, state-sponsored operations, and hybrid actors. CrowdStrike describes China-nexus adversaries as the most active state-sponsored actors in LATAM in its regional analysis. Recorded Future mentions FamousSparrow/TAG-141 using SparrowDoor against entities in Mexico, Argentina, and Chile, as well as Storm-2603 activity deploying different ransomware families against government, energy, agriculture, and telecommunications sectors across LAC/APAC. [S01][S10]

From a Detection Engineering perspective, the distinction between “sophisticated APT” and “criminal ransomware” is less useful than it appears. Both may exploit Exchange or VPNs, abuse valid accounts, use PowerShell, Cobalt Strike, or RMM, steal credentials, and exfiltrate to cloud services. Motivation remains fundamental to attribution and intelligence requirements, but many defensive signals are shared.

This reinforces an adversary-informed approach: design controls around attack functions—gain access, escalate, discover, move, persist, extract, and degrade recovery—not around a specific brand. The same MFA or segmentation control can disrupt a Qilin affiliate, a fraud operator, and an espionage cluster.

## 15. Detection Engineering: What Should Change in a South American Organization

The highest-return detection opportunities occur before T1486. Waiting for the encryptor means the actor probably already has credentials, discovery, access to high-value servers, and the ability to distribute tooling. The following detection families are more resilient to ransomware rebranding.

| **Detection** | **What to look for** | **Telemetry** | **Priority** |
| --- | --- | --- | --- |
| Remote access + identity | Distributed spraying, valid login from a new ASN/device/country, out-of-pattern vendor activity, legacy sessions | VPN / IdP / firewall / UEBA | P0 |
| Tier 0 / AD | GPO/SYSVOL changes, admin logon outside a PAW, LSASS/NTDS access, new admin accounts | DC audit / WEF / EDR / SIEM | P0 |
| Lateral movement | East-west RDP, ADMIN$/C$ fan-out, PsExec, remote service creation, unusual SSH | NDR / Windows / firewall / EDR | P0 |
| EDR impairment | Coordinated heartbeat loss, service stopping, driver loads, DLL side-loading, BYOVD indicators | EDR health / kernel telemetry / SIEM / NDR | P0 |
| Exfiltration | Exceptional uploads from file/DC/backup servers to cloud/file-sharing services, new sync tools | Proxy / NetFlow / NDR / CASB | P1 |
| Backup / vCenter | Task/snapshot deletion, new administrator, password changes, VM shutdown, repository tampering | Veeam / vCenter / hypervisor audit | P0 |
| RMM / tunnels | New installation/tenant, AnyDesk/ScreenConnect/Mesh/Ngrok outside the baseline | EDR / inventory / network | P1 |
| Credential economy | Corporate credentials in stealer logs, password reuse, compromised third-party identities | CTI / identity / exposure monitoring | P0 |

A detection should not live in isolation. A “valid VPN login” may be legitimate. A “valid VPN login + domain discovery + east-west RDP + GPO modification + EDR heartbeat loss” is an intrusion hypothesis. The value lies in temporal context and the relationship among identities, hosts, and control planes.

## 16. For CISOs and Management: From Declared Control to Operable Control

The 2025–2026 landscape reinforces an uncomfortable idea: having a control is not the same as having a capability. An organization may claim to have MFA while maintaining a vendor VPN without MFA; it may have EDR but fail to alert when twenty agents stop reporting; it may have backups while allowing the same domain credentials to administer Veeam; it may have segmentation while allowing SMB/RDP from VPN pools to critical servers.

| **Control** | **Validation question** | **Why it matters** |
| --- | --- | --- |
| MFA / remote access | Are all VPN, vendor, break-glass, and legacy paths covered and free of bypasses? | Remote access continues to appear as a recurring vector. |
| PAM / JIT | Can an identity obtained from an ordinary endpoint progress toward Tier 0? | Limits the conversion of a credential into authority. |
| Segmentation | Can a VPN/user VLAN reach DC, backup, or hypervisor management interfaces? | Limits the blast radius of the initial foothold. |
| EDR resilience | Do service stopping, driver manipulation, or telemetry loss trigger an independent response? | EDR is an active target. |
| Backup | Has full restoration been tested, and are identities separated? | The presence of backups does not equal tested recovery. |
| VMware / ESXi | Does vCenter have isolated access, MFA, logging, and separate accounts where feasible? | Controls the availability of many services simultaneously. |
| Third-party access | Do vendors use JIT, expiration, session recording, and minimum scope? | Third parties concentrate trust paths. |
| Incident reporting | Can the SOC, legal, and leadership teams escalate and report within real deadlines? | In Chile, detection and reporting are part of operational capability. |

For organizations subject to Law 21.663, an incident is no longer only an internal technical problem. The ability to detect, classify, escalate, and report becomes part of the security posture. An organization that discovers ransomware only at the point of encryption may already have lost critical hours or days for containment, evidence preservation, and regulatory communication.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/23.png' | relative_url }}"
    alt="Image 23"
    loading="lazy"
  >
  <figcaption><a href="https://innershell-labs.github.io/2026/07/22/A_Security_Control_Is_Not_Real_Until_It_Can_Be_Operated.html" target="_blank" rel="noopener noreferrer">https://innershell-labs.github.io/2026/07/22/A_Security_Control_Is_Not_Real_Until_It_Can_Be_Operated.html</a></figcaption>
</figure>

> **EXECUTIVE METRIC**  
> **Ransomware severity should be modeled as loss of business capability: Which service can no longer be delivered? For how long? What information left the environment? Which third parties are exposed? Which obligations are triggered? Counting encrypted endpoints is too narrow a metric for an enterprise resilience problem.**

## 17. Outlook for 2026–2027: What Is Reasonable to Expect

There is insufficient evidence to forecast a single campaign “against Chile” led by one actor. A different hypothesis is more consistent with the evidence: global affiliates seek replicable attack surfaces and find in South America the same combinations of remote access, credentials, vulnerable appliances, RMM, Active Directory, VMware, and low tolerance for downtime that they monetize in other markets.

1. Qilin and The Gentlemen will remain relevant, but brand leadership can change quickly. Affiliate mobility is more stable than the name of the RaaS operation.

1. The value of identity compromise will continue to grow. Infostealers, phishing, token theft, and access brokers reduce the cost of entry without requiring a sophisticated exploit.

1. Edge devices will remain a priority attack surface. The time between disclosure and exploitation will continue to shrink, and appliances with poor lifecycle management will remain attractive paths.

1. EDR killers, BYOVD, and defense evasion will become normalized as reusable components. Independent telemetry will matter more than another malware signature.

1. ESXi, vCenter, Veeam, and other recovery/control planes will remain under pressure because they convert privilege into concentrated impact.

1. Extortion will become increasingly independent of encryption. Publishing data, contacting customers, exploiting regulatory consequences, or applying reputational pressure may be sufficient.

1. AI will accelerate tooling, analysis of stolen data, phishing, and script adaptation. The immediate change will be attacker productivity, not full autonomy.

1. MSPs, integrators, and technology providers will become more valuable targets because of the cross-cutting authority and downstream access they concentrate.

1. Visibility in Chile will also continue to grow through institutional maturity: more OIVs, more reporting, and greater capacity to correlate incidents that previously remained isolated.

<figure class="post-image post-image-wide">
  <img
    src="{{ '/assets/img/24.jpg' | relative_url }}"
    alt="Image 24"
    loading="lazy"
  >
  <figcaption><a href="https://www.gartner.com/en/newsroom/press-releases/2026-06-02-gartner-identifies-four-critical-threats-requiring-urgent-improvements-from-cybersecurity-leaders" target="_blank" rel="noopener noreferrer">https://www.gartner.com/en/newsroom/press-releases/2026-06-02-gartner-identifies-four-critical-threats-requiring-urgent-improvements-from-cybersecurity-leaders</a></figcaption>
</figure>

## 18. Intelligence Gaps: What We Still Do Not Know

A serious synthesis must also end with its limitations. Chile's primary gap remains the lack of detailed technical incident disclosures. We have claims, brief and infrequent corporate communications, regulatory alerts, leaks, and investigative reporting, but rarely see complete timelines covering initial vector, dwell time, artifacts, infrastructure, exfiltration path, affiliate, bypassed controls, and root cause. As a result, we do not learn from domestic incidents in a way that allows that knowledge and the corresponding preventive measures to be shared.

- There is no public national denominator for VPNs without MFA, legacy appliances, or exposed vendor accounts.

- There is no unified public dataset that consistently distinguishes victim-confirmed, corroborated, claimed, and false-positive cases for Chile.

- Most Chilean Qilin cases do not identify which affiliate conducted the intrusion.

- The access vector remains publicly unknown for Tanner, SAAM Towage, AGUNSA, Difor, and multiple 2026 listings.

- Trackers use different dates—publication, discovery, estimated attack date, or backfill—and comparing them without normalization manufactures trends.

- Endpoint detections, DLS victims, incident reports, and financial losses are not interchangeable metrics.

- Third-party and MSP exposure in Chile still lacks comparable public measurement.

- The relationship between stealer-log exposure and regional ransomware victimization is plausible and operationally useful, but it should not be converted into individual causation without evidence.

The evidence required to raise confidence is well known: VPN/IdP logs, EDR process trees, Domain Controller auditing, SYSVOL/GPO history, Veeam/vCenter logs, NetFlow/proxy data for exfiltration, ransom notes, hashes, timestamps, and organizational communications. Until that evidence is available, hypotheses must remain labeled as hypotheses.

## 19. Conclusion: Ransomware Is the Visible Outcome of a Much Larger Access Market

The main difference between 2025 and 2026 is not the appearance of a new magical technique. It is that the criminal ecosystem became more efficient at reorganizing existing capabilities. In 2025, the collapse of major brands produced fragmentation; in 2026, operators such as Qilin and The Gentlemen demonstrated that affiliates, credentials, access, and operational knowledge can regroup quickly. The brand changes faster than the function.

South America reflects that dynamic with characteristics of its own. Brazil dominates by scale and by the depth of its financial-fraud ecosystem; Argentina and Colombia sustain significant volumes; Peru retains persistent exposure; and during 2026 Chile shows pressure that is far more visible and diverse than a view limited to the 2025 regional rankings would suggest.

The Tanner case captures the problem well. A listing began as a claim. Days later, multiple checks within the CTI community and an investigative report that accessed internal documents and described specific material elevated the case to a corroborated leak. What remains unknown—vector, encryption, dwell time, and recovery—must remain a gap. That combination of firmness and caution is more useful than the two usual extremes: believing everything a criminal publishes, or dismissing everything until the victim releases a postmortem that will probably never arrive.

For a CISO, the message is less attractive but more actionable: ransomware is not solved by buying “anti-ransomware.” Risk is reduced by preventing a compromised identity from becoming authority over Active Directory, backups, virtualization, data, and third parties. A SOC should not wait for the encryptor to detect the intrusion. For a Red Team, the objective is not to demonstrate that it can launch ransomware, but to validate which control should have interrupted the chain. For CTI, the work is not to accumulate IoCs; it is to connect actors, access, TTPs, sectors, evidence, and confidence levels to defensive decisions.

> **FINAL JUDGMENT**  
> **Chile does not need to wait for every claim to be publicly confirmed before acting, but it also does not need to inflate every listing into a proven breach. Mature intelligence operates in that space: enough evidence to make decisions before complete certainty exists, and enough discipline to know exactly which parts remain unknown.**

In 2026, knowing the names Qilin, The Gentlemen, or Akira is useful. Understanding the system that makes them possible is far more important.

## Key Sources and References

Sources were selected with priority given to official bodies, recognized threat intelligence teams, technical reports, and media outlets that provide direct corroboration. Leak-site trackers are used as claim telemetry, not as automatic confirmation of incidents.

**[S01] Recorded Future / Insikt Group – Cybercrime Landscape in Latin America and the Caribbean (2025).** [https://www.recordedfuture.com/research/latin-america-and-the-caribbean-cybercrime-landscape-es](https://www.recordedfuture.com/research/latin-america-and-the-caribbean-cybercrime-landscape-es)

**[S02] Check Point Research – The State of Ransomware Q2 2025.** [https://research.checkpoint.com/2025/the-state-of-ransomware-q2-2025/](https://research.checkpoint.com/2025/the-state-of-ransomware-q2-2025/)

**[S03] Check Point Research – The State of Ransomware Q3 2025.** [https://research.checkpoint.com/2025/the-state-of-ransomware-q3-2025/](https://research.checkpoint.com/2025/the-state-of-ransomware-q3-2025/)

**[S04] Check Point Research – The State of Ransomware Q1 2026.** [https://research.checkpoint.com/2026/the-state-of-ransomware-q1-2026/](https://research.checkpoint.com/2026/the-state-of-ransomware-q1-2026/)

**[S05] Check Point Research – The State of Ransomware Q2 2026.** [https://research.checkpoint.com/2026/the-state-of-ransomware-q2-2026/](https://research.checkpoint.com/2026/the-state-of-ransomware-q2-2026/)

**[S06] ESET / WeLiveSecurity – Ransomware in the First Half of 2026.** [https://www.welivesecurity.com/es/ransomware/primer-semestre-2026-ataques-sectores-mas-afectados/](https://www.welivesecurity.com/es/ransomware/primer-semestre-2026-ataques-sectores-mas-afectados/)

**[S07] Dragos – Industrial Ransomware Analysis Q1 2026.** [https://www.dragos.com/dragos-industrial-ransomware-analysis-q1-2026](https://www.dragos.com/dragos-industrial-ransomware-analysis-q1-2026)

**[S08] Dragos – Industrial Ransomware Analysis Q2 2026.** [https://www.dragos.com/blog/dragos-industrial-ransomware-analysis-q2-2026](https://www.dragos.com/blog/dragos-industrial-ransomware-analysis-q2-2026)

**[S09] Microsoft – Digital Defense Report 2025.** [https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/security/Microsoft-Digital-Defense-Report-2025.pdf](https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/security/Microsoft-Digital-Defense-Report-2025.pdf)

**[S10] CrowdStrike – 2025 LATAM Threat Landscape Report / Deep Dive.** [https://www.crowdstrike.com/en-us/blog/2025-latam-threat-landscape-report-deep-dive/](https://www.crowdstrike.com/en-us/blog/2025-latam-threat-landscape-report-deep-dive/)

**[S11] ANCI – First Annual Review 2025.** [https://anci.gob.cl/noticias/anci-primer-balance/](https://anci.gob.cl/noticias/anci-primer-balance/)

**[S12] ANCI – First Designation Process for Operators of Vital Importance, July 2026.** [https://anci.gob.cl/noticias/anci-finaliza-el-primer-proceso-de-calificacion-de-operadores-de-importancia-vital/](https://anci.gob.cl/noticias/anci-finaliza-el-primer-proceso-de-calificacion-de-operadores-de-importancia-vital/)

**[S13] ANCI – Update: Leaks Caused by Credential Theft, May 2026.** [https://anci.gob.cl/noticias/actualizacion-anci-filtraciones-por-robo-de-credenciales/](https://anci.gob.cl/noticias/actualizacion-anci-filtraciones-por-robo-de-credenciales/)

**[S14] Public reproduction of National CSIRT alert AIC26-00002 concerning Qilin / OIV-PSE.** [https://blog.nivel4.com/anci/csirt-nacional-alerta-sobre-incidente-de-efecto-significativo-en-entidad-estrategica-e-identifica-a-ransomware-qilin-como-autor](https://blog.nivel4.com/anci/csirt-nacional-alerta-sobre-incidente-de-efecto-significativo-en-entidad-estrategica-e-identifica-a-ransomware-qilin-como-autor)

**[S15] Clínica Maitenes – Information on the Cybersecurity Incident, June 13, 2026.** [https://clinicamaitenes.cl/comunicados/](https://clinicamaitenes.cl/comunicados/)

**[S16] Ransomware.live / Ransomwatch – Chile Map and Records.** [https://ransomwatch.mousqueton.io/map/CL](https://ransomwatch.mousqueton.io/map/CL)

**[S17] Interferencia – Tanner Hack Exposes Work Linked to Clients and Transactions, September 17, 2026.** [https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup](https://interferencia.cl/articulos/hackeo-tanner-expone-gestiones-vinculadas-antonio-jalaff-factop-francisco-frei-y-corpgroup)

**[S18] Google Threat Intelligence Group / Mandiant – BREEZE COMET Targets Brazil, September 2026.** [https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil](https://cloud.google.com/blog/topics/threat-intelligence/financially-motivated-threat-actor-breeze-comet-targets-brazil)

**[S19] CTIR.Gov Brazil – Recommendation 03/2026, ClickFix.** [https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-03-2026](https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-03-2026)

**[S20] CTIR.Gov Brazil – Recommendation 04/2026, Phishing, Vulnerabilities, and Identities.** [https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-04-2026](https://www.gov.br/gsi/pt-br/assuntos/ctir/recomendacoes/2026/recomendacao-04-2026)

**[S21] Colombian Ministry of Justice – Update on the Ransomware Attack, August 3, 2026.** [https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/Actualizacion-sobre-el-ataque-cibernetico.aspx](https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/Actualizacion-sobre-el-ataque-cibernetico.aspx)

**[S22] COLCERT – Intelligence Bulletins and Reports 2026.** [https://colcert.gov.co/800/w3-propertyvalue-412601.html](https://colcert.gov.co/800/w3-propertyvalue-412601.html)

**[S23] ESET Threat Report H1 2026.** [https://www.welivesecurity.com/en/eset-research/eset-threat-report-h1-2026/](https://www.welivesecurity.com/en/eset-research/eset-threat-report-h1-2026/)

**[S24] MITRE ATT&CK – Qilin / Agenda, S1242.** [https://attack.mitre.org/software/S1242/](https://attack.mitre.org/software/S1242/)

**[S25] Check Point Research – Internal Analysis of The Gentlemen (Reference and Threat Report).** [https://research.checkpoint.com/2026/18th-may-threat-intelligence-report/](https://research.checkpoint.com/2026/18th-may-threat-intelligence-report/)

**[S26] Kaspersky – Ransomware Attacks Exceed 1.1 Million Attempts in Latin America, October 2025.** [https://latam.kaspersky.com/about/press-releases/ataques-de-ransomware-superan-11-millones-de-intentos-en-america-latina](https://latam.kaspersky.com/about/press-releases/ataques-de-ransomware-superan-11-millones-de-intentos-en-america-latina)

**[S27] AmCham Chile – Seminar on ANCI and Implementation of the Cybersecurity Framework Law, 2026.** [https://amchamchile.cl/noticia/seminario-de-amcham-chile-reune-a-la-anci-y-a-la-industria-en-plena-implementacion-de-la-ley-marco-de-ciberseguridad/](https://amchamchile.cl/noticia/seminario-de-amcham-chile-reune-a-la-anci-y-a-la-industria-en-plena-implementacion-de-la-ley-marco-de-ciberseguridad/)

**[S28] GalaxyWarden – Hospital Clínico Universidad de Chile Listed by DireWolf, August 2026 (Claim Tracker).** [https://www.galaxywarden.com/blog/breach/hospital-clnico-universidad-de-chile-direwolf-2026-08](https://www.galaxywarden.com/blog/breach/hospital-clnico-universidad-de-chile-direwolf-2026-08)

**[S29] Interferencia – Leak of SAAM Towage Documents by Qilin, May 2026.** [https://interferencia.cl/secciones/empresas](https://interferencia.cl/secciones/empresas)

**[S30] Colombian Ministry of Justice – Technology Recovery Plan, August 2026.** [https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/MinJusticia-activa-plan-de-recuperacion-tecnologica-luego-de-vulneracion-cibernetica-garantizando-servicios-esenciales.aspx](https://www.minjusticia.gov.co/Sala-de-prensa/Paginas/MinJusticia-activa-plan-de-recuperacion-tecnologica-luego-de-vulneracion-cibernetica-garantizando-servicios-esenciales.aspx)
