# Smart ATS

Smart ATS is an Application Tracking System designed to evaluate resumes against job descriptions with high accuracy. It leverages advanced generative AI to provide valuable feedback for improving resumes, particularly in tech fields such as software engineering, data science, data analysis, and big data engineering.

## Features

- **JD Match Percentage:** Calculates the match between the resume and the job description.
- **Missing Keywords:** Identifies crucial missing keywords.
- **Profile Summary:** Summarizes the candidate’s profile and fit for the job.
- **Education Background Check:** Verifies if the candidate’s education meets job requirements.
- **Project Suggestions:** Recommends projects to add, including example names and problem statements.

## Getting Started

### Prerequisites

- Python 3.7+
- Streamlit
- Google Generative AI API Key
- PyPDF2
- dotenv

### Installation

1. Clone the repository:

    ```bash
    git clone https://github.com/devnayyar/ATS_LLM.git
    cd smart-ats
    ```

2. Create a virtual environment and activate it:

    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. Install the required packages:

    ```bash
    pip install -r requirements.txt
    ```

4. Create a `.env` file in the root directory and add your Google API Key:

    ```env
    GOOGLE_API_KEY=your_google_api_key
    ```

### Running the Application

1. Start the Streamlit application:

    ```bash
    streamlit run app.py
    ```

2. Open your browser and go to `http://localhost:8501` to view the application.

## Usage

1. Paste the job description in the provided text area.
2. Upload the resume (PDF format).
3. Click the "Submit" button to get the evaluation.

## Example Code

Below is a snippet of the core implementation:

```python
import streamlit as st
import google.generativeai as genai
import os
import PyPDF2 as pdf
from dotenv import load_dotenv
import json

load_dotenv()  # Load environment variables

genai.configure(api_key=os.getenv("GOOGLE_API_KEY"))

def get_gemini_response(input):
    model = genai.GenerativeModel('gemini-pro')
    response = model.generate_content(input)
    return response.text

def input_pdf_text(uploaded_file):
    reader = pdf.PdfReader(uploaded_file)
    text = ""
    for page in range(len(reader.pages)):
        page = reader.pages[page]
        text += str(page.extract_text())
    return text

# Prompt Template and Streamlit code omitted for brevity
```

## Learning Journey

This project also marks the beginning of my learning journey with **AWS SageMaker**. I have learned how to deploy machine learning models using AWS SageMaker and integrate with S3 buckets. Next, I plan to deploy the Smart ATS on SageMaker to enhance performance and scalability.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

## Acknowledgments

- Special thanks to Krish Naik for his insightful YouTube tutorial on AWS SageMaker.
- Thanks to the open-source community for their valuable resources and tools.
