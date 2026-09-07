EcoSphere - Real-Time Voice AI Sales Agent
EchoSphere Hackathon | Team: Winners4
A production-oriented voice AI sales agent that conducts natural, real-time sales conversations using Agora Conversational AI, LangGraph, and RAG-powered product knowledge.
What It Does
EcoSphere conducts real-time voice sales calls that feel natural:
Qualifies leads by asking about needs, budget, and timeline
Answers pricing questions accurately using RAG (no hallucination)
Handles objections with empathy and provides relevant information
Schedules demos with human agents when needed
Remembers context throughout the entire conversation
Architecture
Code
Quick Start
Prerequisites
Python 3.9+
Agora account with App ID and Certificate
Deepgram API key (for STT)
MiniMax API key (for TTS)
1. Install Dependencies
Bash
2. Configure Environment
Create a .env file:
Env
3. Run
Option A: One-click start
Bash
Option B: Manual start
Terminal 1 - start the server:
Bash
Terminal 2 - start the voice pipeline:
Bash
Option C: Standalone REST API agent (no SDK needed)
Bash
4. Make a Call
Copy the channel name from Terminal 2
Open demo.html in your browser
Paste the channel name and click "Join Call"
Start speaking to the AI agent
Project Structure
Code
How It Works
Intent Classification
The agent classifies user intent in real-time:
Pricing - uses RAG to answer accurately from the product catalog
Objection - sub-classified into Price/Trust/Competitor/Timing/Authority, escalates after 3 objections
Demo - collects info and schedules a meeting
Competitor - professional differentiation without badmouthing
General - lead qualification with slot extraction (user_count, budget, timeline)
Objection Sub-Classification
Each objection is categorized into a sub-type for smarter routing:
Type
Response
Price
ROI-focused response + free trial offer
Trust
Security/SLA info + case studies
Competitor
Professional comparison + discovery questions
Timing
Timeline exploration + follow-up scheduling
Authority
Manager summary prep + include decision-maker
RAG-Powered Answers
Instead of making up answers, the agent retrieves accurate product information:
Python
Persistent Memory
All conversation state is saved to SQLite via LangGraph's SqliteSaver checkpointer. Sessions survive server restarts.
Slot Extraction
The agent automatically extracts and tracks:
user_count - team size mentioned by customer
pricing_tier_discussed - which plan was discussed
competitor_mentioned - which competitor was named
customer_info - name, email, company, role, budget, timeline
Slack Escalation
When objections pile up or a demo is requested, a full escalation payload is sent to Slack including customer info, conversation transcript, and objection history. Set SLACK_WEBHOOK_URL in .env to enable.
Tool Calling
The agent can use tools during conversation:
search_products(query) - find product information
get_pricing_summary() - get all pricing plans
schedule_meeting(...) - book a demo with the sales team
get_competitor_comparison(name) - compare against a competitor
Monitoring Dashboard
Open dashboard.html to see:
Live session list with auto-refresh every 5s
Full transcripts per session with customer/agent messages
Lead scoring that updates based on engagement signals
Objection tracking with sub-type classification
Slot values - user_count, pricing tier, competitor mentioned
Escalation status and outcome tracking
Tech Stack
Component
Technology
Voice Transport
Agora RTC
Speech-to-Text
Deepgram Nova-3
Text-to-Speech
MiniMax Turbo
Agent Framework
LangGraph
LLM
Groq (gpt-oss-20b)
RAG
ChromaDB (fallback: keyword search)
Backend
FastAPI
Frontend
Vanilla JS + Agora Web SDK
Team
Name
Role
Sumodip Patra
Agent Brain (LangGraph)
Harsh Kalbande
Voice Pipeline Engineer
Kanishk Patil
Backend & Integration
Yash Zunzurkar
Frontend, Demo Flow Lead
License
No license specified yet.
Built by Winners4