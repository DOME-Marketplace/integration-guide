# DOME Marketplace Integration and Federation Guide

![DOME Logo](doc/img/DOME_logo_doc.png)

Guide for DOME marketplace integration and federation

<!-- ToC created with: https://github.com/thlorenz/doctoc -->
<!-- Update with: doctoc README.md -->
<!-- Will be also updated during pre-release/release GitHub workflow -->

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- param::title::**Table of Contents**:: -->
**Table of Contents**

- [First section](#first-section)
  - [First subsection](#first-subsection)
- [Second section](#second-section)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
>**_NOTE:_**
> We want future Participants to integrate successfully and efficiently, therefore we provide a clear, structured, step-by-step Integration Guide that is comprehensive, self-contained, self-explanatory and actionable.
This Integration Guide should:
>- be the single point of entry for any stakeholder that wants to _execute_ on integrating and federating a marketplace in DOME
>- be the reference for what is _currently_ available to integrators and with what level of stability vs. expected change
>- not assume knowledge of DOME implementation details from the part of the reader
>- be comprehensive so as to allow an executing IT/eng team to work autonomously
>- provide detailed, self-contained, actionable instructions
>- include context when appropriate to facilitate the comprehension of the Why, the What, the How and the with Whom at each step.
---

## Introduction

### Who is this guide for?

### What is DOME?

### What will I accomplish following this guide?

> A complete and functioning integration of a marketplace in a federated DOME environment (contractual and business aspects not included).

### Pre-requisites

> x. need to be a legal entity of this type or another; have a registration number of this type or another; etc.

## Onboarding as a DOME Participant

### What will I accomplish following this section?

### Pre-requisites

> ex. have an eIDAS certificate; pointers to how one can be procured etc.

### Step-by step process

>- What actions do I need to perform and where?
>- What information do I need to provide, to whom, and in what form?
>- What artefacts do I need to provide and to whom ? (ex. VCs) 
>- How do I obtain/produce/certify those artefacts ? (ex. GAIA-X compliance)
>- What artefacts do I get out of the onboarding process how/where do I use them subsequently ? 
(ex. the signing key that will later be used by my Access Node)

## Distributed components

> Components that need to be operated by a federated participant.

### Access Node

#### Overview and sub-components

> To understand what the sub-components are, how they all work together and how they interact

#### Infrastructure requirements

> ex. internal endpoint for the TMForum APIs ; external endpoint for the context broker API ; other endpoints between components ?

#### How to deploy

> incl. where to find clean, versioned, infrastructure agnostic HELM charts.

#### How to configure

> Recommended configuration for all the sub-components, any considerations. When should I change them?

#### How to validate a deployment

> (validate that everything works)

#### How to operate

>- Management/admin APIs. 
>- Instrumentation, metrics, logs, alerts

#### How to update

#### Release process

> Versioning, release notes, stability considerations

#### Troubleshooting

### IAM components

> (similar to the Access Node section)

## Authentication

### DOME Verifiable Credentials (LEAR)

### How to implement

> using wallets, OIDC4VC&VP. verification etc.

## Integration API (TMForum)

> Samples & tutorials for implementing core federation scenarios using the TMForum APIs (with focus on semantics and workflow, beyond the API reference)
>
> Some content also required for the Knowledgebase, which should be added here as well:
> - How to: autenticate the marketplace on the shared data layer
> - How to: retrieve DOME ecosystem notifications
> - How to: retrieve a list of products from the shared catalog
> - How to: retrieve the product description from the shared catalog
> - How to: retrieve the product price model from the shared catalog
> - How to: push a product on the shared catalog
> - How to: retrieve an order from other marketplaces
> - How to: push a provisioning status on the shared data layer
> - How to: push metering information on the shared data layer
> - How to: push billing information on the shared data layer
> - How to: retrieve billing information on the shared data layer

## Policies

### Defining policies

>- How can a Service Provider create policies that concern the Products that they offer ?
>- How can a Marketplace Operator create policites that concern the Products that they host ?

#### Local policies

> That only the federated marketplace needs to enforce locally.

#### Distributed policies

> That everyone in the federation needs to enforce.

### Enforcing policies

#### In front of TMForum API

> i.e. marketplace -to- Access Node
PEP, PDP - when are they needed and when not ?

#### In front of Context Broker API

> i.e. Access Node -to- Access Node

---



Some content

**Some table:**

| Title 1 | Title 2 | Title 3 |
|---------|---------|---------|
| abc     | def     | ghi     |
| 123     | 456     | 789     |
| jkl     | mno     | pqr     |



### First subsection

Some more content

Some mermaid diagram

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```



## Second section

Second content

* Another table:

  | Title 1 | Title 2 | Title 3 |
  |---------|---------|---------|
  | abc     | def     | ghi     |
  | 123     | 456     | 789     |
  | jkl     | mno     | pqr     |
