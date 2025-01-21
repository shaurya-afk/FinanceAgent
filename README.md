# Finance Agent Project

## **Overview**
The Finance Agent Project is an AI-powered system designed to retrieve and analyze financial information, such as stock prices, analyst recommendations, company news, and more. The agent utilizes Phidata tools, `Groq` large language models, and `YFinanceTools` to provide meaningful financial insights in structured formats like tables.

---

## **Features**
- Fetch real-time stock prices.
- Summarize analyst recommendations.
- Display company profiles and news.
- Present output in Markdown with a table structure for readability.
- Supports debugging and logs all tool calls for transparency.

---

## **Requirements**
Ensure the following are installed and configured before running the project:

### **System Requirements**
- **Operating System**: Windows/Linux/MacOS
- **Python Version**: 3.12 (managed via `uv`)

### **Dependencies**
- `phidata`
- `yfinance`
- `dotenv`

---

## **Setup Instructions**

### **Step 1: Install `uv` Python Manager**
1. Open PowerShell as Administrator.
2. Run the following commands to install `uv`:
   ```powershell
   Invoke-WebRequest -Uri https://astral.sh/uv/install.ps1 -OutFile install.ps1
   powershell -ExecutionPolicy Bypass -File ./install.ps1
   ```

### **Step 2: Install Python 3.12**
1. Use `uv` to install Python:
   ```powershell
   uv python install 3.12
   ```
2. Verify Python installation:
   ```powershell
   uv python --version
   ```

### **Step 3: Initialize the Project**
1. Set up a new project environment:
   ```powershell
   uv init -p 3.12 --name finance_agent_project
   ```
2. Open the project in VS Code:
   ```powershell
   code .
   ```

### **Step 4: Install Dependencies**
1. Add the required packages using:
   ```powershell
   uv add phidata yfinance dotenv
   ```
2. Verify installed dependencies:
   ```powershell
   uv list
   ```

### **Step 5: Configure API Keys**
1. Obtain your API keys:
   - **Phidata API Key:** [Phidata](https://phidata.app)
   - **Groq API Key**: [Groq Cloud](https://groq.app)
2. Create a `.env` file in the project directory and add:
   ```plaintext
   PHI_API_KEY="your_phidata_api_key"
   GROQ_API_KEY="your_groq_api_key"
   ```

---

## **Usage**

### **1. Create and Run `finance_agent.py`**
Use the following script to create and run the finance agent:

```python
from phi.agent import Agent
from phi.model.groq import Groq
from phi.tools.yfinance import YFinanceTools
from dotenv import load_dotenv

load_dotenv()

finance_agent = Agent(
    description="Your task is to find finance information",
    model=Groq(id="llama-3.3-70b-versatile"),
    tools=[
        YFinanceTools(
            stock_price=True,
            analyst_recommendations=True,
            company_info=True,
            company_news=True
        )
    ],
    instructions=["Use tables to display data"],
    show_tool_calls=True,
    markdown=True,
    debug_mode=True
)

finance_agent.print_response(
    "Summarize analyst recommendations for TSLA", stream=True
)
```

Run the script:
```powershell
uv run finance_agent.py
```

### **2. Expand Functionality**
You can create multi-agent systems or extend the current agent by integrating other tools like web search, image analysis, etc., as per the project documentation.

---

## **Troubleshooting**

1. **`uv` Command Not Recognized**
   - Ensure `C:\Users\<YourUsername>\.local\bin` is added to your PATH environment variable.
   - Restart your terminal or system after updating PATH.

2. **API Key Issues**
   - Double-check the `.env` file for correct API keys.
   - Ensure the keys have proper access rights.

3. **Dependency Errors**
   - Reinstall missing dependencies using `uv add <dependency_name>`.

---
