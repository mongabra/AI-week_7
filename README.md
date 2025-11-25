#  ⚖️ Ethical AI & Algorithmic Fairness Audit: COMPAS Recidivism Case Study

This repository contains the deliverables for the [AI for software engineering] assignment, covering the theoretical foundation, case study analysis, practical algorithmic audit, and ethical reflection related to AI fairness.

---

## 👥 Group Members
1. [George Omondi Alando-Group Leader]
2. [Maureen Gathoni]
3. [Francis Promise]
4. [Bill Clinton Onyango]
5. [Erick Midida]
6. [Abraham Sitori]

---

## ✅ Part 1: Theoretical Understanding (Completed)

This section provides definitions and explanations for core concepts in ethical AI.

### 1. Short Answer Questions

| Question | Summary of Answer |
| :--- | :--- |
| **Q1: Algorithmic Bias** | **Algorithmic bias** is the systematic and repeatable error in a computer system's output that creates unfair outcomes, such as favoring one group over another. **Examples** include: 1) A facial recognition system misidentifying non-white faces at higher rates due to **underrepresentation** in the training data, and 2) A credit scoring algorithm denying loans based on zip code, which acts as a **proxy** for protected attributes (e.g., race, socioeconomic status). |
| **Q2: Transparency vs. Explainability** | **Transparency** refers to the openness of the overall AI process (knowing what data was used and the model's architecture), while **Explainability** refers to the ability to detail *why* a specific decision was made for an individual instance. Both are critical: Transparency allows external **auditing** for fairness, and Explainability provides users with the **right to contest** a decision. |
| **Q3: GDPR Impact** | The **General Data Protection Regulation (GDPR)** directly impacts AI by enforcing strict rules on data handling. Key provisions include the **Right to Explanation** (Article 22), which gives individuals the right to contest decisions made solely by automated processing, necessitating high levels of AI transparency and explainability in the EU. |

### 2. Ethical Principles Matching

| Principle | Definition |
| :--- | :--- |
| **B) Non-maleficence** | Ensuring AI does not harm individuals or society. |
| **C) Autonomy** | Respecting users’ right to control their data and decisions. |
| **D) Sustainability** | Designing AI to be environmentally friendly. |
| **A) Justice** | Fair distribution of AI benefits and risks. |

---

## ✅ Part 2: Case Study Analysis (Completed)

This section details the analysis of two key scenarios involving algorithmic fairness failures.

### Case 1: Biased Hiring Tool (Amazon)

| Task | Analysis |
| :--- | :--- |
| **Source of Bias** | **Training Data Bias.** The historical data used to train the system (resumes submitted over 10 years) overwhelmingly favored male candidates, leading the model to penalize resumes containing words associated with women (e.g., "women's chess club captain"). |
| **Proposed Fixes** | 1. **Data Rebalancing:** Over-sample female candidates or synthesize data to achieve parity. 2. **Blind Auditing:** Remove sensitive proxy features (gendered language, names, college affiliations) from the input data. 3. **Fairness-Aware Training:** Integrate a fairness constraint (e.g., Equal Opportunity Difference) into the loss function during model training. |
| **Metrics to Evaluate** | **Statistical Parity Difference (SPD)** and **Equal Opportunity Difference (EOD)**, ensuring the True Positive Rate (TPR) for both male and female candidates is equal. |

### Case 2: Facial Recognition in Policing

| Task | Discussion and Policies |
| :--- | :--- |
| **Ethical Risks** | **Wrongful Arrests:** Higher false positive rates for minorities lead to disproportionate scrutiny and wrongful arrests. **Chilling Effect:** Citizens may alter their behavior if they feel constant surveillance, infringing on **autonomy** and **privacy**. |
| **Recommended Policies** | 1. **Mandatory Bias Audits:** Require independent testing of the system for racial disparities in accuracy *before* deployment. 2. **Prohibition of Sole Reliance:** Policy stating that facial recognition evidence cannot be the *sole* basis for an arrest; corroborating evidence is always required. 3. **Transparency and Documentation:** Publicly document the system's accuracy rates, known limitations, and acceptable confidence thresholds. |

