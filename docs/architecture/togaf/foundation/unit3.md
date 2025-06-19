The `ADM`, Architecture Development Method, is a detailed step by step process for developing or changing an enterprise architecture

![adm](../../../assets/togaf/adm.png)

## Phases

### Preliminary Phase

Determine the Architecture Capability desired by the organization:

* Review the organizational context for conducting Enterprise Architecture
* Identify and scope the elements of the enterprise organizations
* Identify the established frameworks, methods, and processes
* Establish Capability Maturity target

Establish the Architecture Capability:

* Define and establish the Organizational Model
* Define and establish the detailed process and resources for Architecture Governance
* Select and implement tools that support the Architecture Capability
* Define the Architecture Principles

Deliverables: 

* Request for Architecture Work (Demande de mise en chantier d'architecture)
* Architecture Principles

### Phase A: Architecture Vision

* Define the scope of the Architecture Project
* Identify stakeholders, concerns, and associated requirements
* Assess the capability of the Enterprise Architecture team

Deliverables:

* Statement of Architecture Work (stakeholders need to agree on a summary of the target)
* Architecture Vision

> Phase B, C, & D : A set of domain architectures approved by the stakeholders for the problem being addressed, with a set of gaps, and work to clear the gaps understood by the stakeholders (building blocks)

### Phase B: Business Architecture

Development of the target Business Architecture to support the agreed Architecture Vision and stakeholder concerns

Workshop with the business to understand more the business requirements

### Phase C: Information Systems Architecture

Development of the target Information Systems Architectures, describing how the enterprise’s Information Systems 

Development of the Target Data Architecture that enables the Business Architecture and the Architecture Vision, in a way that addresses the Statement of Architecture Work and stakeholder concerns

Divided into two domain:

* Data Architecture: Define data entities, relationships, data governance
* Application Architecture: Identify applications, their interactions, and alignment with business needs

### Phase D: Technology Architecture

Define the logical and physical technology infrastructure to support the agreed Architecture Vision

Focus: Networks, platforms, services, and infrastructure technologies

### Phase E: Opportunities & Solutions

Generate the initial complete version of the Architecture Roadmap, based upon the gap analysis and candidate Architecture Roadmap components from Phases B, C, and D

Determine whether an incremental approach is required, and if so identify Transition Architectures that will deliver continuous business value

Define the overall Solution Building Blocks (SBBs) to finalize the Target Architecture based on the ABBs

Dependency between the set of changes. (Work Package & Gap dependency)

Value, effort, and risk associated with each change and work package.

### Phase F: Migration Planning

Finalize the Architecture Roadmap and the supporting Implementation and Migration Plan

Ensure that the Implementation and Migration Plan is co-ordinated with the enterprise’s approach to managing and implementing change in the enterprise’s overall change portfolio

Ensure that the business value and cost of work packages and Transition Architectures is understood by key stakeholders

### Phase G: Implementation Governance

Ensure conformance with the Target Architecture by Implementation Projects

Perform appropriate Architecture Governance functions for the solution and any implementation-driven architecture Change Requests

### Phase H: Architecture Change Management

Procedures for managing change to the new architecture

* Ensure that the architecture development cycle is maintained
* Ensure that the Architecture Governance framework is executed
* Ensure that the Enterprise Architecture Capability meets current requirements

### Requirements Management

Acts as a central repository and validation mechanism for all phases

* Ensure that the Requirements Management process is sustained and operates for all relevant ADM phases.
* Manage Architecture Requirements identified during any execution of the ADM cycle or a phase.
* Ensure that relevant Architecture Requirements are available for use by each phase as the phase is executed.

## Scope

The scope of an architecture is first expressed in terms of `breadth`, `depth`, and `time`

* `Breadth`: what is the full extent of the enterprise, and what part of that extent will this architecting effort deal with?
* `Depth`: to what level of detail should the architecting effort go?
* `Time Period`: what is the time period that needs to be articulated for the Architecture Vision, and does it make sense for the same period to be covered in the detailed Architecture Description?
