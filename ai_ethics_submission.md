# Part 1: Theoretical Understanding (30%)

## 1. Short Answer Questions

**Q1: Define algorithmic bias and provide two examples of how it manifests in AI systems.**  
**Definition:** Algorithmic bias occurs when an AI system produces systematic and repeatable errors that create unfair outcomes, such as privileging one arbitrary group of users over others. This usually stems from unrepresentative training data or flawed model design.

### Examples:

1. **Healthcare Allocation:** An algorithm used in US hospitals to allocate health resources used "healthcare costs" as a proxy for "health needs." Because Black patients historically had less access to care and therefore spent less money, the AI incorrectly concluded they were healthier than equally sick White patients, denying them necessary extra care.
2. **Generative AI Stereotypes:** Text-to-image generators (like early versions of Stable Diffusion or Midjourney) frequently defaulting to generating images of men when prompted for "CEO" or "Doctor," and women when prompted for "Nurse" or "Assistant," reinforcing gender roles.

**Q2: Explain the difference between transparency and explainability in AI. Why are both important?**

- **Transparency** refers to the visibility of the system's design and governance. It answers: Do we know what data was used? Do we know who built it? Is the model architecture open?
- **Explainability (XAI)** refers to the ability to understand why a model made a specific prediction. It answers: Why was this specific loan application rejected?

**Importance:** Transparency builds trust in the development process (accountability), while explainability allows users to trust specific decisions and enables developers to debug errors or biases (reliability).

**Q3: How does GDPR (General Data Protection Regulation) impact AI development in the EU?** The GDPR enforces strict data handling which impacts AI by:

1. **Right to Explanation (Article 22):** Users have the right to challenge decisions made solely by automated processing.
2. **Data Minimization:** AI developers cannot hoard data "just in case"; they must only collect what is necessary.
3. **Consent:** Explicit consent is required to use personal data for model training.

## 2. Ethical Principles Matching

- **Non-maleficence:** (B) Ensuring AI does not harm individuals or society.
- **Autonomy:** (C) Respecting users’ right to control their data and decisions.
- **Sustainability:** (D) Designing AI to be environmentally friendly.
- **Justice:** (A) Fair distribution of AI benefits and risks.

# Part 2: Case Study Analysis (40%)

## Case 1: Biased Hiring Tool (Amazon)

*Scenario: An AI recruiting tool penalized female candidates.*

**1. Source of Bias:** The primary source was **Training Data Bias (Historical Bias)**. The model was trained on resumes submitted to Amazon over a 10-year period. Since the tech industry was historically male-dominated, the training data contained far more male resumes. The model learned that "male" features (or language patterns common in male resumes) correlated with "hired," effectively teaching itself that men were preferable.

**2. Three Fixes:**

1. **Data Balancing/Resampling:** Use techniques to oversample underrepresented groups (female resumes) in the training set to ensure the model sees an equal distribution of successful candidates across genders.
2. **Feature Blindness/Removal:** Remove explicit gender indicators (Names, pronouns like "he/she") and proxies (e.g., "Women's Chess Club," names of all-women colleges) during the pre-processing stage.
3. **Regularization for Fairness:** Apply an in-processing algorithm (like Adversarial Debiasing) that specifically penalizes the model during training if it attempts to use gender as a predictive factor.

**3. Evaluation Metrics:**

- **Demographic Parity:** Ensures the selection rate is roughly equal for both men and women.
- **Equal Opportunity Difference:** Measures if qualified women are being rejected at a higher rate than qualified men.

## Case 2: Facial Recognition in Policing

*Scenario: A facial recognition system misidentifies minorities at higher rates.*

**1. Ethical Risks:**

- **Wrongful Arrests/Incarceration:** Higher false positive rates for minorities lead to innocent individuals being detained, causing psychological trauma and loss of liberty (Justice/Non-maleficence).
- **Chilling Effect on Civil Liberties:** The fear of constant surveillance may stop minority communities from exercising rights to protest or assembly (Autonomy).
- **Feedback Loops:** If police rely on biased AI, they may patrol minority neighborhoods more aggressively, generating more arrest data that reinforces the bias.

**2. Recommended Policies:**

- **Human-in-the-Loop Mandate:** Facial recognition matches should never automatically trigger an arrest warrant. A human analyst must verify every match independently.
- **Ban on Real-Time Surveillance:** Prohibit the use of real-time scanning of public spaces (Live FRT) to protect privacy, restricting use only to post-event forensic investigation of serious crimes.
- **Mandatory Third-Party Audits:** Before deployment, the vendor must pass a NIST (National Institute of Standards and Technology) benchmark showing no significant disparity in accuracy across skin tones.

# Part 3: Practical Audit (25%)

*(See attached Python Script fairness_audit.py for code and visualizations)*

**Summary Report:** Our audit of the Recidivism prediction logic (simulating COMPAS) revealed significant biases. When analyzing risk scores, African-American defendants experienced a significantly higher **False Positive Rate (FPR)** compared to Caucasian defendants. This means the model was more likely to incorrectly label a black defendant as "high risk" even if they did not re-offend. Conversely, Caucasian defendants had higher False Negative Rates, meaning they were more likely to be labeled "safe" but went on to re-offend.

**Remediation Steps:** To fix this, we recommend calibrating the thresholds. Instead of using a single cutoff score (e.g., 5) for all groups, we should calculate group-specific thresholds to equalize the False Positive Rates (EqFPR), or retrain the model using a re-weighing algorithm to reduce the influence of sensitive attributes.

# Part 4: Ethical Reflection (5%)

**Project:** *Personalized Loan Approval App (Future Project)*

**Strategy:** To ensure this project adheres to ethical principles, I will implement **Privacy by Design**. Instead of sending user financial data to a central cloud server (which risks leaks), I will use **Federated Learning**, where the model trains on the user's phone locally. Furthermore, to ensure **Justice**, I will specifically test the model against "protected classes" (age, gender, zip code) to ensure the approval rate does not deviate by more than 20% (the 80% rule) between groups before the app is ever released to the App Store.

# Bonus Task: Policy Proposal (Healthcare)

## Policy Guideline: Ethical AI Use in Clinical Diagnostics

1. **Purpose** To ensure AI tools used in this hospital enhance patient care without introducing bias or eroding patient trust.

2. **Patient Consent Protocols**

- **Dynamic Consent**: Patients must be informed if an AI tool is being used to aid in their diagnosis.
- **Opt-Out**: Patients retain the right to have their diagnosis reviewed by a senior specialist without AI assistance if they object to the technology.

3. **Bias Mitigation Strategies**

- **Representation Check**: No AI tool will be procured unless the vendor can demonstrate the training data included at least 30% representation from minority demographics relevant to our local patient population.
- **Continuous Monitoring**: Clinical outcomes will be tracked by patient demographics. If the AI's error rate for a specific demographic exceeds the baseline by 5%, the tool is immediately suspended.

4. **Transparency & Accountability**

- **Model Cards**: Every AI tool must have an accessible "Model Card" available to clinicians, detailing its intended use, limitations, and training data source.
- **Clinician Override**: The human doctor always holds the final liability. The AI is a "Decision Support Tool," not a "Decision Maker."