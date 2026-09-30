<!--
Copyright (c) 2026 Huawei Technologies Co., Ltd.
All Rights Reserved.

SPDX-License-Identifier: Apache-2.0

   Licensed under the Apache License, Version 2.0 (the "License"); you may
   not use this file except in compliance with the License. You may obtain
   a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
   WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the
   License for the specific language governing permissions and limitations
   under the License.
-->
# Release Notes

This document is the release notes for OpenAN-v26.09.

# Introduction

OpenAN is an autonomous network open source project collection, supporting the development and deployment of telecom intelligent agents through a series of open source projects, enabling multi-vendor, cross-layer, cross-domain integration, and accelerating autonomous networks toward L4-L5. Its core vision is:

- End-to-end closed-loop autonomous network: Accelerating cross-layer, cross-domain integration and deployment of telecom-specific agents, efficient multi-agent orchestration and collaboration, enabling global operators to accelerate achieving AN L4.

- Vendor-neutral and open ecosystem: Based on industry standards (value scenario Solution Package, agent interconnection protocol, etc.), advancing vendor-neutral, industry-shared scenario-based "skills, components, knowledge, and practices," forming a telecom industry-wide collaborative ecosystem around AN, jointly improving the industry's AN level.

- Industry-led and future evolution: Driving OpenAN to become the telecom industry de facto standard, exploring integration and collaboration toward next-generation intelligent systems for AN L5.

# User Notes

OpenAN version numbering uses year and month as the version number, allowing users to understand the release time. For example, v26.06 indicates the release time is June 2026.

# Version Introduction

This version is the first release of OpenAN, with modules including registry-center, orchestration-center, A2A-T SDK (a2a-t-sdk-python, a2a-t-sdk-java), and execution engine SDKs (workflow-engine-sdk-python, workflow-engine-sdk-java).

