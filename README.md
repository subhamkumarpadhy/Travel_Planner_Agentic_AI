# **🌍 AI-Based Trip Planner (Agentic AI)**

**Moto:** Plan a trip for any destination worldwide with real-time data.

## **✨ Introduction**

The AI-Based Trip Planner is an intelligent application designed to revolutionize travel planning. Leveraging the power of Agentic AI and the LangGraph framework, this project automates the complex process of creating detailed travel itineraries. It integrates real-time data from various external sources to provide comprehensive, personalized, and up-to-the-minute travel plans for any destination across the globe.

Say goodbye to endless tabs and manual research – let our AI agent handle the heavy lifting, providing you with two distinct plans: one for popular tourist spots and another for more off-beat, unique locations around your chosen destination.

## **🚀 Features**

* **Real-time Weather Information:** Get current and forecasted weather conditions for your destination to pack perfectly.  
* **Attractions & Activities:** Discover popular tourist attractions and exciting activities in and around your chosen location.  
* **Hotel Cost Estimation:** Receive approximate per-night hotel costs for multiple days.  
* **Currency Conversion:** Seamlessly convert currencies for accurate budget planning.  
* **Complete Itinerary Generation:** A detailed, day-by-day breakdown of your trip.  
* **Total Expense Calculation:** Get a comprehensive overview of all estimated costs.  
* **Daily Expense Budget:** Understand your approximate spending per day.  
* **Restaurant Recommendations:** Find top-rated eateries and their price ranges.  
* **Transportation Details:** Information on available modes of transport in the area.  
* **Comprehensive Trip Summary:** A concise overview of your entire travel plan.  
* **Dynamic Planning:** The agent intelligently uses tools and LLMs to adapt to your queries and provide relevant information.  
* **Markdown Export:** Easily save your generated travel plans to a well-formatted Markdown file.

## **🏗️ Architecture**

This project employs a robust agentic architecture built on **LangGraph**, enabling a multi-agent system to handle complex, dynamic queries.

* **Frontend (Streamlit):** A user-friendly web interface for interacting with the AI agent.  
* **Backend (FastAPI):** A lightweight and fast API that serves as the communication bridge between the frontend and the core AI logic.  
* **Agentic Workflow (LangGraph):** The heart of the application. It orchestrates various specialized AI agents (tools) and Large Language Models (LLMs) in a stateful graph. This allows for iterative reasoning, tool use, and decision-making to fulfill complex travel planning requests.  
* **LLM Integration:** Utilizes langchain\_groq (default: deepseek-r1-distill-llama-70b) and langchain\_openai for powerful natural language understanding and generation.  
* **External Tools/APIs:**  
  * **OpenWeatherMap API:** For real-time weather data.  
  * **Google Places API:** For searching attractions, restaurants, activities, and transportation.  
  * **Tavily Search API:** As a fallback for place-related searches if Google Places encounters issues, ensuring robust information retrieval.  
  * **ExchangeRate-API:** For real-time currency conversion.  
  * **Custom Calculator:** For expense estimations and budget calculations.

The system prompt guides the LLM to act as a helpful travel agent, ensuring comprehensive and well-structured responses.

## **⚙️ Tech Stack**

* **Python**  
* **LangChain & LangGraph:** For building and orchestrating AI agents.  
* **FastAPI:** For the backend API.  
* **Streamlit:** For the interactive web UI.  
* **python-dotenv:** For environment variable management.  
* **pydantic:** For data validation.  
* **httpx, requests:** For making HTTP requests to external APIs.  
* **langchain\_google\_community, langchain\_tavily, langchain\_groq, langchain\_openai:** LangChain integrations for various services.  
* **pyyaml:** For loading configuration from config.yaml.  
* **External APIs:** OpenWeatherMap, Google Places, Tavily, ExchangeRate-API.

## **🚀 Installation & Setup**

Follow these steps to get the AI-Based Trip Planner up and running on your local machine.

### **Prerequisites**

