# Hiring Assistent Chatbot


## 📌 Project Overview

**Hiring Assistent Chatbot** is an intelligent Streamlit-based chatbot that automates and enhances the candidate screening process. By leveraging **LLMs (LLaMA 3 70B via Groq)** and resume parsing tools, it gathers structured candidate data, assesses technical competencies, and generates an evaluation report — all within an interactive, dynamic UI. The assistant adapts its questioning style based on user inputs and confidence levels, offering a highly personalized and scalable interview experience.

---

## ⚙️ Installation Instructions

### 1. Clone the Repository


```bash
git clone https://github.com/tanishq056/Hiring-assistent-chatbot
cd Hiring-assistent-chatbot
```

### 2. Create a Virtual Environment (Recommended)

```bash
python -m venv venv
source venv/bin/activate       # macOS/Linux
venv\Scripts\activate        # Windows
```

### 3. Install Dependencies


```bash
pip install -r requirements.txt
```


### 4. Set up Secrets

Create a `.streamlit/secrets.toml` file to securely store your API key:


```toml
GROQ_API_KEY = "your_groq_api_key_here"
```


### 5. Run the Application


```bash
streamlit run app.py
```

---


## 🧑‍💻 Usage Guide

1. **Upload Resume**: Upload a `.pdf` or `.docx` file of the candidate’s resume.
2. **Resume Analysis**: The assistant extracts key details like name, email, skills, experience, and validates consistency.
3. **Technical Interview**:
   - Select a **persona** (e.g., Expert, Analytical, Creative).
   - Answer **LLM-generated technical questions** based on your tech stack.
   - Provide a **confidence level** for each response (Low, Medium, High).
   - Receive **follow-up questions** accordingly.
4. **Evaluation**: The assistant scores the candidate, highlights strong/weak areas, and makes a recommendation.
5. **Report Generation**: Download a complete evaluation report.

---


## 🔍 Technical Details

### 🧰 Libraries & Tools

- `Streamlit` – Web UI framework
- `LangChain` – LLM pipeline orchestration
- `Groq API` – LLaMA 3-70B inference
- `PyPDF2` / `python-docx` – Resume parsing
- `re` – Pattern extraction
- `dotenv` – Secrets handling

### 🧠 Model Used

- **LLaMA 3-70B via Groq API**
- Provides fast, high-quality completions for technical questions and evaluations.

### 🧱 Architecture


```
User → Streamlit Frontend → Resume Parser → Persona Selection → LLM Q&A Loop
     → Evaluation Logic → LangChain → Groq API → Response → Report Generator
```


---

## ✍️ Prompt Design

### 🧾 Information Gathering Prompts

Crafted using structured role-based prompts like:

```text
"You are a resume parser bot. Extract the following information: Name, Email, Phone, Tech Stack, Projects, Education..."
```

These are followed by consistency checks, such as:

```text
"Is the declared tech stack used consistently across the resume?"
```

### 🧠 Technical Question Prompts

We use **persona-based prompting** to adapt question difficulty and tone:

```text
"As an expert-level technical interviewer, generate 3 deep-dive questions on {tech_stack} for a candidate with X years of experience."
```

Follow-up questions are triggered when confidence is below a threshold:

```text
"Generate a follow-up question to probe further based on the previous answer."
```

---

## 🚧 Challenges & Solutions

### Challenge: Inconsistent Resume Formats  
**Solution**: Used a hybrid parser for `.pdf` and `.docx`, followed by regex-based key phrase matching.

### Challenge: Dynamic Technical Evaluation  
**Solution**: Created a confidence-based loop to guide the LLM on when to ask deeper questions or move on.

### Challenge: Persona-Based Conversations  
**Solution**: Designed multiple personas with prompt templates and injected their traits into the system message using LangChain’s chat memory.

### Challenge: Speed & Token Limits  
**Solution**: Chose Groq for ultra-fast LLaMA inference and used chunked context to avoid exceeding token limits.

---
