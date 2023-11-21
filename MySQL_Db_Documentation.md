# Welcome to Miski AI

## Introduction
Welcome to **Miski AI**. At Miski, we utilize state-of-the-art AI to revolutionize Business Intelligence. We offer you the next generation of conversational BI tools, bringing your data to life and making insights more accessible than ever.

## Miksi-IO SQL Agent
The Miksi-IO SQL Agent is a powerful tool designed to connect seamlessly with your SQL databases. It's part of the broader Miski AI ecosystem, crafted to enhance your experience with business intelligence.

### Important Information
Our agent interacts with your database by executing queries within sandboxed environments. While it's highly tuned not to execute queries that modify the database, we highly recommend that you do not run against the main production database and provide user accounts with no rights to modify the database. 

This is a Python documentation for the SQL agent.

## Process
1. **Create a Virtual Environment:**
   - `python -m venv venv`
   - or `python3 -m venv venv`
2. **Activate the Virtual Environment:**
   - Windows: `source venv/Script/activate`
   - Other platforms: `source venv/bin/activate`
3. **Generate API Key:**
   - Visit [MiksiAPI](https://miksiapi-miksi.pythonanywhere.com), sign up or log in, then generate your API key.
4. **Install Miksi SDK:**
   - Visit [MiksiSDK](https://pypi.org/project/miksisdk/0.0.6/)
   - Install the latest version: `pip install miksisdk==<version>`

## Using the Package
```python
from miksisdk.base import DatabaseConnector

# Connect to your database
connector = DatabaseConnector(db_user=db_user, db_password=db_password,
                              db_host=db_host, db_name=db_name)

# Check connection status
status = connector.connect()

# Get a new DB instance
db = connector.getdbinstance()

# Example function to get DB
def get_db():
    connector = DatabaseConnector(db_user=db_user, db_password=db_password,
                                  db_host=db_host, db_name=db_name)
    db = connector.getdbinstance()
    return db

db = get_db()  # The DB instance must be assigned to a global variable named 'db'


```python
# Simplified DB Connection Function
def get_db():
    connector = DatabaseConnector(db_user=db_user, db_password=db_password, 
                                  db_host=db_host, db_name=db_name)
    db = connector.getdbinstance()
    return db

db = get_db()
# Note: The DB instance should be assigned to a global variable named 'db', as it's required by the agent.

# Defining a Large Language Model (LLM)
# Define your own LLM:
llm = ChatOpenAI(model="model_name", openai_api_key=openai_api_key, 
                 temperature=0, streaming=True)
# Default Model: If not specified, the agent uses a predefined model.

# Creating the Agent
# Setting Up the Agent

# Import AgentInitializer:
from miksisdk.agent import AgentInitializer

# Instantiate the AgentInitializer:
agent_initializer = AgentInitializer(llm, db)

# Optionally, specify a path for image/chart storage:
path = 'your path here'
agent_initializer = AgentInitializer(llm, db, path)

# Create the agent:
agent = agent_initializer.create_agent()

# Running Queries
# Execute a query and get the response:
query = "use a chart to show top 10 countries in terms of sales"
response = agent.run(query)
