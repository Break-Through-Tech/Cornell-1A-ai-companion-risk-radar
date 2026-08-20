---

> ## Challenge Advisor: Update & Finalize Your Project Overview
>
> > 💡 **These grey text instructions are just for you, the team's Challenge Advisor; please delete them once you have completed the steps below.**
>
> We've pre-populated this Challenge Project Overview page — which is what will be shared with your Break Through Tech student team in August — using the details from your submission form. You should have received an email inviting you to join this repo as a Collaborator, enabling you to add files and make edits.
> 
> In order for your project to be finalized and assigned to a team, please:
> 1. **Review all sections below** and update or expand any content as needed, making sure to address the SME Feedback in the section immediately below. Look for square brackets to find the places below that require additional inputs from you (e.g., "About [Company / Org Name]").
> 2. **Add your dataset** to the [data folder](data) in this repo.
> 3. **Close the Issue assigned to you in this repo** to let us know that you have made your edits and the overview page is ready for final review. You can do this by going to the _Issues_ tab in the top left section of the menu above, add a comment that says "CA review complete", and click the button to Close the Issue. 
>
> If you're unfamiliar with how to edit a page like this in GitHub, check out [this tutorial](https://ubc-lib-geo.github.io/gis-workshop-waml-template/content/handson/edit-readme.html) for a quick overview (start with step 2 and only edit this page), and [this guide](https://ubc-lib-geo.github.io/gis-workshop-waml-template/content/markdown.html) on how to use Markdown to compose text.
>
>
> ❌ Remember that this is a public repo. Do NOT include: Proprietary data, PII, API keys, credentials, or anything confidential.

---


## 📋 BTT Internal Evaluation Notes
*(This section is for BTT staff only — remove before sharing with students)*

| Check | Status | Notes |
|-------|--------|-------|
| Python Compatibility | 🟢 | The project uses Python-compatible libraries for NLP and classification tasks, aligning with students' current skills. |
| Data Readiness | 🟢 | The dataset is under 1GB and stored in CSV/TSV format, making it accessible and ready for immediate use, facilitating effective learning in data preparation. |
| Resource Check | 🟢 | All required tools and platforms (e.g., Google Colab) are readily available to students without access issues. |

**Student Fit Score:** 8/10  
**Technical Depth Score:** 7/10  
**Overall Recommendation:** APPROVE

**Advisor Feedback Draft:**
The project effectively leverages NLP for real-world applications in mental health. However, consider providing a more structured approach to data cleaning and annotate the dataset with explicit guidelines. Additionally, ensure that classification models are accessible for interpretation by non-technical stakeholders. Please take these adjustments into account to enhance project clarity and objectives.

---

# AI Companion Risk Radar: Classifying Risk in Mental Health Apps

**Company / Org:** Cornell Brooks School of Public Policy  
**Challenge Advisor:** Ibrahim Emara, ie68@cornell.edu              
**AI Studio Coach:** Shaun Figueiro, shaun.figueiro@breakthroughtech.org              
**Program:** Break Through Tech AI Studio - Fall 2026       

---

## 🏢 About Cornell Brooks School of Public Policy

The Cornell Brooks School of Public Policy is dedicated to advancing the well-being of all people through the development of new knowledge to solve pressing global policy challenges, rigorous training of the next generation of policy leaders, and active engagement with policymaking around the globe.

---

## 🎯 The Challenge

### Project Summary
In this project, you will use public mental health app review data and natural language processing/supervised classification techniques to build a model that classifies user-reported risk themes in app reviews, such as dependence, attachment, isolation, crisis-response frustration, or other concerns. This will help product, trust and safety, compliance, and app-quality teams better identify recurring user-risk signals that may not be visible from safety policies alone.

### Success Criteria
Success will be measured by whether the team can produce a clear, reproducible risk-theme classification workflow using public app review data. A successful December outcome would include:

- A cleaned and documented review dataset or subset.
- A labeled training sample with a clear risk-theme codebook.
- At least one baseline classifier that predicts review-level risk themes.
- Model evaluation using macro F1, per-class precision/recall, and confusion matrices.
- Error analysis explaining where the model performs well or poorly.
- A final presentation that explains what the results mean for product, trust and safety, compliance, or app-quality teams.

If the team completes the optional dashboard, success would also include a basic visualization of which risk themes appear most often by app and, if feasible, over time.

### Stretch Goals
If the team progresses quickly, the natural stretch goal is a 'Temporal Risk Theme' Dashboard. The team could aggregate labeled reviews by app, risk theme, and week or month to show whether certain themes rise over time or cluster around specific tools. A further extension could compare AI/chatbot-relevant apps with broader mental health apps.