- The main features of registry-center are shown in [Table 1](#table_registry_features). For detailed information on feature descriptions, please refer to [Registry-center User Guide](https://github.com/project-openan/registry-center/blob/main/docs/en/Registry%20Center%20User%20Guide.md).
  
- The main features of orchestration-center are shown in [Table 2](#table_orchestrate_features). For detailed information on feature descriptions, please refer to [Orchestration-center User Guide](https://github.com/project-openan/orchestration-center/blob/main/docs/en/Orchestration%20Center%20User%20Guide.md).
  
- The main features of a2a-t-sdk-python are shown in [Table 3](#table_a2at_sdk_features). For detailed information on feature descriptions, please refer to [a2a-t-sdk-python Development Guide](https://github.com/project-openan/a2a-t-sdk-python/blob/main/docs/en/developer_guide.md).
  
- The main features of a2a-t-sdk-java are shown in [Table 4](#table_a2at_java_features). For detailed information on feature descriptions, please refer to [a2a-t-sdk-java Development Guide](https://github.com/project-openan/a2a-t-sdk-java/blob/main/docs/en/developer_guide.md).
  
- The main features of the execution engine SDK (Python) are shown in [Table 5](#table_exec_engine_py_features). For detailed information on feature descriptions, please refer to [workflow-engine-sdk-python Design Notes](https://github.com/project-openan/workflow-engine-sdk-python/blob/main/DESIGN.md).
  
- The main features of the execution engine SDK (Java) are shown in [Table 6](#table_exec_engine_java_features). For detailed information on feature descriptions, please refer to [workflow-engine-sdk-java Integration Guide](https://github.com/project-openan/workflow-engine-sdk-java/blob/main/docs/en/INTEGRATION_GUIDE.md).

**Table 1** Registry-center Feature List<a id="table_registry_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="5">AgentCard Management</td>
      <td>AgentCard Registration</td>
      <td>Supports registering AgentCard information of third-party agents via REST API, including metadata such as Agent name, organization, skill description, endpoint address, etc.</td>
    </tr>
    <tr>
      <td>AgentCard Query</td>
      <td>Supports querying registered AgentCards by conditions, including full query, detail query by ID, query by name, etc.</td>
    </tr>
    <tr>
      <td>AgentCard Modification</td>
      <td>Supports modifying and updating registered AgentCard information. Only the Agent owner is allowed to perform modification operations.</td>
    </tr>
    <tr>
      <td>AgentCard Deletion</td>
      <td>Supports removing registered AgentCards from the registry-center. Only the Agent owner is allowed to perform deletion operations.</td>
    </tr>
    <tr>
      <td>Semantic Search</td>
      <td>Implements AgentCard semantic search based on LLM semantic matching and vector database: uses LLM intelligent matching by default, with optional Milvus vector search (use_vectordb=true), supporting natural language description to match target Agents.</td>
    </tr>
    <tr>
      <td rowspan="4">Agent Governance</td>
      <td>Agent Review</td>
      <td>Provides an AgentCard manual review process. Administrators can approve or reject AgentCards pending registration, ensuring the quality and compliance of registered Agents.</td>
    </tr>
    <tr>
      <td>Tag Management</td>
      <td>Supports setting custom tags for AgentCards, facilitating classification and organizational management.</td>
    </tr>
    <tr>
      <td>AgentCard Content Security</td>
      <td>Automatically identifies and intercepts AgentCards containing malicious intents during the registration phase; defaults to verifying AgentCard integrity to prevent information tampering.</td>
    </tr>
    <tr>
      <td>AgentCard Signing</td>
      <td>The registry-center digitally signs registered AgentCards, enabling receivers to verify the authenticity and integrity of AgentCard sources.</td>
    </tr>
    <tr>
      <td rowspan="2">CLI Management</td>
      <td>CLI Client</td>
      <td>Provides a command-line interface (CLI), supporting management operations such as Agent query (full/detail), review (approve/reject), and tag management (create/query/modify/delete/list), etc.</td>
    </tr>
    <tr>
      <td>CLI Secure Input</td>
      <td>Sensitive input parameters for backend command lines use interactive input to avoid sensitive parameters being recorded in system logs.</td>
    </tr>
    <tr>
      <td rowspan="5">Interface Services</td>
      <td>AgentCard Management API</td>
      <td>Provides REST interfaces for AgentCard registration, query, modification, deletion, etc., defaulting to HTTPS protocol to ensure communication security.</td>
    </tr>
    <tr>
      <td>Internal Service API</td>
      <td>Provides internal service interfaces for the upper-layer orchestration system, supporting AgentCard discovery and management under the A2A protocol.</td>
    </tr>
    <tr>
      <td>Signature Verification Public Key Download</td>
      <td>Provides interfaces for external systems to download the registry-center's signature verification public key, used to verify the authenticity of AgentCard signatures.</td>
    </tr>
    <tr>
      <td>Integration Access API</td>
      <td>Provides a dedicated integration access plane for third-party systems (/integration/v1/*, separate HTTPS port, disabled by default), supporting four authentication types: static Bearer, OAuth2 JWT, OAuth2 introspection, and mTLS, with built-in failure banning and rate limiting.</td>
    </tr>
    <tr>
      <td>Knowledge Graph API</td>
      <td>Provides a Neo4j-based knowledge graph API (/rest/v1/registry-center/knowledge-graph), supporting graph node and relationship management, batch import/export, and Cypher queries.</td>
    </tr>
    <tr>
      <td rowspan="5">Data Storage</td>
      <td>File Storage</td>
      <td>Defaults to using the local file system to store AgentCard data. Data is saved in {installation directory}/data/agentcard.json.</td>
    </tr>
    <tr>
      <td>PostgreSQL Storage</td>
      <td>Supports switching to PostgreSQL database for AgentCard data persistence, enabled through the configuration item persistence.mode=postgresql.</td>
    </tr>
    <tr>
      <td>MySQL Storage</td>
      <td>Supports switching to MySQL database for AgentCard data persistence, enabled through the configuration item persistence.mode=mysql.</td>
    </tr>
    <tr>
      <td>SQLite Storage</td>
      <td>Supports using SQLite embedded database for data persistence, enabled through the configuration item persistence.mode=sqlite, suitable for lightweight deployment scenarios.</td>
    </tr>
    <tr>
      <td>GaussDB Storage</td>
      <td>Supports switching to GaussDB database for AgentCard data persistence, enabled through the configuration item persistence.mode=gauss.</td>
    </tr>
    <tr>
      <td rowspan="3">Monitoring & Ecosystem</td>
      <td>Agent Heartbeat Detection</td>
      <td>Supports Agent heartbeat reporting and health queries (health status, history records, and SSE health event streams), with configurable failure thresholds and automatic offline deregistration, and supports hiding unhealthy Agents in query and semantic search results.</td>
    </tr>
    <tr>
      <td>Change Subscription & Broadcast</td>
      <td>Supports subscription management and version-based reconciliation change queries. AgentCard changes are reliably delivered via the event Outbox to Webhook callbacks carrying an HMAC signature header, with debounce and rate limiting configuration.</td>
    </tr>
    <tr>
      <td>Web Console</td>
      <td>Provides a React Web console (registry-center-web), supporting visual AgentCard management and heartbeat monitoring, which can run independently or be built as an OpenAN Portal plugin.</td>
    </tr>
    <tr>
      <td rowspan="7">Security Capabilities</td>
      <td>TLS Secure Communication</td>
      <td>Inter-system interactions default to HTTPS protocol, supporting TLSv1.3 and TLSv1.2 protocol versions and secure cipher suites, ensuring communication channel security.</td>
    </tr>
    <tr>
      <td>Access Control</td>
      <td>Provides authentication callback functions for custom implementation. AgentCard operations are isolated by Agent owner; only the Agent owner is allowed to modify and delete their own AgentCards.</td>
    </tr>
    <tr>
      <td>Storage Security</td>
      <td>Provides encryption/decryption callback functions for custom implementation, used to protect sensitive data storage security.</td>
    </tr>
    <tr>
      <td>Log Audit</td>
      <td>Defaults to logging to an independent log file, recording 6 key elements of critical operations; also provides log audit callback functions for custom implementation.</td>
    </tr>
    <tr>
      <td>Certificate Verification</td>
      <td>Supports mutual verification of server identity certificates and client certificates. Certificate requirements: X.509v3 format, RSA (>=3072 bits) or ECDSA (>=256 bits) key algorithm, pem encoding format.</td>
    </tr>
    <tr>
      <td>Revocation List Check</td>
      <td>Supports configuring certificate revocation lists (CRL), X.509v2 format, pem encoding, verifying whether certificates are revoked during the TLS handshake phase.</td>
    </tr>
    <tr>
      <td>Certificate Generation Tool</td>
      <td>Provides the standalone `generate_selfsign_cert.py` tool for generating self-signed certificates, for use in debugging scenarios.</td>
    </tr>
    <tr>
      <td rowspan="1">Extensibility</td>
      <td>Callback Function Reservation</td>
      <td>Reserves authentication, authorization, encryption/decryption, key management, and log audit callback function interfaces in the source code, allowing integrators to customize implementations based on their own system security infrastructure.</td>
    </tr>
  </tbody>
</table>

**Table 2** Orchestration-center Feature List<a id="table_orchestrate_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3">Workflow Orchestration</td>
      <td>Visual Orchestration</td>
      <td>Provides a graphical workflow designer, supporting Agent collaboration process design through drag-and-drop and connection, without requiring code writing.</td>
    </tr>
    <tr>
      <td>Multi-mode Generation</td>
      <td>Supports three workflow creation methods: PDF import, manual orchestration, and natural language generation, adapting to different user preferences.</td>
    </tr>
    <tr>
      <td>Intelligent Search</td>
      <td>Searches historical workflows based on natural language intent, quickly reusing existing processes to reduce repeated orchestration costs.</td>
    </tr>
    <tr>
      <td rowspan="4">Process Execution</td>
      <td>Dynamic Workflow Engine</td>
      <td>Workflow execution based on the PSOP (Plan-Specific Operation Protocol) model is driven by the execution engine SDK (workflow-exec-engine) embedded in the Host Agent, supporting multiple execution topologies such as linear, parallel, and conditional branching; the orchestration center is responsible for workflow retrieval, task dispatch, and event forwarding.</td>
    </tr>
    <tr>
      <td>Real-time Streaming Execution</td>
      <td>Real-time execution progress push via SSE (Server-Sent Events) technology, including step status, Agent output, and intermediate results, facilitating frontend display and issue localization.</td>
    </tr>
    <tr>
      <td>Execution Record Management</td>
      <td>Automatically records the complete process of each workflow execution, supporting execution result queries and historical traceback by execution ID.</td>
    </tr>
    <tr>
      <td>Sandbox Validation</td>
      <td>Performs static validation (topology/capability/reference checks) on saved workflows (PSOP) first, then simulates execution using stub Agents and generates a structured validation report without requiring real Agents to be online; reports are stored in the data/workflow_storage/sandbox/ directory.</td>
    </tr>
    <tr>
      <td rowspan="2">A2A-T Negotiation</td>
      <td>Negotiation-T Negotiation</td>
      <td>Conducts multi-round Negotiation-T negotiation interactions with the Agent side through negotiation callbacks of the execution engine SDK embedded in the Host Agent. Negotiation activation and decisions are owned by the host, with a default maximum of 3 negotiation exchanges.</td>
    </tr>
    <tr>
      <td>Negotiation Context Transmission</td>
      <td>Negotiation context is transmitted between Agents through the Negotiation-T extension content carried in Task.metadata, supporting multi-round negotiation processes.</td>
    </tr>
    <tr>
      <td rowspan="2">Interface Services</td>
      <td>Internal REST API</td>
      <td>Provides internal APIs for the frontend designer (/rest/v1/orchestrate/*), supporting frontend interactions such as workflow design, saving, and execution.</td>
    </tr>
    <tr>
      <td>External REST API</td>
      <td>Provides public APIs for external systems (/api/v1/*), supporting SOP orchestration, intent orchestration, automatic execution, specified execution, Agent query, result query, and other functions.</td>
    </tr>
    <tr>
      <td rowspan="2">Data Storage</td>
      <td>File Storage</td>
      <td>Defaults to using the local file system to store workflow data (PSOP, PreFlow, execution records). Data is saved in the {installation directory}/data/workflow_storage directory.</td>
    </tr>
    <tr>
      <td>PostgreSQL Storage</td>
      <td>Supports switching to PostgreSQL database for workflow data persistence, enabled through the configuration item persistence_mode=postgresql, with automatic table creation on startup.</td>
    </tr>
    <tr>
      <td rowspan="2">Secure Communication</td>
      <td>TLS Transport</td>
      <td>Supports the HTTPS protocol (enable_https configuration, disabled by default in the shipped configuration and can be enabled), using TLSv1.3 and TLSv1.2 protocol versions, with mutual authentication and certificate revocation list (CRL) checks, ensuring communication channel security.</td>
    </tr>
    <tr>
      <td>Certificate Verification</td>
      <td>Supports configuring server identity certificate and client certificate verification. Certificate format is X.509v3, supporting RSA (>=3072 bits) and ECDSA (>=256 bits) key algorithms.</td>
    </tr>
  </tbody>
</table>

**Table 3** a2a-t-sdk-python Feature List<a id="table_a2at_sdk_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">Task Prompt Generation</td>
      <td>Scenario Identification</td>
      <td>Performs scenario identification on user input based on LLM, automatically matching predefined telecom operation scenarios (such as alarm subscription, fault diagnosis, energy-saving optimization, dedicated line complaints, etc.), supporting Chinese and English bilingual scenario definitions.</td>
    </tr>
    <tr>
      <td>Slot Extraction</td>
      <td>Extracts structured slot information from user input based on LLM. Each scenario corresponds to an independent JSON Schema slot definition, supporting mandatory/optional slot validation.</td>
    </tr>
    <tr>
      <td>Template Rendering</td>
      <td>Supports task prompt rendering based on scenario templates, using <code>{{slot}}</code> placeholders to fill extracted slot values into Markdown templates, generating standardized task prompts.</td>
    </tr>
    <tr>
      <td>Metadata Formatting</td>
      <td>Task prompts adopt YAML front-matter format, including metadata such as scenario_code, language, description, etc., facilitating server-side parsing and validation.</td>
    </tr>
    <tr>
      <td rowspan="4">Task Prompt Compliance Validation</td>
      <td>Scenario Parsing</td>
      <td>Automatically parses the front-matter metadata of the task prompt, identifies scenario_code, and loads the corresponding slot Schema and scenario template.</td>
    </tr>
    <tr>
      <td>Slot Validation</td>
      <td>Performs structural validation on extracted slot values based on JSON Schema, ensuring slot value types, formats, and mandatory constraints all conform to scenario definitions.</td>
    </tr>
    <tr>
      <td>Semantic Validation</td>
      <td>Performs semantic-level rationality validation on slot values based on LLM, detecting logical contradictions or values that do not conform to business semantics. Validation is optional.</td>
    </tr>
    <tr>
      <td>Compliance Pipeline</td>
      <td>The server provides a complete compliance validation pipeline (scenario parsing → slot extraction → Schema validation → semantic validation). The pipeline is fixedly assembled and uniformly invoked through the check_task_prompt entry point of A2ATServer.</td>
    </tr>
    <tr>
      <td rowspan="3">Multi-round Negotiation</td>
      <td>Information Negotiation</td>
      <td>Supports information supplement negotiation between Agents. When task prompt information is incomplete, the server can initiate an information negotiation request to obtain missing information.</td>
    </tr>
    <tr>
      <td>Feasibility Negotiation</td>
      <td>Supports feasibility confirmation negotiation between Agents, evaluating feasibility before task execution to avoid ineffective execution of infeasible tasks.</td>
    </tr>
    <tr>
      <td>Target Negotiation</td>
      <td>Supports task goal alignment negotiation between Agents. The execution phase begins after task goals and constraints are clarified; the target negotiation message includes built-in alignment and clarification (alignment_and_clarification) fields.</td>
    </tr>
    <tr>
      <td rowspan="3">Negotiation State Management</td>
      <td>State Machine Driven</td>
      <td>The current negotiation is a stateless content-driven API, with negotiation state carried round by round in message metadata; the early state machine API (IN_PROGRESS, AGREED, REJECTED state transitions) is marked as deprecated since 1.1.0.</td>
    </tr>
    <tr>
      <td>Context Transmission</td>
      <td>Negotiation context supports serialization and deserialization, can be transmitted between Agents through Task.metadata, ensuring continuity of multi-round negotiation states.</td>
    </tr>
    <tr>
      <td>State Storage</td>
      <td>Provides the NegotiationStateStore protocol interface with a built-in in-memory storage implementation, supporting negotiation state access by session ID; this state storage API is marked as deprecated since 1.1.0.</td>
    </tr>
    <tr>
      <td rowspan="4">LLM Runtime</td>
      <td>Multi-mode Invocation</td>
      <td>Supports the structured output invocation mode, generating structured responses constrained by JSON Schema to meet requirements of scenarios such as scenario identification and slot extraction.</td>
    </tr>
    <tr>
      <td>Adapter Factory</td>
      <td>Provides the LLMClientFactory factory class, supporting registration of custom LLM client adapters. Currently pre-registers the openai (OpenAI-compatible protocol) adapter.</td>
    </tr>
    <tr>
      <td>Session Management</td>
      <td>Built-in session history management, supporting configuration of history window size (A2AT_LLM_HISTORY_WINDOW), maximum total sessions, and per-Provider session limit to prevent memory overflow.</td>
    </tr>
    <tr>
      <td>Extensible</td>
      <td>LLM adapters support dynamic registration. All model services compatible with OpenAI protocol can be connected through configuration without modifying SDK source code.</td>
    </tr>
    <tr>
      <td rowspan="3">Prompt Resource Management</td>
      <td>Multi-language Resources</td>
      <td>Prompt resources are organized by language directories, supporting Chinese (zh-CN) and English (en-US) bilingual, covering scenario definitions, slot Schemas, templates, and system/user prompts.</td>
    </tr>
    <tr>
      <td>Custom Resource Directory</td>
      <td>Supports specifying a custom resource root directory through the A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR configuration item; in local_file mode, business resources use local-first overlay semantics, with locally missing resources automatically falling back to in-package copies (one warning per path), while LLM prompts and error messages always come from in-package resources.</td>
    </tr>
    <tr>
      <td>Standardized Organization</td>
      <td>Prompt resources are organized using a standardized directory structure: scenarios/{lang}/scenarios.json (scenario definitions), slots/{scenario}/{lang}/slot.json (slot Schemas), templates/{protocol type}/{level}/{scenario}/{action}/v1/{lang}/template.md (templates), with built-in negotiation vocabulary (negotiation-vocabulary) and error code (errors) resources.</td>
    </tr>
    <tr>
      <td rowspan="2">Configuration Management</td>
      <td>Environment Variable Configuration</td>
      <td>All configuration items are managed through .env files, supporting configuration categories such as prompt runtime, input limits, LLM runtime, and negotiation. The full configuration template is available in the env.example file at the repository root.</td>
    </tr>
    <tr>
      <td>Configuration Layering</td>
      <td>Supports layered configuration between package-level defaults and user-defined custom configurations. Users only need to override configuration items they want to modify, with the rest using default values.</td>
    </tr>
  </tbody>
</table>

**Table 4** a2a-t-sdk-java Feature List<a id="table_a2at_java_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="5">Task Prompt Generation</td>
      <td>Scenario Identification</td>
      <td>Performs scenario identification on user input based on LLM, automatically matching predefined telecom operation scenarios (such as alarm subscription, fault diagnosis, energy-saving optimization, dedicated line complaints, etc.), supporting Chinese and English bilingual scenario definitions.</td>
    </tr>
    <tr>
      <td>Slot Extraction</td>
      <td>Extracts structured slot information from user input based on LLM. Each scenario corresponds to an independent JSON Schema slot definition (<code>ClientSlotJsonSchema</code>), supporting mandatory/optional slot validation.</td>
    </tr>
    <tr>
      <td>Template Rendering</td>
      <td>Supports task prompt rendering based on scenario templates, using <code>{{variable}}</code> placeholders to fill extracted slot values into Markdown templates, generating standardized task prompts. Template URIs are expressed through <code>StandardTemplates</code>/<code>TemplateUri</code> constants and string URIs, organized by protocol type, level, scenario, action, version, and language.</td>
    </tr>
    <tr>
      <td>Metadata Formatting</td>
      <td>Task prompts adopt YAML front-matter format, including metadata such as scenario_code, language, description, etc., facilitating server-side parsing and validation.</td>
    </tr>
    <tr>
      <td>Orchestrator Pattern</td>
      <td>Client prompt generation is driven by the <code>ClientPromptGenerationOrchestrator</code> orchestrator, providing default implementation <code>DefaultClientPromptGenerationOrchestrator</code>, supporting custom replacement of each stage component through the Builder pattern.</td>
    </tr>
    <tr>
      <td rowspan="5">Task Prompt Compliance Validation</td>
      <td>Scenario Parsing</td>
      <td>Automatically parses the front-matter metadata of the task prompt, identifies scenario_code, and loads the corresponding slot Schema and scenario template. Provides the ServerPromptMetadataExtractor interface and an LLM parsing implementation (<code>LlmBackedPromptMetadataExtractor</code>).</td>
    </tr>
    <tr>
      <td>Slot Validation</td>
      <td>Performs structural validation on extracted slot values based on JSON Schema, ensuring slot value types, formats, and mandatory constraints all conform to scenario definitions.</td>
    </tr>
    <tr>
      <td>Semantic Validation</td>
      <td>Supports LLM semantic validation (<code>LlmBackedPromptSemanticValidator</code>) and a built-in default semantic validator, extended from the <code>ServerPromptSemanticValidator</code> interface, detecting logical contradictions or values that do not conform to business semantics.</td>
    </tr>
    <tr>
      <td>Compliance Pipeline</td>
      <td>The server provides a compliance validation pipeline (input length threshold → metadata parsing → semantic validation), driven by the <code>ServerPromptComplianceOrchestrator</code> orchestrator, with the compliance validation switch controlled through configuration items.</td>
    </tr>
    <tr>
      <td>Compliance Result Model</td>
      <td>Provides <code>PromptComplianceResult</code> and <code>PromptComplianceFailure</code> structured result models, clearly recording validation failure stages and error codes, facilitating issue localization.</td>
    </tr>
    <tr>
      <td rowspan="3">Multi-round Negotiation</td>
      <td>Information Negotiation</td>
      <td>Supports information supplement negotiation between Agents. When task prompt information is incomplete, the server can initiate an information negotiation request to obtain missing information.</td>
    </tr>
    <tr>
      <td>Feasibility Negotiation</td>
      <td>Supports feasibility confirmation negotiation between Agents, evaluating feasibility before task execution to avoid ineffective execution of infeasible tasks.</td>
    </tr>
    <tr>
      <td>Target Negotiation</td>
      <td>Supports task goal alignment negotiation between Agents. The execution phase begins after task goals and constraints are clarified; the target negotiation message includes built-in alignment and clarification (alignment_and_clarification) fields.</td>
    </tr>
    <tr>
      <td rowspan="4">Negotiation State Management</td>
      <td>State Machine Driven</td>
      <td>Each negotiation type is driven by a state machine, supporting three state transitions: IN_PROGRESS, AGREED, REJECTED, automatically tracking negotiation rounds and limiting maximum rounds to prevent infinite loops. Throws <code>NegotiationStateException</code> when rounds do not match.</td>
    </tr>
    <tr>
      <td>Context Transmission</td>
      <td>Negotiation context follows A2A-T protocol extension URI convention, carried in Task.metadata through the <code>https://projects.tmforum.org/a2aproject/telecommunication/extensions/Negotiation-T/v1</code> key, supporting serialization and deserialization, ensuring multi-round negotiation state continuity.</td>
    </tr>
    <tr>
      <td>State Storage</td>
      <td>Provides <code>NegotiationStore</code> interface. Currently has built-in <code>InMemoryNegotiationStore</code> in-memory implementation, supporting negotiation state access by session ID, with extensible persistence implementation.</td>
    </tr>
    <tr>
      <td>Handler Registration Pattern</td>
      <td>Provides <code>NegotiationHandler</code> core handler, supporting registration of negotiation handlers and state storage by negotiation type through the Builder pattern. Client and server share negotiation orchestration logic through <code>RoleBoundNegotiationOrchestrator</code>.</td>
    </tr>
    <tr>
      <td rowspan="4">LLM Runtime</td>
      <td>Adapter Architecture</td>
      <td>Provides the <code>LLMClient</code> interface and <code>providers.OpenAIClient</code> implementation, based on OpenAI Java SDK (v4.36.0) compatible with all OpenAI protocol model services, registered and switched through <code>LLMClientFactory</code>.</td>
    </tr>
    <tr>
      <td>Structured Generation</td>
      <td>Supports structured output constrained by JSON Schema, used for LLM invocation scenarios requiring structured responses such as scenario identification and slot extraction.</td>
    </tr>
    <tr>
      <td>Session Management</td>
      <td>Built-in session history management, supporting configuration of history window size (A2AT_LLM_HISTORY_WINDOW), maximum total sessions, and per-Provider session limit to prevent memory overflow.</td>
    </tr>
    <tr>
      <td>Local Rule Engine</td>
      <td>In addition to the OpenAI-compatible adapter, provides <code>local_rule</code> provider type, supporting rule-based local scenario identification and slot extraction, suitable for deterministic scenarios without LLM requirements.</td>
    </tr>
    <tr>
      <td rowspan="3">Prompt Resource Management</td>
      <td>Multi-language Resources</td>
      <td>Prompt resources are organized by language directories, supporting Chinese (zh-CN) and English (en-US) bilingual, covering scenario definitions, slot Schemas, templates, and system/user prompts, with built-in telecom scenario resources such as ran-energy-saving (energy-saving optimization).</td>
    </tr>
    <tr>
      <td>Multi-source Loading</td>
      <td>Supports Classpath resource loading (<code>ClasspathPromptResourceLoader</code>) and local file system loading; in local_file mode, locally missing business resources automatically fall back to in-package Classpath copies (overlay semantics, one warning per path). Users can specify custom resource directories through configuration.</td>
    </tr>
    <tr>
      <td>Standardized Organization</td>
      <td>Prompt resources are organized using a standardized directory structure: scenarios/{lang}/scenarios.json (scenario definitions), slots/{scenario}/{lang}/slot.json (slot Schemas), templates/{protocol type}/{level}/{scenario}/{action}/v1/{lang}/template.md (templates), with built-in negotiation vocabulary (negotiation-vocabulary) and error code (errors) resources.</td>
    </tr>
    <tr>
      <td rowspan="3">Configuration Management</td>
      <td>Environment Variable Configuration</td>
      <td>All configuration items are managed through .env files. The SDK does not automatically discover .env files; the path must be explicitly provided by the caller. Supports four major categories of configuration: prompt runtime, compliance validation, LLM runtime, and negotiation.</td>
    </tr>
    <tr>
      <td>Structured Configuration Model</td>
      <td>Provides Record type configuration models such as <code>A2ATConfig</code>, <code>PromptRuntimeConfig</code>, <code>LlmConfig</code>, <code>NegotiationConfig</code>, <code>PromptComplianceConfig</code>, etc., which are type-safe and immutable.</td>
    </tr>
    <tr>
      <td>BOM Version Management</td>
      <td>Provides <code>a2a-t-bom</code> Bill of Materials module. Integrators can uniformly manage versions of all a2a-t modules by importing the BOM, avoiding version conflicts.</td>
    </tr>
    <tr>
      <td rowspan="2">Sample Integration</td>
      <td>End-to-end Sample</td>
      <td>Provides <code>a2a-t-sample</code> module, demonstrating the complete client-server interaction process, integrating A2A Java SDK (v1.0.0.Beta1) for HTTP transport, including complete scenarios such as AgentCard registration, task prompt generation and validation, SSE streaming event push, etc.</td>
    </tr>
    <tr>
      <td>Builder Construction Pattern</td>
      <td>Both client <code>A2ATClient</code> and server <code>A2ATServer</code> support custom assembly of each component through Builder pattern (<code>DefaultA2ATClientBuilder</code>, <code>DefaultA2ATServerBuilder</code>), facilitating integrators to replace implementations as needed.</td>
    </tr>
  </tbody>
</table>

**Table 5** Execution Engine SDK (Python) Feature List<a id="table_exec_engine_py_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="3">Workflow Execution</td>
      <td>DAG Workflow Execution</td>
      <td>Embedded workflow execution engine for host agents, responsible for workflow DAG traversal, A2A message encapsulation, task and session association, and remote task waiting; supports parallel scheduling, self-loop steps, and conditional branching topologies.</td>
    </tr>
    <tr>
      <td>Conditional Routing</td>
      <td>Non-empty conditional edges are evaluated edge by edge through the on_route callback, allowing a node to activate 0 to N successor edges; empty conditional edges pass by default, and successor steps are scheduled only after all conditional evaluations for the same node are completed.</td>
    </tr>
    <tr>
      <td>Upstream Result Aggregation</td>
      <td>Controls the aggregation scope of upstream results through context_from (default: direct predecessors; ["*"]: all ancestors; []: no passing; specified step names: only aggregate the corresponding steps). Callbacks can obtain ordered upstream outputs grouped by step, along with source information.</td>
    </tr>
    <tr>
      <td rowspan="2">Protocol Extensions</td>
      <td>Negotiation-T Negotiation Loop</td>
      <td>Responsible for the Negotiation-T negotiation loop and lifecycle. Negotiation activation and decisions are owned by the host through ControlPoint callbacks, while the engine handles A2A-T extension declaration and protocol envelopes.</td>
    </tr>
    <tr>
      <td>Independent Protocol Operations</td>
      <td>Provides independent protocol operations for Authorization-T authorization and Notification-T notification subscription, using independent transports and lifecycles; they do not act as workflow DAG nodes, and authorization or subscription failures do not automatically block the workflow.</td>
    </tr>
    <tr>
      <td rowspan="2">Remote Task Management</td>
      <td>Task Management Interface</td>
      <td>Provides standard A2A task interfaces including get_task, list_tasks, cancel_task, and subscribe_to_task, supporting remote task waiting and cancellation; task cancellation and Negotiation-T abort are two independent operations.</td>
    </tr>
    <tr>
      <td>SSE Subscription & Heartbeat</td>
      <td>Client SSE stream normalization and transport activity observation. Streams containing only heartbeats are not misjudged as disconnected, ensuring long-lived subscriptions and streaming event reception.</td>
    </tr>
    <tr>
      <td rowspan="2">Authentication & Transport Security</td>
      <td>Authentication & TLS</td>
      <td>Supports credential configuration declared in AgentCard, custom AuthProvider, custom CA, mTLS client certificates, and CRL checks; server certificates are verified by default, and startup fails when certificates are missing or invalid (fail-closed).</td>
    </tr>
    <tr>
      <td>Concurrency & Lifecycle</td>
      <td>A single WorkflowEngineClient is bound to only one workflow execution at a time; concurrent executions require creating separate client instances.</td>
    </tr>
  </tbody>
</table>

**Table 6** Execution Engine SDK (Java) Feature List<a id="table_exec_engine_java_features" href="#"></a>
<table border="0">
  <thead>
    <tr>
      <th>Category</th>
      <th>Feature</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="2">Workflow Execution</td>
      <td>DAG Workflow Execution</td>
      <td>Supports DAG workflow execution with parallel dispatch, self-loop steps, and conditional routing. Layered architecture: ExecutePsop.Builder (event stream and lifecycle), WorkflowExecutor (DAG traversal and ControlPoint scheduling), WorkflowEngineClient/A2ATransport (A2A sending, authentication, and SSE normalization), and ControlPoint (host business decisions).</td>
    </tr>
    <tr>
      <td>Callback Contract</td>
      <td>ControlPoint provides four content-neutral callbacks: onTask, onSelfTask, onRoute, and onNegotiation. Callbacks return the final MessageContent or a complete ReceivedMessage, supporting local multi-output TaskResult and explicit NegotiationReply.Send/Stop.</td>
    </tr>
    <tr>
      <td rowspan="3">Protocol Extensions</td>
      <td>Negotiation-T Negotiation</td>
      <td>The host activates negotiation through MessageContent.withExtension. The engine mirrors the extension to message.extensions and the A2A-Extensions header, and verifies that the target AgentCard has declared the extension; negotiation fails fast if not activated. Supports taskless bare-message Propose and bounded best-effort cancellation upon negotiation termination.</td>
    </tr>
    <tr>
      <td>Independent Protocol Operations</td>
      <td>Authorization-T authorization and Notification-T long-lived subscriptions are triggered independently of the workflow causal chain; authorization or subscription failures do not automatically block the workflow, and subscriptions remain open until host-defined termination events or explicit cancellation.</td>
    </tr>
    <tr>
      <td>fail-closed Protocol Semantics</td>
      <td>A2A-T templates, slot Schemas, normalized URIs, and validation results are the authoritative source. Protocol generation or validation failure means failure; bare text is never sent as a degraded fallback.</td>
    </tr>
    <tr>
      <td rowspan="3">Transport & Security</td>
      <td>Multi-protocol Transport</td>
      <td>REST, JSON-RPC, and gRPC transports are automatically selected according to the AgentCard declaration.</td>
    </tr>
    <tr>
      <td>Authentication & TLS</td>
      <td>Supports custom CA, mTLS client certificates, and CRL checks, with built-in Bearer token login TTL caching and AES-256-GCM encrypted credential storage.</td>
    </tr>
    <tr>
      <td>SSE Heartbeat & Polling Fallback</td>
      <td>The server sends SSE heartbeats on message streams and task subscription streams (heartbeat-interval-seconds, 15 seconds by default). After stream interruption, it falls back to polling at taskPollIntervalMillis (20 seconds by default) until the task reaches a final state.</td>
    </tr>
    <tr>
      <td rowspan="1">Observability</td>
      <td>Protocol Logging & Desensitization</td>
      <td>Outputs real HTTP/JSON-RPC boundary logs and gRPC metadata/protobuf view logs. DEBUG level carries message bodies by default and enforces desensitization of sensitive fields.</td>
    </tr>
    <tr>
      <td rowspan="1">Spring Integration</td>
      <td>spring-boot-starter</td>
      <td>Provides A2A server auto-configuration (A2AAutoConfiguration, A2AController), declaring AgentCard, path prefixes, timeouts, and thread pools through the a2at.server.* configuration prefix, and automatically registering host-declared TaskAuthorizationProvider.</td>
    </tr>
  </tbody>
</table>

# Version Compatibility

## Registry-center

### Deliverables

The initial release of registry-center only provides source code, without binary installation packages. Source code can be obtained from the [OpenAN community registry-center repository](https://github.com/project-openan/registry-center).

**Table 1** Registry-center v1.0.0 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Source Code</td>
      <td>registry-center source code</td>
      <td>Complete source code of registry-center, including AgentCard management, CLI client, Web console, knowledge graph API, security capabilities, and other modules</td>
    </tr>
  </tbody>
</table>

> **Note:**
>
> - The initial release only delivers source code; deliverables do not include build engineering or binary installation packages.
> - Users need to complete build and deployment installation themselves. After installation, file and directory permissions must be minimized (file permission 400, directory permission 700, executable .sh file permission 500).
> - Only files under {installation directory}/etc require writable permissions; all other files have only readable permissions.

### Operating System Version Compatibility

**Table 2** Registry-center v1.0.0 Supported Scenarios

| Operating System | Version | Architecture | Applicability |
|---------|------|------|----------|
| openEuler | 22.03 LTS SP3 | x86_64, ARM64 | Recommended for production |
| Ubuntu | 22.04 | x86_64, ARM64 | Available for production |
| Windows | Windows 10/11 | x86_64 | Development and debugging only |

> **Note:**
>
> - This project must run on a Linux operating system, supporting IPv4 network environments.
> - Windows environment is only for development and debugging; production deployment is not supported.
> - Only single-instance deployment is supported. It must be used as an internal system, cannot be exposed to the public network, and cannot be deployed as a cloud service.

### Runtime Environment Version Compatibility

**Table 3** Registry-center v1.0.0 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| Python | >= 3.12 | Registry-center service runtime environment |
| PostgreSQL (optional) | >= 12 | Data persistence database; not required under file or SQLite storage mode |
| MySQL / GaussDB (optional) | - | Data persistence database, used by mysql/gauss storage modes |
| SQLite | Built-in | Embedded database, used by the sqlite storage mode, no additional deployment required |
| Neo4j (optional) | >= 5.0 | Graph database required by the knowledge graph API |
| Milvus (optional) | >= 2.6 | Vector database required by the semantic search vector retrieval mode (use_vectordb=true) |

> **Note:**
>
> - The registry-center service is started via `python -m agent_registry.start`, defaulting to listening on `127.0.0.1:5000`.
> - IP and port can be modified as needed. The configuration file is {installation directory}/etc/conf/server.conf.
> - Defaults to file storage mode (persistence.mode=file), with data saved in {installation directory}/data/agentcard.json. Supports switching to postgresql, mysql, sqlite, or gauss storage modes. The configuration file is {installation directory}/etc/conf/persistence.conf, and invalid storage modes will fail with an error during startup validation.
> - Semantic search uses LLM intelligent matching by default (no Milvus deployment required). When use_vectordb=true is configured, it switches to Milvus vector search; if semantic search is not used, Milvus does not need to be deployed.

### Core Dependency Version Compatibility

**Table 4** Registry-center v1.0.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| a2a-sdk[signing] | >= 1.0.0a1 | A2A protocol implementation and AgentCard signing capability |
| fastapi | >= 0.115.11 | REST API framework |
| uvicorn | >= 0.47.0 | ASGI server |
| loguru | >= 0.7.3 | Logging |
| cryptography | ~= 46.0.5 | Cryptographic algorithm support |
| openai | >= 2.26.0 | LLM client (semantic search intelligent matching) |
| pymilvus | ~= 2.6.12 | Milvus vector database client (semantic search) |
| psycopg2-binary | >= 2.9.10 | PostgreSQL database driver |
| PyMySQL | >= 1.1.0, < 2.0 | MySQL database driver |
| DBUtils | >= 3.0, < 4.0 | Database connection pool (MySQL storage) |
| neo4j | >= 5.0.0 | Knowledge graph API graph database driver |
| PyJWT | ~= 2.10.1 | JWT token processing |
| requests | ~= 2.32.3 | HTTP client |
| httpx | ~= 0.28.1 | Async HTTP client |
| environs | ~= 15.0.1 | Environment variable parsing |
| python-dotenv | >= 1.1.0, < 2 | Environment variable loading |
| PyYAML | >= 6.0.3 | Model configuration file (models.yaml) parsing |
| limits | ~= 4.0.0 | Rate limiting |
| starlette | ~= 0.50.0 | ASGI framework core |

> **Note:**
>
> - See requirements.txt for the complete dependency list.
> - a2a-sdk[signing] provides AgentCard signing and verification capabilities. The registry-center digitally signs registered AgentCards.
> - The registry-center itself does not provide login authentication, authorization, user management, encryption/decryption, or key management capabilities. These security infrastructure must be provided by the integrator's system.
> - Certificate requirements: Identity certificate server.cer (required, pem encoding, X.509v3 format), private key server_key.pem (required, pem encoding), private key password cert_pwd (required, stored in ciphertext), trust certificate trust.cer (required when verify_client=true), revocation list revocationlist.crl (optional).
> - When the AgentCard signing capability is enabled, the signing private key directory etc/sign_cert (jwk_private_key_path) and the signing certificate (jwk_cert_path) must also be configured.
> - Certificate verification failure will cause process startup failure; certificate changes require process restart to take effect.

## Orchestration-center

### Deliverables

The initial release of orchestration-center only provides source code, without binary installation packages. Source code can be obtained from the [OpenAN community orchestration-center repository](https://github.com/project-openan/orchestration-center/tree/main).

**Table 1** Orchestration-center v1.0.0 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Source Code</td>
      <td>orchestration-center source code</td>
      <td>Complete source code of orchestration-center, including backend orchestration engine, frontend workflow designer, and sample Agents</td>
    </tr>
  </tbody>
</table>

> **Note:**
>
> - The initial release only delivers source code; deliverables do not include build engineering or binary installation packages.
> - Users need to complete build and deployment installation themselves.

### Operating System Version Compatibility

**Table 2** Orchestration-center v1.0.0 Supported Scenarios

| Operating System | Version | Architecture | Applicability |
|---------|------|------|----------|
| openEuler | 22.03 LTS SP3 | x86_64, ARM64 | Recommended for production |
| Ubuntu | 22.04 | x86_64, ARM64 | Available for production |
| Windows | Windows 10/11 | x86_64 | Development and debugging only |

> **Note:**
>
> - Production environments must be deployed on Linux operating systems.
> - Windows environment is only for development and debugging; production deployment is not supported.
> - Mixed deployment of different OS within the same cluster is not supported.

### Runtime Environment Version Compatibility

**Table 3** Orchestration-center v1.0.0 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| Python | >= 3.12 | Backend orchestration engine runtime environment |
| Node.js | >= 20.19 | Frontend workflow designer runtime environment |
| PostgreSQL (optional) | >= 12 | Data persistence database; not required under file storage mode |

> **Note:**
>
> - The backend service is started via `python -m orchestrate.start`, defaulting to listening on `127.0.0.1:5001`.
> - The frontend service is started via `npm run dev`, defaulting to listening on `localhost:3003`.
> - Sample Agents are started via `python -m samples.start_agents_server`, as optional components, but workflow execution depends on sample Agents providing A2A Agent endpoints.
> - Defaults to file storage mode (persistence_mode=file), with data saved in the {installation directory}/data/workflow_storage directory. To switch to PostgreSQL, configure persistence_mode=postgresql and modify the database connection information in {installation directory}/etc/conf/db_config.json.

### Core Dependency Version Compatibility

**Table 4** Orchestration-center v1.0.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| a2a-t-sdk | >= 1.0.9, < 2 | A2A-T protocol negotiation capability |
| workflow-exec-engine | >= 0.0.9, < 0.1 | Workflow execution engine SDK (embedded execution in the Host Agent) |
| a2a-sdk[http-server,grpc] | >= 1.1.2, < 2 | A2A protocol implementation (http-server + grpc) |
| fastapi | >= 0.135.1 | REST API framework |
| uvicorn | >= 0.42 | ASGI server |
| pydantic | >= 2.12.5 | Data model validation |
| openai | >= 2.26.0 | LLM invocation |
| loguru | >= 0.7.3 | Logging |
| PyYAML | >= 6.0.3 | YAML parsing |
| pymupdf | Not pinned | PDF document parsing |
| limits | >= 5.8.0 | Rate limiting |
| python-multipart | >= 0.0.24 | File upload parsing |
| psycopg2-binary | >= 2.9.10 | PostgreSQL database driver |
| cryptography | >= 41.0.0 | Cryptographic algorithm support |
| bcrypt | >= 4.0 | Password hashing |

> **Note:**
>
> - See requirements.txt for the complete dependency list.
> - The negotiation configuration of the A2A-T SDK is provided through the `A2AT_*` environment variables in the `.env` file at the orchestration center root directory (such as A2AT_LLM_PROVIDER, A2AT_LLM_MODEL, A2AT_LLM_API_KEY, etc.), independent of the orchestration center's own LLM configuration (etc/config/models.yaml); the legacy llm_config.json configuration can be migrated using `python -m scripts.migrate_legacy_llm_json`.

## a2a-t-sdk-python

### Deliverables

a2a-t-sdk-python has been published to PyPI (package name a2a-t-sdk), and is also available as source code. Source code can be obtained from the [OpenAN community a2a-t-sdk-python repository](https://github.com/project-openan/a2a-t-sdk-python).

**Table 1** a2a-t-sdk-python v1.1.0 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>PyPI Artifact</td>
      <td>a2a-t-sdk</td>
      <td>Python package (wheel and sdist), installable online via pip or uv</td>
    </tr>
    <tr>
      <td>Source Code</td>
      <td>a2a-t-sdk-python source code</td>
      <td>Complete source code of A2A-T SDK, including client task prompt generation, server compliance validation, multi-round negotiation, LLM runtime, and prompt resource management modules</td>
    </tr>
  </tbody>
</table>


> **Note:**
>
> - Online installation: `pip install a2a-t-sdk`; for offline or development scenarios, build and install from source via `uv sync --dev` or `pip install -e .`.
> - This version has been published to PyPI (currently 1.x); interfaces and resource organization may be adjusted with subsequent version evolution.

### Operating System Version Compatibility

**Table 2** a2a-t-sdk-python v1.1.0 Supported Scenarios

| Operating System | Version | Architecture | Applicability |
|---------|------|------|----------|
| openEuler | 22.03 LTS SP3 | x86_64, ARM64 | Recommended for production |
| Ubuntu | 22.04 / 24.04 | x86_64, ARM64 | Available for production |
| macOS | 13+ | x86_64, Apple Silicon | Development and debugging |
| Windows | Windows 10/11 | x86_64 | Development and debugging only |

> **Note:**
>
> - a2a-t-sdk-python is a pure Python package with no platform-native dependencies, theoretically supporting all platforms where Python 3.12+ can run.
> - Windows and macOS environments are only for development and debugging; production deployment is not supported.
> - This SDK itself does not provide HTTP services; the transport layer and deployment environment must be provided by the integrator's business system.

### Runtime Environment Version Compatibility

**Table 3** a2a-t-sdk-python v1.1.0 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| Python | >= 3.12 | SDK runtime environment |
| uv (recommended) / pip | uv >= 0.4 / pip >= 23 | Package management and build tools |
| LLM service | OpenAI protocol compatible | Dependency for LLM invocation scenarios such as task prompt generation, slot extraction, semantic validation |

> **Note:**
>
> - It is recommended to use uv for package management, installing dependencies via `uv sync --dev`; `pip install -e .` can also be used for installation.
> - LLM service is an SDK feature dependency. LLM-related features of the SDK such as scenario identification, slot extraction, semantic validation, and negotiation interaction all depend on external LLM services; samples can automatically degrade to a scripted mock LLM when no API Key is configured (for demonstration only).
> - The built-in openai adapter (compatible with OpenAI protocol) is used. The LLM provider, model, API key, and base URL are configured through `A2AT_LLM_PROVIDER`, `A2AT_LLM_MODEL`, `A2AT_LLM_API_KEY`, and `A2AT_LLM_BASE_URL` respectively (all required), and can connect to any model service compatible with the OpenAI protocol (such as DeepSeek, Tongyi Qianwen, etc.).
> - The configuration file template is available in `env.example` at the repository root. Copy it to a `.env` file and modify as needed when using.

### Core Dependency Version Compatibility

**Table 4** a2a-t-sdk-python v1.1.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| openai | Not pinned | OpenAI-compatible protocol LLM client, used for LLM invocations such as scenario identification, slot extraction, semantic validation, negotiation interaction |
| jsonschema | >= 4.23.0 | JSON Schema validation, used for structural validation of slot values on the server side |
| httpx | >= 0.23.0, < 1 | Async HTTP client |
| python-dotenv | >= 1.1.0 | Environment variable loading, used to read SDK configuration from .env files |

> **Note:**
>
> - See `pyproject.toml` for the complete dependency list.
> - The openai library is the core dependency for LLM invocation, supporting multiple model service backends through its compatible protocol.
> - jsonschema is used for the slot Schema validation stage in the server-side compliance validation pipeline.
> - python-dotenv is responsible for loading configuration from .env files at SDK startup. All configuration items are injected through environment variables.
> - Development dependencies include: pytest (>= 8.0.0, testing framework), ruff (>= 0.3.0, code checking and formatting), mypy (>= 1.9.0, type checking).

### Configuration Item Compatibility

**Table 5** a2a-t-sdk-python v1.1.0 Configuration Item Description

| Configuration Category | Configuration Item | Default Value | Description |
|---------|-------|-------|------|
| Prompt Runtime | A2AT_LANGUAGE | en-US | Prompt resource language, supporting zh-CN, en-US |
| Prompt Runtime | A2AT_PROMPT_SOURCE_TYPE | packaged | Prompt resource source type (packaged/local_file; default packaged since 1.1.0) |
| Prompt Runtime | A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR | (empty) | Custom resource root directory, used only in local_file mode; fails fast when unset or the path does not exist |
| Input Limits | A2AT_INPUT_TEXT_MAX_CHARS | 16384 | Maximum character count for free-text input; fails fast when exceeded (error code input.text_too_long) |
| LLM Runtime | A2AT_LLM_PROVIDER | (empty, required) | LLM provider name; currently built-in openai |
| LLM Runtime | A2AT_LLM_MODEL | (empty, required) | Model name |
| LLM Runtime | A2AT_LLM_API_KEY | (empty, required) | API key |
| LLM Runtime | A2AT_LLM_BASE_URL | (empty) | API base URL |
| LLM Runtime | A2AT_LLM_MAX_TOKENS | 2000 | Maximum token count |
| LLM Runtime | A2AT_LLM_TEMPERATURE | 0 | Sampling temperature |
| LLM Runtime | A2AT_LLM_TIMEOUT_SECONDS | 60 | Request timeout (seconds) |
| LLM Runtime | A2AT_LLM_HISTORY_WINDOW | 10 | Conversation history window message count |
| LLM Runtime | A2AT_LLM_REASONING_EFFORT | (empty) | Reasoning effort level (none/minimal/low/medium/high/xhigh); skipped when empty |
| LLM Runtime | A2AT_LLM_SSL_VERIFY | true | Whether to verify the LLM endpoint TLS certificate chain and hostname; disabling is allowed only for short-term use in controlled environments |
| LLM Runtime | A2AT_LLM_MAX_ATTEMPTS | 3 | Maximum attempts for retryable LLM steps (range 1-10) |
| LLM Runtime | A2AT_LLM_DETAIL_LOG_ENABLED | false | Whether to print complete LLM request/response messages (may expose sensitive information, for debugging only) |
| LLM Runtime | A2AT_LLM_SESSION_MAX_TOTAL | 300 | Maximum total sessions |
| LLM Runtime | A2AT_LLM_SESSION_MAX_PER_PROVIDER | 100 | Maximum sessions per Provider |
| Negotiation | A2AT_NEGOTIATION_STATE_STORE_TYPE | in_memory | Negotiation state storage type (for legacy state machine demonstration, deprecated) |

> **Note:**
>
> - All configuration items are managed through .env files. See `env.example` at the repository root for the configuration template.
> - A2AT_LLM_PROVIDER, A2AT_LLM_MODEL, and A2AT_LLM_API_KEY are required. The SDK throws LLMConfigError when they are not configured.
> - A2AT_LLM_BASE_URL can be replaced with any OpenAI protocol-compatible service endpoint. Connecting to different model services only requires modifying this configuration and the corresponding API_KEY.
> - A2AT_LLM_SSL_VERIFY enables TLS certificate verification by default. Disabling it is allowed only for short-term use in controlled environments; importing a trusted CA is recommended.
> - When A2AT_LLM_DETAIL_LOG_ENABLED is enabled, complete LLM interaction messages are output (may expose sensitive information and consume significant log space). It is for debugging only and should remain disabled in production.

### Protocol Standard Compatibility

**Table 6** Protocol Standards Followed by a2a-t-sdk-python v1.1.0

| Standard | Version | Description |
|-----|------|------|
| IG1453 A Structured Prompt of Agent to Agent Protocol for Telecoms (A2AT) | v1.0.0 | A2A-T structured prompt protocol standard published by TM Forum |
| IG1453 Agent to Agent Protocol for Telecoms (A2AT) | v2.0.0 | A2A-T protocol standard published by TM Forum, covering negotiation extensions |

> **Note:**
>
> - a2a-t-sdk-python is the reference implementation SDK for the A2A-T protocol standard. Task prompt format and negotiation process follow the above protocol standards.
> - The A2A-T protocol is the telecom domain extension of the A2A (Agent-to-Agent) protocol, standardized and published by TM Forum.


## a2a-t-sdk-java

### Deliverables

a2a-t-sdk-java has been published to Maven Central (groupId: net.openan.a2a-t.sdk), and is also available as source code. Source code can be obtained from the [OpenAN community a2a-t-sdk-java repository](https://github.com/project-openan/a2a-t-sdk-java).

**Table 1** a2a-t-sdk-java v1.1.1 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Source Code</td>
      <td>a2a-t-java source code</td>
      <td>Complete source code of a2a-t-sdk-java, including 10 Maven modules: core model, resource management, LLM runtime, prompt processing, negotiation runtime, client facade, server facade, accuracy validation corpus, and sample integration</td>
    </tr>
    <tr>
      <td>Maven Artifact</td>
      <td>a2a-t-bom</td>
      <td>Bill of Materials, for unified management of A2A-T module version dependencies</td>
    </tr>
    <tr>
      <td>Maven Artifact</td>
      <td>a2a-t-client</td>
      <td>Client SDK module, providing A2ATClient facade and task prompt generation capability</td>
    </tr>
    <tr>
      <td>Maven Artifact</td>
      <td>a2a-t-server</td>
      <td>Server SDK module, providing A2ATServer facade and task prompt compliance validation capability</td>
    </tr>
    <tr>
      <td>Maven Artifact</td>
      <td>a2a-t-core and other base modules</td>
      <td>Core model, resource management, LLM runtime, prompt processing, and negotiation runtime modules (a2a-t-core/resources/llm/prompt/negotiation), published together with the SDK</td>
    </tr>
  </tbody>
</table>

> **Note:**
>
> - SDK artifacts have been published to Maven Central (groupId net.openan.a2a-t.sdk). Integrators can import the SDK directly through Maven dependencies, or build from source via `mvn -DskipTests package`.
> - This version (1.1.1) has been published to Maven Central; interfaces and module organization may be adjusted with subsequent version evolution.

### Operating System Version Compatibility

**Table 2** a2a-t-sdk-java v1.1.1 Supported Scenarios

| Operating System | Version | Architecture | Applicability |
|---------|------|------|----------|
| openEuler | 22.03 LTS SP3 | x86_64, ARM64 | Recommended for production |
| Ubuntu | 22.04 / 24.04 | x86_64, ARM64 | Available for production |
| macOS | 13+ | x86_64, Apple Silicon | Development and debugging |
| Windows | Windows 10/11 | x86_64 | Development and debugging only |

> **Note:**
>
> - a2a-t-sdk-java is a pure Java SDK with no platform-native dependencies, theoretically supporting all platforms where JDK 17+ can run.
> - Windows and macOS environments are only for development and debugging; production deployment is not supported.
> - This SDK itself does not provide HTTP services; the transport layer and deployment environment must be provided by the integrator's business system.

### Runtime Environment Version Compatibility

**Table 3** a2a-t-sdk-java v1.1.1 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| JDK | >= 17 | SDK runtime environment |
| Maven | >= 3.8 | Build and dependency management tool |
| LLM service | OpenAI protocol compatible | Dependency for LLM invocation scenarios such as scenario identification, slot extraction, semantic validation |

> **Note:**
>
> - JDK 17 is the minimum version requirement. LTS versions (JDK 17 or JDK 21) are recommended.
> - The build command is `mvn -DskipTests package`; run tests using `mvn test`.
> - LLM service is a required dependency. All LLM-related features of the SDK (scenario identification, slot extraction, semantic validation, negotiation interaction) depend on external LLM services.
> - The openai_compatible adapter is pre-registered by default. Model services compatible with OpenAI protocol (such as OpenAI, Azure OpenAI, DeepSeek, Tongyi Qianwen, etc.) can be connected through `A2AT_LLM_BASE_URL` and `A2AT_LLM_API_KEY` configuration.
> - The configuration file template is available at `package_data/env.example`. Copy it to a `.env` file and modify as needed when using. The SDK does not automatically discover .env files; the path must be explicitly provided by the caller.

### Core Dependency Version Compatibility

**Table 4** a2a-t-sdk-java v1.1.1 Core Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| Lombok | 1.18.38 | Code generation (annotation processor, provided scope) |
| Jackson Databind | 2.20.1 | JSON serialization and deserialization |
| Jackson Annotations | 2.20 | Jackson annotation support |
| Jackson Core | 2.20.1 | Jackson core parser |
| OpenAI Java SDK (okhttp) | 4.36.0 | OpenAI-compatible protocol LLM client |
| OpenAI Java Core | 4.36.0 | OpenAI Java SDK core module |
| JUnit Jupiter | 5.10.2 | Unit testing framework |

> **Note:**
>
> - See each module's `pom.xml` for the complete dependency list.
> - Lombok is a compile-time dependency (provided scope) and is not required at runtime.
> - OpenAI Java SDK is the core dependency for LLM invocation, supporting multiple model service backends through its compatible protocol.
> - A2A Java SDK (v1.0.0.Beta1) is only used for the `a2a-t-sample` sample module and is not a required SDK runtime dependency.

### Module Version Compatibility

**Table 5** a2a-t-sdk-java v1.1.1 Module List

| Module | ArtifactId | Purpose | Dependent Modules |
|------|-----------|------|----------|
| BOM | a2a-t-bom | Unified version management; integrators manage all module versions by importing BOM | None |
| Core | a2a-t-core | Shared abstractions and value types (OperationResult, PromptMessage, configuration models, exception hierarchy, etc.) | None |
| Resources | a2a-t-resources | Packaged prompt resources and loaders (scenario definitions, slot Schemas, templates, system prompts) | a2a-t-core |
| LLM | a2a-t-llm | LLM Provider integration (LLMClient interface, OpenAI-compatible client, factory registration) | a2a-t-core |
| Prompt | a2a-t-prompt | Prompt templates, rendering, Schema validation (scenario identification, slot extraction, template rendering, semantic validation) | a2a-t-core, a2a-t-resources, a2a-t-llm |
| Negotiation | a2a-t-negotiation | Negotiation workflow and state processing (information/feasibility/target negotiation types, state machine, storage interface, Handler registration) | a2a-t-core |
| Client | a2a-t-client | Client facade (A2ATClient), providing task prompt generation and client negotiation capability | a2a-t-core, a2a-t-llm, a2a-t-prompt, a2a-t-negotiation |
| Server | a2a-t-server | Server facade (A2ATServer), providing task prompt compliance validation and server negotiation capability | a2a-t-core, a2a-t-llm, a2a-t-prompt, a2a-t-negotiation |
| Corpus Validation | a2a-t-corpus | Data-driven Negotiation-T/Task-T accuracy validation corpus (JSON cases, LLM invocation transcripts, and latency/token metrics) | a2a-t-client, a2a-t-server, a2a-t-negotiation, a2a-t-resources |
| Sample | a2a-t-sample | End-to-end sample, integrating A2A Java SDK to demonstrate complete client-server interaction process | a2a-t-client, a2a-t-server |

> **Note:**
>
> - Most integration scenarios only need to import `a2a-t-client` or `a2a-t-server`; Maven will automatically transitively depend on the required other modules.
> - Importing version management through BOM can avoid module version inconsistency issues:
>   ```xml
>   <dependencyManagement>
>       <dependencies>
>           <dependency>
>               <groupId>net.openan.a2a-t.sdk</groupId>
>               <artifactId>a2a-t-bom</artifactId>
>               <version>1.1.1</version>
>               <type>pom</type>
>               <scope>import</scope>
>           </dependency>
>       </dependencies>
>   </dependencyManagement>
>   ```
> - `a2a-t-corpus` is an accuracy validation corpus module. It is not an SDK runtime dependency and is not included in the Maven Central publishing scope.
> - `a2a-t-sample` is a sample module, only for development reference.

### Configuration Item Compatibility

**Table 6** a2a-t-sdk-java v1.1.1 Configuration Item Description

| Configuration Category | Configuration Item | Default Value | Description |
|---------|-------|-------|------|
| Prompt Runtime | A2AT_LANGUAGE | en-US | Prompt resource language, supporting zh-CN, en-US |
| Prompt Runtime | A2AT_PROMPT_SOURCE_TYPE | classpath | Prompt resource source type (classpath/local_file) |
| Prompt Runtime | A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR | (empty) | Custom resource root directory, required only in local_file mode; assembly fails fast when unset or the path does not exist |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_ENABLED | false | Whether to enable the server-side compliance validation pipeline (input length threshold → metadata parsing → semantic validation) |
| Input Limits | A2AT_INPUT_TEXT_MAX_CHARS | 16384 | Maximum character count for free-text input; fails fast when exceeded (error code input.text_too_long) |
| LLM Runtime | A2AT_LLM_PROVIDER | (empty, required) | LLM provider name; currently built-in openai; local_rule is supported only by the negotiation generation path |
| LLM Runtime | A2AT_LLM_MODEL | (empty, required) | Model name |
| LLM Runtime | A2AT_LLM_API_KEY | (empty, required) | API key |
| LLM Runtime | A2AT_LLM_BASE_URL | (empty) | API base URL |
| LLM Runtime | A2AT_LLM_MAX_TOKENS | 2000 | Maximum token count |
| LLM Runtime | A2AT_LLM_TEMPERATURE | 0 | Sampling temperature |
| LLM Runtime | A2AT_LLM_TIMEOUT_SECONDS | 60 | Request timeout (seconds) |
| LLM Runtime | A2AT_LLM_HISTORY_WINDOW | 10 | Conversation history window message count |
| LLM Runtime | A2AT_LLM_REASONING_EFFORT | (empty) | Reasoning effort level (none/minimal/low/medium/high/xhigh); skipped when empty |
| LLM Runtime | A2AT_LLM_DISABLE_SYSTEM_PROXY | false | Whether to bypass the system HTTP proxy for LLM invocations |
| LLM Runtime | A2AT_LLM_SSL_VERIFY | true | Whether to verify the LLM endpoint TLS certificate chain and hostname; disabling is allowed only for short-term use in controlled environments |
| LLM Runtime | A2AT_LLM_MAX_ATTEMPTS | 3 | Maximum attempts for retryable LLM steps (range 1-10) |
| LLM Runtime | A2AT_LLM_DETAIL_LOG_ENABLED | false | Whether to print complete LLM request/response messages (may expose sensitive information, for debugging only) |
| LLM Runtime | A2AT_LLM_SESSION_MAX_TOTAL | 300 | Maximum total sessions |
| LLM Runtime | A2AT_LLM_SESSION_MAX_PER_PROVIDER | 100 | Maximum sessions per Provider |
| Negotiation | A2AT_NEGOTIATION_STATE_STORE_TYPE | in_memory | Negotiation state storage type |

> **Note:**
>
> - All configuration items are managed through .env files. See `env.example` at the repository root for the configuration template.
> - The SDK does not automatically discover .env files; the caller must explicitly provide the .env file path via `new A2ATClient(Path envPath)` or `new A2ATServer(Path envPath)`.
> - A2AT_LLM_PROVIDER, A2AT_LLM_MODEL, and A2AT_LLM_API_KEY are required. SDK assembly fails when they are not configured.
> - A2AT_LLM_BASE_URL can be replaced with any OpenAI protocol-compatible service endpoint. Connecting to different model services only requires modifying this configuration and the corresponding API_KEY.
> - A2AT_PROMPT_COMPLIANCE_ENABLED is disabled by default. When enabled, the server executes the compliance validation pipeline.
> - A2AT_LLM_SSL_VERIFY enables TLS certificate verification by default. Disabling it is allowed only for short-term use in controlled environments; importing a trusted CA is recommended. When A2AT_LLM_DETAIL_LOG_ENABLED is enabled, complete LLM interaction messages are output (may expose sensitive information and consume significant log space). It is for debugging only and should remain disabled in production.

### Protocol Standard Compatibility

**Table 7** Protocol Standards Followed by a2a-t-sdk-java v1.1.1

| Standard | Version | Description |
|-----|------|------|
| IG1453 A Structured Prompt of Agent to Agent Protocol for Telecoms (A2AT) | v1.0.0 | A2A-T structured prompt protocol standard published by TM Forum |
| IG1453 Agent to Agent Protocol for Telecoms (A2AT) | v2.0.0 | A2A-T protocol standard published by TM Forum, covering negotiation extensions |

> **Note:**
>
> - a2a-t-sdk-java is the Java reference implementation SDK for the A2A-T protocol standard. Task prompt format and negotiation process follow the above protocol standards.
> - The A2A-T protocol is the telecom domain extension of the A2A (Agent-to-Agent) protocol, standardized and published by TM Forum.
> - Negotiation context transmission follows the A2A project telecom extension URI convention, carried in Task.metadata through the `https://projects.tmforum.org/a2aproject/telecommunication/extensions/Negotiation-T/v1` key.


## Execution Engine SDK (Python)

### Deliverables

The execution engine SDK (Python) has been published to PyPI (package name workflow-exec-engine), and is also available as source code. Source code can be obtained from the [OpenAN community execution engine SDK Python repository](https://github.com/project-openan/workflow-engine-sdk-python).

**Table 1** Execution Engine SDK (Python) v0.1.0 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>PyPI Artifact</td>
      <td>workflow-exec-engine</td>
      <td>Embedded workflow execution engine SDK for host agents (wheel and sdist), installable via `python -m pip install workflow-exec-engine`</td>
    </tr>
    <tr>
      <td>Source Code</td>
      <td>workflow-engine-sdk-python source code</td>
      <td>Complete source code of the execution engine SDK, including the engine core, examples, and documents such as DESIGN.md and DEVELOPER_GUIDE.md</td>
    </tr>
  </tbody>
</table>

### Runtime Environment Version Compatibility

**Table 2** Execution Engine SDK (Python) v0.1.0 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| Python | >= 3.12 | SDK runtime environment |

> **Note:**
>
> - The execution engine SDK is a library that runs within the host Agent process, with no independent service port or daemon.
> - The engine directly uses A2A-T core metadata types for protocol identification. It does not call LLMs itself, nor does it generate or validate Task-T, Negotiation-T, Authorization-T, or Notification-T business content on behalf of the host; this content is completed by the host calling a2a-t-sdk.

### Core Dependency Version Compatibility

**Table 3** Execution Engine SDK (Python) v0.1.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| a2a-sdk | >= 1.1.2, < 2 | A2A protocol implementation |
| a2a-t-sdk | >= 1.0.9, < 2 | A2A-T core protocol metadata (protocol identification) |
| httpx | >= 0.27.0 | Async HTTP client |
| loguru | >= 0.7.0 | Logging |
| protobuf | >= 4.25.0 | gRPC/protobuf protocol support |
| cryptography | >= 42.0.0 | TLS and encryption support |
| packaging | >= 23.0 | Version parsing |

> **Note:**
>
> - See pyproject.toml for the complete dependency list.
> - When the host performs A2A-T content generation and semantic validation, it needs to separately call the content APIs of a2a-t-sdk and configure LLM services.

## Execution Engine SDK (Java)

### Deliverables

The execution engine SDK (Java) has been published to Maven Central (groupId: net.openan.workflow.sdk), and is also available as source code. Source code can be obtained from the [OpenAN community execution engine SDK Java repository](https://github.com/project-openan/workflow-engine-sdk-java).

**Table 1** Execution Engine SDK (Java) v0.1.1 Deliverable List

<table border="0">
  <thead>
    <tr>
      <th>Delivery Form</th>
      <th>Name</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Maven Artifact</td>
      <td>workflow-engine</td>
      <td>Core SDK of the multi-agent workflow execution engine embedded in the host Agent</td>
    </tr>
    <tr>
      <td>Maven Artifact</td>
      <td>spring-boot-starter</td>
      <td>Spring Boot server auto-configuration module (A2A server auto-assembly)</td>
    </tr>
    <tr>
      <td>Source Code</td>
      <td>workflow-engine-sdk-java source code</td>
      <td>Complete source code of the execution engine SDK, including the engine core, samples, and bilingual docs/zh and docs/en documents</td>
    </tr>
  </tbody>
</table>

> **Note:**
>
> - The publishing scope includes the parent pom (workflow-engine-parent), workflow-engine, and spring-boot-starter; the samples module is not included in the release deployment, and sample source code can be obtained from the repository.
> - This SDK has no independent BOM module. Integrators can directly depend on workflow-engine or spring-boot-starter.

### Runtime Environment Version Compatibility

**Table 2** Execution Engine SDK (Java) v0.1.1 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| JDK | >= 17 | SDK runtime environment |
| Maven | >= 3.6 | Build and dependency management tool |

> **Note:**
>
> - The execution engine SDK is a library that runs within the host Agent process, with no independent service port.
> - The engine itself does not call LLMs (the sample LlmHelper is located only in the samples module); A2A-T content generation, Schema validation, and LLM invocation are completed by the host through a2a-t-client/a2a-t-server.

### Core Dependency Version Compatibility

**Table 3** Execution Engine SDK (Java) v0.1.1 Core Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| org.a2aproject.sdk:a2a-java-sdk-bom | 1.2.0.Final | A2A Java SDK (protocol implementation) |
| net.openan.a2a-t.sdk:a2a-t-core | 1.1.1 | A2A-T protocol metadata and core types |
| spring-boot | 3.3.10 | Spring Boot foundation (spring-boot-starter only) |
| Jackson | 2.22.0 | JSON serialization and deserialization |
| gRPC | 1.81.0 | gRPC transport support |
| Log4j2 / SLF4J | 2.24.3 / 2.0.18 | Logging |
| protobuf-java-util | 4.35.0 | protobuf JSON runtime (aligned with the A2A Java SDK REST transport) |
| Lombok | 1.18.38 | Code generation (compile-time dependency) |

> **Note:**
>
> - See each module's pom.xml for the complete dependency list.
> - When the host performs A2A-T content generation, add a2a-t-client as needed; server Agents performing content validation add a2a-t-server as needed (both 1.1.1, published to Maven Central).


# CVE Vulnerabilities

This version is the first release of OpenAN, with no CVE disclosed vulnerabilities.

# Source Code

OpenAN repository address: <https://github.com/project-openan>

# Contributing

As an OpenAN user, you can assist the OpenAN community in various ways. For methods of contributing to the community, please refer to the [Contributing to OpenAN](https://github.com/project-openan/.github/blob/main/CONTRIBUTING.md).

# Acknowledgments

We sincerely thank all members who participated in and assisted the OpenAN project. Your dedication has made the successful release of this version possible and provides possibilities for OpenAN's continued development.