* Python 3.9+  
* API Keys for the following services:  
  * OPENWEATHERMAP\_API\_KEY (from [OpenWeatherMap](https://openweathermap.org/api))  
  * GPLACES\_API\_KEY (from [Google Cloud Platform \- Places API](https://developers.google.com/maps/documentation/places/web-service/overview))  
  * TAVILY\_API\_KEY (from [Tavily AI](https://tavily.com/))  
  * EXCHANGE\_RATE\_API\_KEY (from [ExchangeRate-API.com](https://www.exchangerate-api.com/))  
  * GROQ\_API\_KEY (from [GroqCloud](https://groq.com/)) \- *Required if using Groq models.*  
  * OPENAI\_API\_KEY (from [OpenAI](https://platform.openai.com/)) \- *Required if using OpenAI models.*

### **Steps**

1. **Clone the repository:**  
   git clone https://github.com/subhamkumarpadhy/Travel_Planner_Agentic_AI
   cd AI-Trip-Planner

2. **Create a virtual environment (recommended):**  
   python \-m venv venv  
   source venv/bin/activate  \# On Windows: venv\\Scripts\\activate

3. **Install dependencies:**  
   pip install \-r requirements.txt

   (Note: requirements.txt is generated from setup.py which uses get\_requirements(). Ensure requirements.txt is present or run python setup.py install if it's not.)  
4. Set up environment variables:  
   Create a .env file in the root directory of the project and add your API keys:  
   OPENWEATHERMAP\_API\_KEY="your\_openweathermap\_api\_key"  
   GPLACES\_API\_KEY="your\_gplaces\_api\_key"  
   TAVILY\_API\_KEY="your\_tavily\_api\_key"  
   EXCHANGE\_RATE\_API\_KEY="your\_exchange\_rate\_api\_key"  
   GROQ\_API\_KEY="your\_groq\_api\_key"  
   OPENAI\_API\_KEY="your\_openai\_api\_key"

   *Make sure to replace "your\_..." with your actual API keys.*  
5. Run the FastAPI backend:  
   Open a new terminal, activate your virtual environment, and run:  
   uvicorn main:app \--reload \--port 8000

   The backend will be running at http://localhost:8000.  
6. Run the Streamlit frontend:  
   Open another new terminal, activate your virtual environment, and run:  
   streamlit run streamlit\_app.py

   This will open the Streamlit application in your web browser.

## **💡 Usage**

Once both the FastAPI backend and Streamlit frontend are running:

1. Navigate to the Streamlit application in your browser.  
2. Enter your travel query in the input box (e.g., "Plan a trip to Paris for 7 days, including famous landmarks and local cuisine. What's the weather like?").  
3. Click "Send" and watch the AI agent generate a comprehensive travel plan, including all the requested details.  
4. The generated plan will be displayed in Markdown format directly in the Streamlit app and also saved as a .md file in the ./output directory.

## **📁 Project Structure**

.  
├── agent/  
│   └── agentic\_workflow.py           \# Defines the LangGraph agent orchestration  
├── config/  
│   └── config.yaml                   \# Configuration for LLM providers  
├── prompt\_library/  
│   └── prompt.py                     \# System prompt for the AI agent  
├── tools/  
│   ├── arithmatic\_operation.py       \# Basic arithmetic operations (e.g., multiply)  
│   ├── currency\_conversion\_tool.py   \# LangChain tool for currency conversion  
│   ├── expense\_calculator\_tool.py    \# LangChain tool for expense calculations  
│   ├── place\_search\_tool.py          \# LangChain tool for place-related searches (attractions, restaurants, etc.)  
│   └── weather\_info\_tool.py          \# LangChain tool for weather information  
├── utils/  
│   ├── load\_config.py                \# Utility to load configuration from YAML  
│   ├── currency\_converter.py         \# Handles external API calls for currency exchange  
│   ├── expense\_calculator.py         \# Core logic for expense calculations  
│   ├── model\_loader.py               \# Utility to load LLM models (Groq/OpenAI)  
│   ├── place\_info\_search.py          \# Handles external API calls for Google Places and Tavily  
│   ├── save\_to\_document.py           \# Utility to save generated plans to Markdown  
│   └── weather\_info.py               \# Handles external API calls for OpenWeatherMap  
├── main.py                           \# FastAPI backend application  
├── streamlit\_app.py                  \# Streamlit frontend application  
├── setup.py                          \# Project setup and dependency management  
├── requirements.txt                  \# List of Python dependencies  
└── .env                              \# Environment variables (API keys)

## **💡 Future Enhancements**

* Integration with hotel booking APIs for direct booking links.  
* Support for flight search and booking.  
* User authentication and personalized trip history.  
* Map integration for visualizing itineraries.  
* More advanced natural language understanding for complex, multi-turn conversations.  
* Integration with calendar applications.

## **🤝 Contributing**

Contributions are welcome\! If you have ideas for improvements or new features, feel free to:

1. Fork the repository.  
2. Create a new branch (git checkout \-b feature/YourFeature).  
3. Make your changes.  
4. Commit your changes (git commit \-m 'Add new feature').  
5. Push to the branch (git push origin feature/YourFeature).  
6. Open a Pull Request.