### Project Milestones

Use these milestones to guide your work. Your team will create a **GitHub Projects board** to track tasks within each milestone.

| Month | Milestone | Key Activities |
|---|---|---|
| September | Data exploration, preprocessing, and label design | • Review the MHARD mental health app review dataset and data dictionary.<br>• Explore review text, app names, star ratings, dates, helpful counts, and metadata.<br>• Subset AI/chatbot-relevant apps if feasible.<br>• Define a small risk-theme taxonomy, such as dependence, attachment, isolation, crisis-response frustration, and other.<br>• Hand-label a training sample and check basic label consistency. |
| October | Baseline modeling and model comparison | • Convert review text into model-ready features using methods such as TF-IDF.<br>• Train baseline supervised classifiers, such as logistic regression and random forest.<br>• Compare model performance across risk-theme classes.<br>• Review errors to understand which themes are easy or difficult to detect. |
| November | Evaluation, interpretation, and optional dashboard prototype | • Finalize evaluation metrics, including macro F1 and per-class precision/recall.<br>• Interpret which words, features, or review patterns help classify each risk theme.<br>• If time allows, aggregate labeled reviews by app and time period to build a simple dashboard showing risk-theme patterns. |

> **Note for the team:** Please create a GitHub Projects board in this repository to break these milestones into weekly tasks. Go to the **Projects** tab → **New project** → Choose **Board** → Add columns for each month.

---

## 📊 Dataset

**Name and Source:** AI-Mediated Mental Health Support on Reddit: Annotated Dataset of 5,126 Posts Across 47 Communities — Aghakhani & Rezapour (2026), Zenodo
**Format:** CSV 
**Size:** ~2.3 MB
**Location:** https://github.com/Sensify-Lab/MHARD; https://zenodo.org/records/18751157

### Key Details
- Contains 5,126 Reddit posts from 47 mental health-related subreddits discussing AI use for emotional support and therapy-related purposes.
- Includes annotations for factors such as:
    A. Perceived usefulness
    B. Trust
    C. Risks
    D. Bond
    E. Sentiment
    F. Usage intent
    G. Comparison to human therapy
- **Limitation**: Raw post text is not included; the dataset provides raw identifiers and derived annotations to reduce re-identification risk.
---

## 🛠️ Suggested Approach

**ML Problem Type:** Classification, NLP, Time Series Analysis

**Recommended Libraries:**
- [e.g., pandas, scikit-learn, TensorFlow, Hugging Face]

**Evaluation Metrics:**
- [e.g., Accuracy, Precision/Recall, RMSE, BLEU score]

---

## 📚 Resources to Get Started

The following resources will help your team understand the problem space and potential technical approaches for this project:

**Background Reading:**
- [e.g., Link to an article or blog post about the problem domain]
- [e.g., Link to an industry report or case study]

**Technical Tutorials:**
- [e.g., Link to a free tutorial on the ML technique(s) involved]
- [e.g., Link to documentation for a key library or tool]

**Code Examples:**
- [e.g., Link to a relevant GitHub repo]
- [e.g., Link to a sample implementation or starter code]

**Other:**
- [Links to any additional resources — e.g., papers, videos, podcasts, etc.]

*Feel free to explore beyond these, and share anything interesting you find with me!*

---

## 🤝 How We'll Work Together

**Official check-ins:** During our biweekly 45-minute AI Studio Lab Section meeting block (2nd and 4th week of every month)

 **Other ways to reach out to me with questions:** 
* [e.g., Your team's channel within Break Through Tech’s Discord space]
* [e.g., Email; please copy your teammates and AI Studio Coach]
* [e.g., Request a team check-in on Zoom]
* [Note: I will aim to respond within 48 hours. Please reach out to your AI Studio Coach with urgent questions.]

> 💡 **Challenge Advisor: Please update the above based on your availability and preference. If you are not able to answer questions or meet with fellows outside of the biweekly Lab Section check-ins, simply write in "N/A (only available during the official check-in times)"**

**Recommended free coding / collaboration tools**
* […]
* […]

---

## 🚀 Getting Started

1. **Review this overview document** and note any questions for our first meeting
2. **Begin reviewing the dataset** using the link above
3. **Read the GitHub Projects documentation** [here](https://docs.github.com/en/issues/planning-and-tracking-with-projects/learning-about-projects/about-projects)

I’m excited to work with you!

---

## ❓ Questions?

Please bring any questions to our first meeting during the week of August 24th (Break Through Tech’s Bridge to Studio - Session C). 
