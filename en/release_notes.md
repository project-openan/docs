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

This document is the release notes for OpenAN-v26.06.

# Introduction

OpenAN is an autonomous network open source project collection, supporting the development and deployment of telecom intelligent agents through a series of open source projects, enabling multi-vendor, cross-layer, cross-domain integration, and accelerating autonomous networks toward L4-L5. Its core vision is:

- End-to-end closed-loop autonomous network: Accelerating cross-layer, cross-domain integration and deployment of telecom-specific agents, efficient multi-agent orchestration and collaboration, enabling global operators to accelerate achieving AN L4.

- Vendor-neutral and open ecosystem: Based on industry standards (value scenario Solution Package, agent interconnection protocol, etc.), advancing vendor-neutral, industry-shared scenario-based "skills, components, knowledge, and practices," forming a telecom industry-wide collaborative ecosystem around AN, jointly improving the industry's AN level.

- Industry-led and future evolution: Driving OpenAN to become the telecom industry de facto standard, exploring integration and collaboration toward next-generation intelligent systems for AN L5.

# User Notes

OpenAN version numbering uses year and month as the version number, allowing users to understand the release time. For example, v26.06 indicates the release time is June 2026.

# Version Introduction

This version is the first release of OpenAN, with modules including registry-center, orchestration-center, A2A-T SDK (a2a-t-sdk-python, a2a-t-sdk-java).

