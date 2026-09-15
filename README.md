# Agentic_AI_FacilityOps_and_SDLC_Platform-


A conversational AI application for managing dental appointments using **LangGraph, LangChain, and Grok-4 through the xAI API**. The system uses a multi-agent architecture to understand user requests and route them to specialized agents for appointment-related operations.

## Features

The system supports the following operations through natural language:

* Check available dental appointment slots
* View doctor information and specializations
* Book new dental appointments
* Cancel existing appointments
* Reschedule appointments
* Check a patient's existing appointments
* Route user requests through a supervisor agent

## Architecture

The application follows a supervisor-based multi-agent architecture.

```text
                         ┌─────────────────┐
                         │   Supervisor    │
                         │ Intent Routing  │
                         └────────┬────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
          ▼                       ▼                       ▼
   ┌──────────────┐       ┌──────────────┐       ┌──────────────┐
   │  Info Agent  │       │ Booking Agent│       │ Cancel Agent │
   └──────────────┘       └──────────────┘       └──────────────┘
                                  │
                                  ▼
                         ┌────────────────┐
                         │ Reschedule     │
                         │ Agent          │
                         └────────────────┘
```

### Agent Responsibilities

* **Supervisor Agent:** Identifies the user's intent and routes the request.
* **Info Agent:** Handles doctor information, available slots, and patient appointment queries.
* **Booking Agent:** Creates new appointments after validating the requested slot.
* **Cancellation Agent:** Cancels existing appointments.
* **Rescheduling Agent:** Moves appointments to a different date or time.

## Technology Stack

* **Python:** Application development
* **LangGraph:** Multi-agent workflow orchestration and state management
* **LangChain:** LLM integration and tool execution
* **Grok-4:** Conversational AI model through the xAI API
* **Pandas:** CSV data processing
* **Pydantic:** Data validation
* **python-dotenv:** Environment variable management
* **CSV:** Appointment data storage

## Project Structure

```text
Dental-Appointment-System/
│
├── main.py
├── doctor_availability.csv
├── requirements.txt
├── .env
├── .gitignore
├── README.md
│
└── dental_agent/
    ├── agent.py
    ├── utils.py
    │
    ├── agents/
    │   ├── supervisor.py
    │   ├── info_agent.py
    │   ├── booking_agent.py
    │   ├── cancellation_agent.py
    │   └── rescheduling_agent.py
    │
    ├── config/
    │   └── settings.py
    │
    ├── models/
    │   └── state.py
    │
    ├── tools/
    │   ├── csv_reader.py
    │   └── csv_writer.py
    │
    └── workflows/
        └── graph.py
```

## Requirements

Before running the project, install the following:

* Python 3.10 or higher
* Anaconda or Miniconda
* An xAI API key with access to the selected model

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Mahfooz167/Agentic_AI_FacilityOps_and_SDLC_Platform-.git
```

Navigate to the project directory:

```bash
cd Agentic_AI_FacilityOps_and_SDLC_Platform-
cd Dental-Appointment-System
```

### 2. Create a Conda Environment

```bash
conda create -n dental-agent python=3.12
```

Activate the environment:

```bash
conda activate dental-agent
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root directory:

```env
XAI_API_KEY=your_xai_api_key_here
MODEL_NAME=grok-4
TEMPERATURE=0
```

Replace `your_xai_api_key_here` with your actual xAI API key.

**Important:** Never publish your real API key on GitHub or share it publicly.

## Running the Application

Make sure the Conda environment is activated and you are inside the project directory:

```bash
conda activate dental-agent
```

Run the application:

```bash
python main.py
```

The system will open an interactive command-line interface.

Type `quit` to exit the application.

## Example Queries

### Check Available Slots

```text
Show available slots for an orthodontist
```

### Book an Appointment

```text
Book patient 1000082 with Emily Johnson on 5/10/2026 9:00
```

### Check Patient Appointments

```text
What appointments does patient 1000048 have?
```

### Cancel an Appointment

```text
Cancel appointment for patient 1000082 at 5/10/2026 9:00
```

### Reschedule an Appointment

```text
Reschedule patient 1000082 from 5/10/2026 9:00 to 5/12/2026 10:00
```

## Supported Dental Specializations

The appointment data supports the following specializations:

* General Dentist
* Oral Surgeon
* Orthodontist
* Cosmetic Dentist
* Prosthodontist
* Pediatric Dentist
* Emergency Dentist

## Data Storage

Appointment information is stored in:

```text
doctor_availability.csv
```

The CSV file contains fields such as:

| Field               | Description                               |
| ------------------- | ----------------------------------------- |
| `date_slot`         | Appointment date and time                 |
| `specialization`    | Dental specialization                     |
| `doctor_name`       | Doctor's name                             |
| `is_available`      | Whether the appointment slot is available |
| `patient_to_attend` | Patient ID assigned to the appointment    |

The system uses CSV reader and writer tools to retrieve and update appointment information.

## Workflow

The application follows this general workflow:

1. The user enters a natural-language request.
2. The supervisor agent identifies the intent.
3. The request is routed to the correct specialized agent.
4. The specialized agent uses the required tools.
5. Appointment data is read or updated.
6. The system returns a response to the user.

## Environment Verification

To verify that the required Python packages are installed, run:

```bash
python -c "import langchain, langgraph, langchain_xai, pandas, dotenv, pydantic; print('All required packages are working')"
```

To check the installed xAI integration package:

```bash
pip show langchain-xai
```

To check the current configuration:

```bash
python -c "from dental_agent.config.settings import MODEL_NAME, TEMPERATURE, XAI_API_KEY; print('Model:', MODEL_NAME); print('Temperature:', TEMPERATURE); print('API key configured:', XAI_API_KEY != 'API_KEY')"
```

## Current Configuration

The default configuration uses:

```env
MODEL_NAME=grok-4
TEMPERATURE=0
```

The application requires a valid xAI API key to communicate with the Grok model.

## Educational Purpose

This project demonstrates practical AI engineering concepts, including:

* Multi-agent system design
* Intent classification
* Supervisor-based routing
* LangGraph workflow orchestration
* Tool calling
* State management
* Structured data validation
* CSV-based data operations
* Natural-language appointment management

## Future Improvements

Possible future enhancements include:

* Replacing CSV storage with a relational database
* Adding a web-based user interface
* Adding patient authentication
* Adding doctor and administrator dashboards
* Supporting appointment reminders
* Adding conversation memory
* Supporting local LLMs through Ollama
* Adding automated tests
* Deploying the application as an API service

## License

This project is intended for educational and demonstration purposes.
