---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

Education
======
* **Ph.D. in Astrophysics**, National Astronomical Observatories, Chinese Academy of Sciences, Beijing, China, 2022 – present
  * Advisor: Prof. Jie Wang
  * Research focus: HI 21 cm surveys, numerical simulations
* **B.S. in Astronomy / Physics**, Tsinghua University, Beijing, China, 2018 – 2022

Research Experience
======
* **2023 – present: HI intensity mapping cross-correlation with DESI galaxies**
  * Computational Cosmological Group, National Astronomical Observatories, CAS
  * First-author project; paper in preparation, results not yet public
  * Cross-correlating FAST HI intensity mapping with DESI DR1 galaxy spectroscopy in the HD2 deep field, to constrain the cosmic HI abundance and its halo-model decomposition.
  * Built the analysis end to end: HiFAST pipeline reduction, foreground subtraction, and the construction of inverse-variance-weighted HI and galaxy fields.
  * Validating the measurement with a suite of null tests, together with a full systematic error budget.

* **2025 – present: Cosmic evolution of the HI density parameter in IllustrisTNG**
  * Computational Cosmological Group, National Astronomical Observatories, CAS
  * First-author project; paper in preparation, results not yet public
  * Tracing neutral hydrogen across cosmic time in IllustrisTNG-100 with the Krumholz (2013) partitioning model, deriving the HI density parameter and its dependence on cosmic-web environment.
  * Mapping where the HI lives across the cosmic web, and assessing what the environmental distribution implies for 21 cm stacking measurements.

* **2020 – 2022: Machine-learning detection of exoplanets via gravitational microlensing**
  * Department of Astronomy, Tsinghua University
  * Undergraduate research project; introduced to the field by Shude Mao and directly supervised by Wei Zhu.
  * Applied machine-learning methods to gravitational microlensing light curves to search for planetary signals in survey photometry.

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% if post.category == 'manuscripts' %}
    {% include archive-single-cv.html %}
    {% endif %}
  {% endfor %}</ul>

In preparation &amp; submitted
======
  <ul>{% for post in site.publications reversed %}
    {% if post.category == 'preprints' %}
    {% include archive-single-cv.html %}
    {% endif %}
  {% endfor %}</ul>

Conference Presentations
======
  <ul>{% for post in site.talks reversed %}
    {% include archive-single-talk-cv.html  %}
  {% endfor %}</ul>

Awards & Honors
======
* **2017 — Gold Medal, National Finals, Chinese Physics Olympiad (CPhO)**, Chinese Physical Society
  * Selected for the national training team; admitted to the Department of Physics, Tsinghua University, by recommendation, exempt from the national entrance examination.

Computing & Technical Skills
======
* **Programming:** Python (NumPy, SciPy, Astropy, Matplotlib); C/C++; Git; Linux / HPC
* **Cosmology & inference:** CAMB; FFT power-spectrum estimation; MCMC with emcee; halo-model decomposition (colossus); FKP weighting
* **Radio data reduction:** FAST; HiFAST calibration & imaging pipeline; AOFlagger RFI flagging; standing-wave removal
* **Foregrounds & systematics:** Gaussian Process Regression subtraction; null-test design; systematic error budgeting
* **Simulations & surveys:** IllustrisTNG-100 / AREPO; subgrid HI partitioning (Krumholz 2013); 21 cm stacking; DESI DR1
* **Writing & typesetting:** LaTeX; Matplotlib; corner
* **Languages:** Chinese (native); English (fluent)

References
======
* **Jie Wang** — Researcher; Group Leader, Computational Cosmology Group, National Astronomical Observatories, CAS. Ph.D. advisor. [jie.wang@nao.cas.cn](mailto:jie.wang@nao.cas.cn)
* **Wei Zhu** — Associate Professor, Department of Astronomy, Tsinghua University. BSc research supervisor. [weizhu@mail.tsinghua.edu.cn](mailto:weizhu@mail.tsinghua.edu.cn)
* **Yingjie Jing** — FAST Fellow, Computational Cosmology Group, National Astronomical Observatories, CAS. Co-author on all five publications above; HiFAST pipeline lead. [jyj@nao.cas.cn](mailto:jyj@nao.cas.cn)
* **Shude Mao** — Chair Professor of Astronomy, Westlake University. BSc research mentor. [shude.mao@westlake.edu.cn](mailto:shude.mao@westlake.edu.cn)
* **Qi Guo** — Researcher, Computational Cosmology Group, National Astronomical Observatories, CAS. Co-author, HiFAST pipeline & FAST HD² Survey. [guoqi@nao.cas.cn](mailto:guoqi@nao.cas.cn)
* **Liang Gao** — Professor, Beijing Normal University. Co-author, HiFAST pipeline & FAST HD² Survey. [lgao@bnu.edu.cn](mailto:lgao@bnu.edu.cn)
