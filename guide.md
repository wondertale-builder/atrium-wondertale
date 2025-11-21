# Atrium CRM: Development Instructions

## 1. Introduction

This document provides a detailed breakdown of the tasks required to build the Atrium CRM application, as specified in the Product Requirements Document (PRD). The tasks are organized hierarchically, from major features to granular sub-tasks, to guide the development process.

## 2. Technology Stack

The following technologies will be used for this project:

*   **Runtime:** Bun
*   **Framework:** Next.js
*   **Authentication:** Clerk
*   **Language:** React
*   **API:** tRPC
*   **ORM:** Drizzle
*   **Server:** Fastify
*   **UI:** React Flow, shadcn/ui, Tailwind CSS
*   **Database:** Neon DB
*   **Email:** Resend

## 3. Project Setup

*   **Initialize Project:**
    *   Set up a new Next.js project with Bun.
    *   Integrate Tailwind CSS for styling.
    *   Set up shadcn/ui for UI components.
*   **Database Setup:**
    *   Set up a new Neon DB project.
    *   Configure Drizzle ORM and connect it to the Neon DB.
*   **Authentication Setup:**
    *   Set up a new Clerk project.
    *   Integrate Clerk for user authentication in the Next.js app.
*   **API Setup:**
    *   Integrate tRPC for typesafe API routes.
    *   Set up Fastify for the server.

## 4. Core Data Management

*   **Object & Field Management:**
    *   Create database schemas for standard objects (Contacts, Companies, Tasks, Notes).
    *   Implement functionality to create, edit, and delete custom objects.
    *   Implement support for various field types: text, number, boolean, picklist, multi-select, date, owner, lookup.
*   **Relationships:**
    *   Implement one-to-many and many-to-many relationships between objects.
*   **Views & Filtering:**
    *   Implement filtering, sorting, and grouping of records.
    *   Implement functionality to save and share views.
*   **Email Integration:**
    *   Integrate with Gmail/Outlook using OAuth (IMAP/SMTP).
    *   Implement automatic contact creation from inbound emails.
*   **Data Sovereignty:**
    *   Implement region selection and data residency policies.
    *   Implement audit logs for data changes.

## 5. AI Assistants & Integrations

*   **Conversational AI:**
    *   Integrate with an AI/LLM provider (e.g., OpenAI).
    *   Develop a natural language interface for interacting with the CRM data.
*   **Calendar Integration:**
    *   Integrate with Google Calendar using OAuth.
    *   Ingest events, track meetings, and associate them with contacts.
*   **AI Sequence Generator:**
    *   Develop a feature to generate multi-step outreach sequences based on persona, stage, and goals.
*   **Scoring Models:**
    *   Implement configurable scoring models for contacts and companies.
*   **Data Enrichment:**
    *   Integrate with third-party data enrichment providers (e.g., Clearbit, Apollo).
*   **Analytics & Reporting AI:**
    *   Develop natural language queries for analyzing dashboards and reports.
*   **Message Personalization:**
    *   Implement AI-powered suggestions for email snippets and call scripts.
*   **Opportunity Surfacing:**
    *   Develop a feature to monitor signals and propose next actions.
*   **Task Automation:**
    *   Implement AI-powered task creation based on conversations and workflow events.

## 6. Workflows & Automation

*   **Visual Workflow Builder:**
    *   Implement a visual builder (using React Flow) to define triggers, conditions, and actions.
*   **Outbound Sequencer:**
    *   Develop a sequencer for outbound campaigns with manual and automated steps.
*   **Reporting & Dashboards:**
    *   Implement custom report building and scheduling.
    *   Develop a drag-and-drop dashboard with various widgets.

## 7. Collaboration & Templates

*   **User Roles & Permissions:**
    *   Implement user roles (Admin, Manager, Member, Viewer).
    *   Implement role-based access control (RBAC).
*   **Team Collaboration:**
    *   Implement the ability to invite users via email and assign roles.
    *   Implement @mentions in notes and tasks.
    *   Implement real-time editing for shared views and documents.
*   **Template Library:**
    *   Develop a template library for sequences, workflows, tasks, notes, and emails.
    *   Implement AI-powered template suggestions.

## 8. Platform Features & Extensibility

*   **Interaction Tracking:**
    *   Implement a centralized timeline for each contact and company.
*   **Security:**
    *   Implement encryption at rest and in transit.
    *   Implement SSO/SAML/OAuth for secure authentication.
*   **Token Purchase:**
    *   Implement a billing portal for purchasing AI tokens/credits.
*   **API & Webhooks:**
    *   Develop REST and GraphQL APIs with OAuth2 authentication.
    *   Implement webhooks for real-time data updates.

## 9. Bonus Features

*   **Chrome Extension:**
    *   Develop a Chrome extension to capture contact and company data from LinkedIn and Gmail.
*   **Knowledge Base Import (RAG):**
    *   Implement a feature to upload documents to create a knowledge base.
    *   Implement AI-assisted document modifications.

## 10. Non-Functional Requirements

*   **Performance:**
    *   Optimize page load times to be <2s for 95% of page loads.
    *   Optimize AI responses to be <5s for standard queries.
*   **Scalability:**
    *   Ensure the application can support 100k+ records per object and 10M+ stored emails.
*   **Reliability:**
    *   Aim for 99.9% uptime.
*   **Security & Compliance:**
    *   Work towards SOC 2 Type II compliance.
    *   Ensure GDPR-ready with data residency options.

## 11. Deployment & DevOps

*   **Infrastructure as Code (IaC):**
    *   Use a tool like Terraform or Pulumi to manage infrastructure.
*   **CI/CD:**
    *   Set up a CI/CD pipeline for automated testing and deployment.
*   **Monitoring & Logging:**
    *   Integrate with a monitoring and logging service to track application health and performance.