---

## ✅ Part 3: Practical Audit (COMPAS Dataset) (Completed)

This section details the audit of the COMPAS dataset for racial bias using the IBM AI Fairness 360 (AIF360) toolkit.

| Task | Status | Details |
| :--- | :--- | :--- |
| **Data Preparation** | Complete | Data filtered (ProPublica criteria), manually one-hot encoded, standardized, and converted to AIF360 `BinaryLabelDataset`. |
| **Bias Analysis Goal** | **Equalized Odds / False Positive Rate Disparity.** The audit focused on the difference in the False Positive Rate (FPR) between the unprivileged (African-American) and privileged (Caucasian) groups. |
| **Mitigation Applied** | **Reweighing (Pre-processing).** The training data sample weights were adjusted to reduce the correlation between the protected attribute and the prediction label. |
| **Visualization** | Complete | A bar chart was generated illustrating the quantified difference in FPR between the groups in the baseline model. |
| **300-word Report** | Complete | A formal report summarizing the quantitative findings, mitigation steps, and outcome metrics is provided in the final deliverable. |

---

## ✅ Part 4: Ethical Reflection (Completed)

### 1. Project Goal

To develop an AI-powered recommendation system that connects users with local events, volunteer opportunities, and essential community resources (e.g., social services, training programs) based on user interests and location.

**Ethical Risk Profile:** High risk of **algorithmic bias** (excluding certain communities from beneficial resources) and **privacy infringement** (handling sensitive location and service data).

---

### 2. Core Ethical Principles and Adherence

We commit to designing this system in adherence to the following key ethical principles:

#### 2.1. Fairness and Non-Discrimination ⚖️

We must prevent the system from reinforcing societal inequalities based on protected attributes or their proxies (like zip code).

| Principle | Actionable Implementation |
| :--- | :--- |
| **Bias Mitigation** | Employ pre-processing techniques (e.g., **Reweighing**) or in-processing techniques to ensure model performance metrics are consistent across different socioeconomic (proxy) and age groups. |
| **Data Equity** | Actively source events and services from **low-income and diverse community organizations** to ensure representational fairness in the data. |
| **Auditing** | Implement regular **disparity audits** (using metrics like Disparate Impact and Equal Opportunity Difference) to quantitatively verify the system is not systematically excluding unprivileged groups from favorable recommendations. |

#### 2.2. Transparency and Explainability 🗣️

Users must understand the rationale behind recommendations.

| Principle | Actionable Implementation |
| :--- | :--- |
| **Recommendation Justification** | Provide a simple, clear explanation for every output (e.g., "Recommended because you showed interest in 'Cooking' and this event is within 5 miles"). |
| **Model Documentation** | Maintain clear, public documentation detailing the features used, data sources, and model architecture to ensure **auditability**. |
| **Explainability Tools** | Utilize highly interpretable models, or if a complex model is necessary, integrate **post-hoc explanation tools** (like SHAP values) to show feature influence. |

#### 2.3. Privacy and Data Governance 🛡️

We must treat sensitive user and location data with the utmost care.

| Principle | Actionable Implementation |
| :--- | :--- |
| **Data Minimization** | Collect only the minimum data necessary for core functionality (e.g., using zip codes instead of precise coordinates where possible). |
| **Security & Consent** | Ensure all user data is **encrypted both in transit and at rest**. Implement clear, granular **opt-in consent** allowing users to control specific data usage. |
| **Retention Policy** | Establish a strict policy for data deletion, automatically removing interaction logs and non-essential identifiers after a defined period (e.g., 90 days). |

#### 2.4. Accountability and Safety ✅

The system must be safe to use and have clear oversight.

| Principle | Actionable Implementation |
| :--- | :--- |
| **Feedback Loop** | Implement an easily accessible **"Report this Recommendation"** mechanism to allow users to flag unsafe content, errors, or biased outputs for continuous model refinement. |
| **Human Oversight** | Flag critical recommendations, particularly those involving social services, for **manual review** if the model's prediction confidence is below a certain threshold. |