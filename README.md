# Real-Time Voice AI Calendar Assistant (Vapi + n8n + Google Calendar API)

## System Showcase

| Vapi Voice Execution | n8n Workflow Execution |
| :---: | :---: |
| ![Vapi Chat](./vapi%20chat%20view.png) | ![n8n Workflow](./n8n%20execution%20view.png) |

An automated low-latency integration bridging **Vapi.ai** voice agents with **Google Calendar** via **n8n** production webhooks. Enables real-time schedule availability checks during live voice conversations with sub-2-second response latency.
```
[User Voice Input] 
       │
       ▼
[Vapi.ai Assistant] ──(Tool Call Webhook)──▶ [n8n Production Endpoint]
                                                     │
                                            (ISO 8601 Date Parsing)
                                                     │
                                                     ▼
[Vapi Response Node] ◄──(JSON Response)─── [Google Calendar REST API]
```
## Key Engineering Highlights

* **Sub-2-Second Execution**: Engineered node processing logic to complete the full request-response cycle in ~1.9s to prevent voice AI silence timeouts.
* **ISO Timestamp Standardization**: Formatted incoming Vapi date parameters into clean ISO 8601 strings, bypassing millisecond parsing mismatches in Google Calendar API endpoints.
* **Dynamic Webhook Response**: Returned structured JSON payloads linked directly to Vapi's unique `toolCallId` to enable seamless natural language synthesis.

## Workflow Setup & Installation

1. **n8n Workflow**:
   * Import `workflow-check-availability.json` into your n8n instance.
   * Configure Google Calendar OAuth2 API credentials.
   * Activate the workflow to generate the **Production Webhook URL**.

2. **Vapi Custom Tool**:
   * Create a custom tool in Vapi with function parameters for `startTime` and `endTime`.
   * Paste the n8n Production Webhook URL into **Server Settings**.
   * Set **Server Timeout** to 20s and attach the tool to your assistant.