- The main features of registry-center are shown in [Table 1](#table_registry_features). For detailed information on feature descriptions, please refer to [Registry-center User Guide](https://github.com/project-openan/registry-center/blob/main/docs/en/Registry%20Center%20User%20Guide.md).
  
- The main features of orchestration-center are shown in [Table 2](#table_orchestrate_features). For detailed information on feature descriptions, please refer to [Orchestration-center User Guide](https://github.com/project-openan/orchestration-center/blob/main/docs/en/Orchestration%20Center%20User%20Guide.md).
  
- The main features of a2a-t-sdk-python are shown in [Table 3](#table_a2at_sdk_features). For detailed information on feature descriptions, please refer to [a2a-t-sdk-python User Guide](https://github.com/project-openan/a2a-t-sdk-python/blob/main/docs/en/user_guide.md).
  
- The main features of a2a-t-sdk-java are shown in [Table 4](#table_a2at_java_features). For detailed information on feature descriptions, please refer to [a2a-t-sdk-java User Guide](https://github.com/project-openan/a2a-t-sdk-java/blob/main/docs/en/user_guide.md).

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
      <td>Implements AgentCard semantic search based on Milvus vector database, supporting natural language description to match target Agents.</td>
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
      <td>Provides a command-line interface (CLI), supporting management operations such as Agent query (full/detail), review (approve/reject), tag setting, etc.</td>
    </tr>
    <tr>
      <td>CLI Secure Input</td>
      <td>Sensitive input parameters for backend command lines use interactive input to avoid sensitive parameters being recorded in system logs.</td>
    </tr>
    <tr>
      <td rowspan="3">Interface Services</td>
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
      <td rowspan="3">Data Storage</td>
      <td>File Storage</td>
      <td>Defaults to using the local file system to store AgentCard data. Data is saved in {installation directory}/data/agentcard.json.</td>
    </tr>
    <tr>
      <td>PostgreSQL Storage</td>
      <td>Supports switching to PostgreSQL database for AgentCard data persistence, enabled through the configuration item persistence_mode=postgresql.</td>
    </tr>
    <tr>
      <td>SQLite Storage</td>
      <td>Supports using SQLite embedded database for data persistence (in development), enabled through the configuration item persistence_mode=sqlite, suitable for lightweight deployment scenarios.</td>
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
      <td rowspan="3">Process Execution</td>
      <td>Dynamic Workflow Engine</td>
      <td>Execution engine driven by the PSOP (Plan-Specific Operation Protocol) model, supporting multiple execution topologies such as linear, parallel, and conditional branching.</td>
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
      <td rowspan="2">A2A-T Negotiation</td>
      <td>Fulfillment Negotiation</td>
      <td>Integrates a2a-t-sdk's fulfillment negotiation capability. The orchestration side and Agent side conduct multi-round negotiation interactions before task execution, with negotiation context carried through Task.metadata.</td>
    </tr>
    <tr>
      <td>Negotiation Context Transmission</td>
      <td>The orchestration side automatically parses negotiationContext in the metadata returned by the Agent, supporting negotiation state persistence and multi-round negotiation processes.</td>
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
      <td>Supports enabling HTTPS protocol, using TLSv1.3 and TLSv1.2 protocol versions, ensuring communication channel security.</td>
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
      <td rowspan="5">Task Prompt Compliance Validation</td>
      <td>Guardrail Check</td>
      <td>After receiving a task prompt, the server first performs security guardrail checks, identifying and intercepting prompts containing malicious intents to ensure interaction security. Currently provides noop (pass-through) implementation, with AWS Bedrock and Azure Content Safety extension interfaces reserved.</td>
    </tr>
    <tr>
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
      <td>The server provides a complete compliance validation pipeline (guardrail → scenario parsing → slot extraction → Schema validation → semantic validation), with each stage configurable for on-demand enabling/disabling.</td>
    </tr>
    <tr>
      <td rowspan="4">Multi-round Negotiation</td>
      <td>Information Negotiation</td>
      <td>Supports information supplement negotiation between Agents. When task prompt information is incomplete, the server can initiate an information negotiation request to obtain missing information.</td>
    </tr>
    <tr>
      <td>Clarification Negotiation</td>
      <td>Supports requirement clarification negotiation between Agents. When task intent is ambiguous or unclear, specific requirements are clarified through multi-round interactions.</td>
    </tr>
    <tr>
      <td>Feasibility Negotiation</td>
      <td>Supports feasibility confirmation negotiation between Agents, evaluating feasibility before task execution to avoid ineffective execution of infeasible tasks.</td>
    </tr>
    <tr>
      <td>Fulfillment Negotiation</td>
      <td>Supports task execution detail negotiation between Agents, negotiating task execution plans, timing, resources, and other details. After reaching agreement, enters the execution phase.</td>
    </tr>
    <tr>
      <td rowspan="3">Negotiation State Management</td>
      <td>State Machine Driven</td>
      <td>Each negotiation type is driven by a state machine, supporting three state transitions: IN_PROGRESS, AGREED, REJECTED, automatically tracking negotiation rounds and limiting maximum rounds to prevent infinite loops.</td>
    </tr>
    <tr>
      <td>Context Transmission</td>
      <td>Negotiation context supports serialization and deserialization, can be transmitted between Agents through Task.metadata, ensuring continuity of multi-round negotiation states.</td>
    </tr>
    <tr>
      <td>State Storage</td>
      <td>Provides NegotiationStateStore protocol interface. Currently has built-in in-memory storage implementation, supporting negotiation state access by session ID.</td>
    </tr>
    <tr>
      <td rowspan="4">LLM Runtime</td>
      <td>Multi-mode Invocation</td>
      <td>Supports three LLM invocation modes: single completion (complete), conversation with session history (chat), and structured output (structured), meeting different scenario requirements.</td>
    </tr>
    <tr>
      <td>Adapter Factory</td>
      <td>Provides LLMAdapterFactory factory class, supporting direct adapter registration and composite registration (transport + payload_builder + response_parser). Currently pre-registers deepseek (OpenAI-compatible protocol) adapter.</td>
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
      <td>Supports specifying a custom resource root directory through the A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR configuration item, loading custom scenarios, slots, and templates, with in-package resources as fallback.</td>
    </tr>
    <tr>
      <td>Standardized Organization</td>
      <td>Prompt resources are organized using a standardized directory structure: scenarios/{lang}/scenarios.json (scenario definitions), slots/{scenario}/{lang}/slot.json (slot Schemas), templates/{scenario}/{lang}/template.md (templates), prompts/{action}/{lang}/ (system/user prompts).</td>
    </tr>
    <tr>
      <td rowspan="2">Configuration Management</td>
      <td>Environment Variable Configuration</td>
      <td>All configuration items are managed through .env files, supporting four major categories of configuration: prompt runtime, compliance validation, LLM runtime, and negotiation, with an env.example template file provided.</td>
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
      <td>Supports task prompt rendering based on scenario templates, using <code>{{variable}}</code> placeholders to fill extracted slot values into Markdown templates, generating standardized task prompts. Templates are organized in two levels: L0 base templates (Task-T, Notification-T) and L1 scenario templates.</td>
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
      <td rowspan="6">Task Prompt Compliance Validation</td>
      <td>Guardrail Check</td>
      <td>After receiving a task prompt, the server first performs security guardrail checks, identifying and intercepting prompts containing malicious intents to ensure interaction security. Provides <code>ServerPromptGuardrail</code> extension interface and <code>NoopServerPromptGuardrail</code> default pass-through implementation, with AWS Bedrock and Azure Content Safety external policy endpoint configurations reserved.</td>
    </tr>
    <tr>
      <td>Scenario Parsing</td>
      <td>Automatically parses the front-matter metadata of the task prompt, identifies scenario_code, and loads the corresponding slot Schema and scenario template. Supports two strategies: LLM parsing (<code>LlmBackedPromptMetadataExtractor</code>) and template matching parsing (<code>TemplateMatchingPromptMetadataExtractor</code>).</td>
    </tr>
    <tr>
      <td>Slot Validation</td>
      <td>Performs structural validation on extracted slot values based on JSON Schema, ensuring slot value types, formats, and mandatory constraints all conform to scenario definitions.</td>
    </tr>
    <tr>
      <td>Semantic Validation</td>
      <td>Supports two semantic validation strategies: LLM semantic validation (<code>LlmBackedPromptSemanticValidator</code>) and template round-trip validation (<code>TemplateRoundTripPromptSemanticValidator</code>), detecting logical contradictions or values that do not conform to business semantics.</td>
    </tr>
    <tr>
      <td>Compliance Pipeline</td>
      <td>The server provides a complete compliance validation pipeline (guardrail → scenario parsing → slot extraction → Schema validation → semantic validation), driven by the <code>ServerPromptComplianceOrchestrator</code> orchestrator, with each stage configurable for on-demand enabling/disabling.</td>
    </tr>
    <tr>
      <td>Compliance Result Model</td>
      <td>Provides <code>PromptComplianceResult</code> and <code>PromptComplianceFailure</code> structured result models, clearly recording validation failure stages and error codes, facilitating issue localization.</td>
    </tr>
    <tr>
      <td rowspan="4">Multi-round Negotiation</td>
      <td>Information Negotiation</td>
      <td>Supports information supplement negotiation between Agents. When task prompt information is incomplete, the server can initiate an information negotiation request to obtain missing information.</td>
    </tr>
    <tr>
      <td>Clarification Negotiation</td>
      <td>Supports requirement clarification negotiation between Agents. When task intent is ambiguous or unclear, specific requirements are clarified through multi-round interactions.</td>
    </tr>
    <tr>
      <td>Feasibility Negotiation</td>
      <td>Supports feasibility confirmation negotiation between Agents, evaluating feasibility before task execution to avoid ineffective execution of infeasible tasks.</td>
    </tr>
    <tr>
      <td>Fulfillment Negotiation</td>
      <td>Supports task execution detail negotiation between Agents, negotiating task execution plans, timing, resources, and other details. After reaching agreement, enters the execution phase.</td>
    </tr>
    <tr>
      <td rowspan="4">Negotiation State Management</td>
      <td>State Machine Driven</td>
      <td>Each negotiation type is driven by a state machine, supporting three state transitions: IN_PROGRESS, AGREED, REJECTED, automatically tracking negotiation rounds and limiting maximum rounds to prevent infinite loops. Throws <code>NegotiationStateException</code> when rounds do not match.</td>
    </tr>
    <tr>
      <td>Context Transmission</td>
      <td>Negotiation context follows A2A-T protocol extension URI convention, carried in Task.metadata through the <code>https://projects.tmforum.org/a2aproject/telecommunication/extensions/DATA-NEGOTIATION-T/v1</code> key, supporting serialization and deserialization, ensuring multi-round negotiation state continuity.</td>
    </tr>
    <tr>
      <td>State Storage</td>
      <td>Provides <code>NegotiationStore</code> interface. Currently has built-in <code>InMemoryNegotiationStore</code> in-memory implementation, supporting negotiation state access by session ID, with extensible persistence implementation.</td>
    </tr>
    <tr>
      <td>Handler Registration Pattern</td>
      <td>Provides <code>NegotiationHandler</code> core handler, supporting Builder pattern registration of negotiation type handlers (<code>NegotiationTypeHandler</code>) and state storage. Client and server share negotiation orchestration logic through <code>RoleBoundNegotiationOrchestrator</code>.</td>
    </tr>
    <tr>
      <td rowspan="4">LLM Runtime</td>
      <td>Adapter Architecture</td>
      <td>Provides <code>LLMAdapter</code> interface and <code>OpenAICompatibleAdapter</code> implementation, based on OpenAI Java SDK (v4.36.0) compatible with all OpenAI protocol model services, switching different LLM backends through configuration.</td>
    </tr>
    <tr>
      <td>Structured Generation</td>
      <td>Supports structured output constrained by JSON Schema (<code>StructuredGenerationRequest</code>), used for LLM invocation scenarios requiring structured responses such as scenario identification and slot extraction.</td>
    </tr>
    <tr>
      <td>Session Management</td>
      <td>Built-in <code>LlmSessionStore</code> and <code>InMemoryLlmSessionStore</code>, supporting configuration of history window size, maximum total sessions, and per-Provider session limit to prevent memory overflow. Provides token usage tracking (<code>LlmUsage</code>).</td>
    </tr>
    <tr>
      <td>Local Rule Engine</td>
      <td>In addition to the OpenAI-compatible adapter, provides <code>local_rule</code> provider type, supporting rule-based local scenario identification and slot extraction, suitable for deterministic scenarios without LLM requirements.</td>
    </tr>
    <tr>
      <td rowspan="3">Prompt Resource Management</td>
      <td>Multi-language Resources</td>
      <td>Prompt resources are organized by language directories, supporting Chinese (zh-CN) and English (en-US) bilingual, covering scenario definitions, slot Schemas, templates, and system/user prompts.</td>
    </tr>
    <tr>
      <td>Multi-source Loading</td>
      <td>Supports Classpath resource loading (<code>ClasspathPromptResourceLoader</code>) and local file system loading (<code>LocalFilePromptTemplateLoader</code>, etc.), with in-package Classpath resources as fallback. Users can specify custom resource directories through configuration.</td>
    </tr>
    <tr>
      <td>Standardized Organization</td>
      <td>Prompt resources are organized using a standardized directory structure: scenarios/{lang}/scenarios.json (scenario definitions), slots/{scenario}/{lang}/slot.json (slot Schemas), templates/{scenario}/{lang}/template.md (templates), prompts/{action}/{lang}/ (system/user prompts).</td>
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
      <td>Complete source code of registry-center, including AgentCard management, CLI client, security capabilities, and other modules</td>
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
| PostgreSQL (optional) | >= 12 | Data persistence database; not required under file storage or SQLite storage mode |
| Milvus (optional) | >= 2.6 | Vector database required for semantic search capability |

> **Note:**
>
> - The registry-center service is started via `python -m agent_registry.start`, defaulting to listening on `127.0.0.1:5000`.
> - IP and port can be modified as needed. The configuration file is {installation directory}/etc/conf/server.conf.
> - Defaults to file storage mode (persistence_mode=file), with data saved in {installation directory}/data/agentcard.json. Supports switching to postgresql or sqlite (in development) storage mode. The configuration file is {installation directory}/etc/conf/persistence.conf.
> - Milvus is an optional dependency for the semantic search feature; if semantic search is not used, Milvus does not need to be deployed.

### Core Dependency Version Compatibility

**Table 4** Registry-center v1.0.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| a2a-sdk | >= 1.0.0a1 | A2A protocol implementation |
| a2a-sdk[signing] | >= 1.0.0a1 | AgentCard signing capability |
| fastapi | >= 0.115.11 | REST API framework |
| uvicorn | >= 0.34.0 | ASGI server |
| loguru | >= 0.7.3 | Logging |
| cryptography | ~= 46.0.5 | Cryptographic algorithm support |
| pymilvus | ~= 2.6.12 | Milvus vector database client (semantic search) |
| PyJWT | ~= 2.10.1 | JWT token processing |
| requests | ~= 2.32.3 | HTTP client |
| httpx | ~= 0.28.1 | Async HTTP client |
| environs | ~= 15.0.1 | Environment variable parsing |
| limits | ~= 4.0.0 | Rate limiting |
| starlette | ~= 0.50.0 | ASGI framework core |

> **Note:**
>
> - See requirements.txt for the complete dependency list.
> - a2a-sdk[signing] provides AgentCard signing and verification capabilities. The registry-center digitally signs registered AgentCards.
> - The registry-center itself does not provide login authentication, authorization, user management, encryption/decryption, or key management capabilities. These security infrastructure must be provided by the integrator's system.
> - Certificate requirements: Identity certificate server.cer (required, pem encoding, X.509v3 format), private key server_key.pem (required, pem encoding), private key password cert_pwd (required, stored in ciphertext), trust certificate trust.cer (required when verify_client=true), revocation list revocationlist.crl (optional).
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
| a2a-t-sdk | >= 1.0.0 | Agent negotiation capability (fulfillment negotiation) |
| a2a-sdk | latest | A2A protocol implementation (http-server + grpc) |
| fastapi | >= 0.135.1 | REST API framework |
| uvicorn | >= 0.42 | ASGI server |
| pydantic | >= 2.12.5 | Data model validation |
| openai | >= 2.26.0 | LLM invocation |
| loguru | >= 0.7.3 | Logging |
| PyYAML | >= 6.0.3 | YAML parsing |
| pymupdf | latest | PDF document parsing |

> **Note:**
>
> - See requirements.txt for the complete dependency list.
> - The negotiation configuration of a2a-t-sdk is automatically generated from `common/config/llm_config.json` to `samples/a2at_config/.env`.

## a2a-t-sdk-python

### Deliverables

The initial release of a2a-t-sdk-python only provides source code, without binary installation packages. Source code can be obtained from the [OpenAN community a2a-t-sdk-python repository](https://github.com/project-openan/a2a-t-sdk-python).

**Table 1** a2a-t-sdk-python v1.0.0 Deliverable List

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
      <td>a2a-t-sdk-python source code</td>
      <td>Complete source code of A2A-T SDK, including client task prompt generation, server compliance validation, multi-round negotiation, LLM runtime, and prompt resource management modules</td>
    </tr>
  </tbody>
</table>


> **Note:**
>
> - The initial release only delivers source code; deliverables do not include build engineering or binary installation packages.
> - Users need to complete build and installation themselves via `uv sync --dev` or `pip install -e .`.
> - This version is in the Alpha stage (v1.0.0); interfaces and resource organization may be adjusted with subsequent version evolution.

### Operating System Version Compatibility

**Table 2** a2a-t-sdk-python v1.0.0 Supported Scenarios

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

**Table 3** a2a-t-sdk-python v1.0.0 Runtime Environment Requirements

| Software | Version Requirement | Purpose |
|-----|---------|------|
| Python | >= 3.12 | SDK runtime environment |
| uv (recommended) / pip | uv >= 0.4 / pip >= 23 | Package management and build tools |
| LLM service | OpenAI protocol compatible | Dependency for LLM invocation scenarios such as task prompt generation, slot extraction, semantic validation |

> **Note:**
>
> - It is recommended to use uv for package management, installing dependencies via `uv sync --dev`; `pip install -e .` can also be used for installation.
> - LLM service is a required dependency. All LLM-related features of the SDK (scenario identification, slot extraction, semantic validation, negotiation interaction) depend on external LLM services.
> - The deepseek adapter (compatible with OpenAI protocol) is pre-registered by default. Other model services compatible with OpenAI protocol (such as OpenAI, Tongyi Qianwen, etc.) can be connected through `A2AT_LLM_BASE_URL` and `A2AT_LLM_API_KEY` configuration.
> - The configuration file template is available at `package_data/env.example`. Copy it to a `.env` file and modify as needed when using.

### Core Dependency Version Compatibility

**Table 4** a2a-t-sdk-python v1.0.0 Core Python Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| openai | latest | OpenAI-compatible protocol LLM client, used for LLM invocations such as scenario identification, slot extraction, semantic validation, negotiation interaction |
| jsonschema | >= 4.23.0 | JSON Schema validation, used for structural validation of slot values on the server side |
| python-dotenv | >= 1.1.0 | Environment variable loading, used to read SDK configuration from .env files |

> **Note:**
>
> - See `pyproject.toml` for the complete dependency list.
> - The openai library is the core dependency for LLM invocation, supporting multiple model service backends through its compatible protocol.
> - jsonschema is used for the slot Schema validation stage in the server-side compliance validation pipeline.
> - python-dotenv is responsible for loading configuration from .env files at SDK startup. All configuration items are injected through environment variables.
> - Development dependencies include: pytest (>= 8.0.0, testing framework), ruff (>= 0.3.0, code checking and formatting), mypy (>= 1.9.0, type checking).

### Configuration Item Compatibility

**Table 5** a2a-t-sdk-python v1.0.0 Configuration Item Description

| Configuration Category | Configuration Item | Default Value | Description |
|---------|-------|-------|------|
| Prompt Runtime | A2AT_LANGUAGE | en-US | Prompt resource language, supporting zh-CN, en-US |
| Prompt Runtime | A2AT_PROMPT_SOURCE_TYPE | local_file | Prompt resource source type |
| Prompt Runtime | A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR | In-package default directory | Custom resource root directory path |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_ENABLED | false | Whether to enable server-side compliance validation |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_PROVIDER | noop | Guardrail provider (currently only noop) |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_TIMEOUT_SECONDS | 10 | Guardrail request timeout (seconds) |
| LLM Runtime | A2AT_LLM_PROVIDER | deepseek | LLM provider name |
| LLM Runtime | A2AT_LLM_MODEL | deepseek-chat | Model name |
| LLM Runtime | A2AT_LLM_API_KEY | (empty) | API key (required) |
| LLM Runtime | A2AT_LLM_BASE_URL | https://api.deepseek.com | API base URL |
| LLM Runtime | A2AT_LLM_MAX_TOKENS | 2000 | Maximum token count |
| LLM Runtime | A2AT_LLM_TEMPERATURE | 0 | Sampling temperature |
| LLM Runtime | A2AT_LLM_TIMEOUT_SECONDS | 60 | Request timeout (seconds) |
| LLM Runtime | A2AT_LLM_HISTORY_WINDOW | 10 | Conversation history window message count |
| LLM Runtime | A2AT_LLM_SESSION_MAX_TOTAL | 300 | Maximum total sessions |
| LLM Runtime | A2AT_LLM_SESSION_MAX_PER_PROVIDER | 100 | Maximum sessions per Provider |
| Negotiation | A2AT_NEGOTIATION_STATE_STORE_TYPE | in_memory | Negotiation state storage type |

> **Note:**
>
> - All configuration items are managed through .env files. See `package_data/env.example` for the configuration template.
> - A2AT_LLM_API_KEY is required and must be configured with a valid LLM service API key.
> - A2AT_LLM_BASE_URL can be replaced with any OpenAI protocol-compatible service endpoint. Connecting to different model services only requires modifying this configuration and the corresponding API_KEY.
> - Compliance validation-related configurations only affect server-side behavior; the client side does not need to be concerned.
> - A2AT_PROMPT_COMPLIANCE_GUARDRAIL_PROVIDER currently only supports noop (pass-through). aws_bedrock and azure_content_safety are reserved extension interfaces and are not yet implemented.

### Protocol Standard Compatibility

**Table 6** Protocol Standards Followed by a2a-t-sdk-python v1.0.0

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

The initial release of a2a-t-sdk-java only provides source code, without binary installation packages. Source code can be obtained from the [OpenAN community a2a-t-sdk-java repository](https://github.com/project-openan/a2a-t-sdk-java).

**Table 1** a2a-t-sdk-java v1.0.0 Deliverable List

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
      <td>Complete source code of a2a-t-sdk-java, including 9 Maven modules: core model, resource management, LLM runtime, prompt processing, negotiation runtime, client facade, server facade, and sample integration</td>
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
  </tbody>
</table>

> **Note:**
>
> - The initial release only delivers source code. Integrators need to build artifacts through Maven.
> - Users can import the SDK through Maven dependencies, or build it themselves via `mvn -DskipTests package`.
> - This version is in the Alpha stage (v1.0.0); interfaces and module organization may be adjusted with subsequent version evolution.

### Operating System Version Compatibility

**Table 2** a2a-t-sdk-java v1.0.0 Supported Scenarios

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

**Table 3** a2a-t-sdk-java v1.0.0 Runtime Environment Requirements

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

**Table 4** a2a-t-sdk-java v1.0.0 Core Dependencies

| Dependency | Version | Purpose |
|-----|------|------|
| Lombok | 1.18.38 | Code generation (annotation processor, provided scope) |
| Jackson Databind | 2.20.1 | JSON serialization and deserialization |
| Jackson Annotations | 2.20.1 | Jackson annotation support |
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

**Table 5** a2a-t-sdk-java v1.0.0 Module List

| Module | ArtifactId | Purpose | Dependent Modules |
|------|-----------|------|----------|
| BOM | a2a-t-bom | Unified version management; integrators manage all module versions by importing BOM | None |
| Core | a2a-t-core | Shared abstractions and value types (OperationResult, PromptMessage, configuration models, exception hierarchy, etc.) | None |
| Resources | a2a-t-resources | Packaged prompt resources and loaders (scenario definitions, slot Schemas, templates, system prompts) | a2a-t-core |
| LLM | a2a-t-llm | LLM Provider integration (adapter interface, OpenAI-compatible adapter, session management, structured generation) | a2a-t-core |
| Prompt | a2a-t-prompt | Prompt templates, rendering, Schema validation (scenario identification, slot extraction, template rendering, semantic validation) | a2a-t-core, a2a-t-resources, a2a-t-llm |
| Negotiation | a2a-t-negotiation | Negotiation workflow and state processing (four negotiation types, state machine, storage interface, Handler registration) | a2a-t-core |
| Client | a2a-t-client | Client facade (A2ATClient), providing task prompt generation and client negotiation capability | a2a-t-core, a2a-t-llm, a2a-t-prompt, a2a-t-negotiation |
| Server | a2a-t-server | Server facade (A2ATServer), providing task prompt compliance validation and server negotiation capability | a2a-t-core, a2a-t-llm, a2a-t-prompt, a2a-t-negotiation |
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
>               <version>0.1.9</version>
>               <type>pom</type>
>               <scope>import</scope>
>           </dependency>
>       </dependencies>
>   </dependencyManagement>
>   ```
> - `a2a-t-sample` is an optional module, not published as an SDK artifact, and is only for development reference.

### Configuration Item Compatibility

**Table 6** a2a-t-sdk-java v1.0.0 Configuration Item Description

| Configuration Category | Configuration Item | Default Value | Description |
|---------|-------|-------|------|
| Prompt Runtime | A2AT_LANGUAGE | en-US | Prompt resource language, supporting zh-CN, en-US |
| Prompt Runtime | A2AT_PROMPT_SOURCE_TYPE | local_file | Prompt resource source type |
| Prompt Runtime | A2AT_PROMPT_RESOURCE_LOCAL_ROOT_DIR | Parent directory of .env file location | Custom resource root directory path |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_ENABLED | false | Whether to enable server-side compliance validation |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_PROVIDER | noop | Guardrail provider (currently only noop) |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_TIMEOUT_SECONDS | 10.0 | Guardrail request timeout (seconds) |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_POLICY_ID | (empty) | Guardrail policy identifier |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_ENDPOINT | (empty) | Guardrail service endpoint |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_REGION | (empty) | Service region |
| Compliance Validation | A2AT_PROMPT_COMPLIANCE_GUARDRAIL_CREDENTIALS_REF | (empty) | Credentials reference |
| LLM Runtime | A2AT_LLM_PROVIDER | openai_compatible | LLM provider name, supporting openai_compatible and local_rule |
| LLM Runtime | A2AT_LLM_MODEL | (empty) | Model name |
| LLM Runtime | A2AT_LLM_API_KEY | (empty) | API key (required) |
| LLM Runtime | A2AT_LLM_BASE_URL | (empty) | API base URL |
| LLM Runtime | A2AT_LLM_MAX_TOKENS | 2048 | Maximum token count |
| LLM Runtime | A2AT_LLM_TEMPERATURE | 0.2 | Sampling temperature |
| LLM Runtime | A2AT_LLM_TIMEOUT_SECONDS | 30.0 | Request timeout (seconds) |
| LLM Runtime | A2AT_LLM_HISTORY_WINDOW | 12 | Conversation history window message count |
| LLM Runtime | A2AT_LLM_SESSION_MAX_TOTAL | 300 | Maximum total sessions |
| LLM Runtime | A2AT_LLM_SESSION_MAX_PER_PROVIDER | 100 | Maximum sessions per Provider |
| Negotiation | A2AT_NEGOTIATION_STATE_STORE_TYPE | in_memory | Negotiation state storage type |

> **Note:**
>
> - All configuration items are managed through .env files. See `package_data/env.example` for the configuration template.
> - The SDK does not automatically discover .env files; the caller must explicitly provide the .env file path via `new A2ATClient(Path envPath)` or `new A2ATServer(Path envPath)`.
> - A2AT_LLM_API_KEY is required and must be configured with a valid LLM service API key.
> - A2AT_LLM_BASE_URL can be replaced with any OpenAI protocol-compatible service endpoint. Connecting to different model services only requires modifying this configuration and the corresponding API_KEY.
> - Compliance validation-related configurations only affect server-side behavior; the client side does not need to be concerned.
> - A2AT_PROMPT_COMPLIANCE_GUARDRAIL_PROVIDER currently only supports noop (pass-through). aws_bedrock and azure_content_safety are reserved extension interfaces and are not yet implemented.

### Protocol Standard Compatibility

**Table 7** Protocol Standards Followed by a2a-t-sdk-java v1.0.0

| Standard | Version | Description |
|-----|------|------|
| IG1453 A Structured Prompt of Agent to Agent Protocol for Telecoms (A2AT) | v1.0.0 | A2A-T structured prompt protocol standard published by TM Forum |
| IG1453 Agent to Agent Protocol for Telecoms (A2AT) | v2.0.0 | A2A-T protocol standard published by TM Forum, covering negotiation extensions |

> **Note:**
>
> - a2a-t-sdk-java is the Java reference implementation SDK for the A2A-T protocol standard. Task prompt format and negotiation process follow the above protocol standards.
> - The A2A-T protocol is the telecom domain extension of the A2A (Agent-to-Agent) protocol, standardized and published by TM Forum.
> - Negotiation context transmission follows the A2A project telecom extension URI convention, carried in Task.metadata through the `https://projects.tmforum.org/a2aproject/telecommunication/extensions/DATA-NEGOTIATION-T/v1` key.


# CVE Vulnerabilities

This version is the first release of OpenAN, with no CVE disclosed vulnerabilities.

# Source Code

OpenAN repository address: <https://github.com/project-openan>

# Contributing

As an OpenAN user, you can assist the OpenAN community in various ways. For methods of contributing to the community, please refer to the [Contributing to OpenAN](https://github.com/project-openan/.github/blob/main/CONTRIBUTING.md).

# Acknowledgments

We sincerely thank all members who participated in and assisted the OpenAN project. Your dedication has made the successful release of this version possible and provides possibilities for OpenAN's continued development.