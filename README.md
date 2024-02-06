# DOME Marketplace Integration and Federation Guide

![DOME Logo](doc/img/DOME_logo_doc.png)



<!-- ToC created with: https://github.com/thlorenz/doctoc -->
<!-- Update with: doctoc README.md -->
<!-- Will be also updated during pre-release/release GitHub workflow -->

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<!-- param::title::**Table of Contents**:: -->
**Table of Contents**

- [Introduction](#introduction)
  - [Who is this guide for?](#who-is-this-guide-for)
  - [What is DOME?](#what-is-dome)
  - [What will I accomplish following this guide?](#what-will-i-accomplish-following-this-guide)
  - [Pre-requisites](#pre-requisites)
- [Onboarding as a DOME Participant](#onboarding-as-a-dome-participant)
  - [What will I accomplish following this section?](#what-will-i-accomplish-following-this-section)
  - [Pre-requisites](#pre-requisites-1)
  - [Step-by step process](#step-by-step-process)
- [Distributed components](#distributed-components)
  - [Access Node](#access-node)
    - [Overview and sub-components](#overview-and-sub-components)
    - [Infrastructure requirements](#infrastructure-requirements)
    - [How to deploy](#how-to-deploy)
    - [How to configure](#how-to-configure)
    - [How to validate a deployment](#how-to-validate-a-deployment)
    - [How to operate](#how-to-operate)
    - [How to update](#how-to-update)
    - [Release process](#release-process)
    - [Troubleshooting](#troubleshooting)
  - [IAM components](#iam-components)
- [Authentication](#authentication)
  - [DOME Verifiable Credentials (LEAR)](#dome-verifiable-credentials-lear)
  - [How to implement](#how-to-implement)
- [Integration API (TMForum)](#integration-api-tmforum)
- [Policies](#policies)
  - [Defining policies](#defining-policies)
    - [Local policies](#local-policies)
    - [Distributed policies](#distributed-policies)
  - [Enforcing policies](#enforcing-policies)
    - [In front of TMForum API](#in-front-of-tmforum-api)
    - [In front of Context Broker API](#in-front-of-context-broker-api)
- [Example content (to be removed later)](#example-content-to-be-removed-later)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
(to be removed later)  
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

This guide provides detailed, self-contained and actionable technical instructions for integrating and federating a marketplace in DOME.  
It is meant to be the reference for what is _currently_ technically available and ready to be used. When additional functionality, components and/or 
instruction get available, this guide will be adapted accordingly.

This guide limits on the technical details and therefore is not providing any details about contractual 
and business aspects of the marketplace integration and federation.


### Who is this guide for?

This guide aims for future participants willing to technically integrate and federate a marketplace in DOME. Descriptions and instructions are 
given as a comprehensive, step-by-step guide in such detail, so that IT and engineering teams can successfully and efficiently 
perform the necessary steps without profound knowledge of the DOME implementation details.

Nevertheless, this guide focusses on the actual integration of a marketplace in DOME, providing only the information 
needed to perform the actual setup for integration and federation. More details and in-depth knowledge about DOME and its involved 
components can be found in the linked resources.

The suggested deployment target infrastructure is [Kubernetes](https://kubernetes.io/). Therefore a sufficient 
knowledge of Kubernetes and [Helm](https://helm.sh/) is expected when following this guide. Knowledge about 
[ArgoCD](https://argo-cd.readthedocs.io/en/stable/) is also helpful when using it as GitOps 
continuous delivery tool.  
This guide requires access to a domain and it's DNS settings, as well as configuring proper certificates. 
Therefore also knowledge about [cert-manager](https://cert-manager.io/) 
and [external-dns](https://github.com/kubernetes-sigs/external-dns) is recommended.  
Authentication requires usage of decentralized identifiers and verifiable credentials, which requires an 
appropriate configuration of the related components. Therefore, the reader of this guide should be 
familiar with [DIDs](https://www.w3.org/TR/did-core/) and [VC/VP standards](https://www.w3.org/TR/vc-data-model/).





### What is DOME?

Cloud computing is identified as a central piece of Europe’s digital future, giving European
businesses and public organisations the data processing technology required to support their
digital transformation. 
The European Commission thereby stepped up its efforts to support
cloud uptake in Europe as part of its strategy, notably with the pledge to facilitate "the set-up
of a cloud services marketplace for EU users from the private and public sector". 
DOME is
materialising the envisioned online marketplace, providing the means for accessing trusted
services, notably cloud and edge services, building blocks deployed under the Common
Services Platform and more generally any software and data processing services developed
under EU programmes such as the Digital Europe Programme, Horizon 2020 or Horizon
Europe.

Relying on Gaia-X concepts and open standards, DOME is providing the finishing touch to the
technical building that the Digital Europe Program is creating for boosting the development
and adoption of trusted Cloud and Edge services in Europe. It will provide the single point for
enabling customers and service providers to meet each other in a trustful manner. DOME is 
taking the form of a federated collection of marketplaces connected to a shared digital catalogue
of cloud and edge services. Each of the federated marketplaces will be independent or
connected to the offering of a given cloud/edge infrastructure service provider which, in turn,
can be classified as cloud IaaS providers or cloud platform service providers (each of which
provide a platform targeted to solve the integration of vertical data/application services from a
given vertical domain, like smart cities or smart farming, or the integration of certain type of
data/application services, e.g., AI services). DOME is relying on the adoption of common open
standards for the description and the management of the lifecycle of cloud and edge service
products and offerings around those products, as well as their access or match-making
services through a shared catalogue.



### What will I accomplish following this guide?

After following this guide, you will have a complete and functioning integration of a marketplace 
in a federated DOME environment.

The following sections provide details about the necessary steps:
* [Onboarding](#onboarding-as-a-dome-participant): How to perform onboarding as DOME participant (Note, 
  that this topic is currently under discussion and details will be added later).
* [Distributed components](#distributed-components): How to configure, deploy and operate the different 
  required components. This involves the access node and components required for the IAM.
* [Authentication](#authentication): How to authenticate at services and how to implement the authentication.
* [Integration API](#integration-api-tmforum): How to integrate with the TMForum APIs, especially when using an 
  own marketplace implementation instead of the BAE. Some samples and tutorials are given for core federation 
  scenarios.
* [Policies](#policies): How access policies are defined, created and enforced (Note, 
  that this topic is currently under discussion and details will be added later).



### Pre-requisites

There are some prerequisites that need to be fulfilled before following this guide:
* Domain: You need control over an own domain and have access to the DNS settings.
* Public access: Certain components need to be publicly accessible under your own domain. Therefore, a suitable 
  infrastructure (like a cloud-hosted Kubernetes cluster) is required for running the components.
  
Additional prerequisites are provided in the different sections.






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

> One might also link or integrate this guide: [https://dome-marketplace.github.io/iam-guide/](https://dome-marketplace.github.io/iam-guide/)

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

## Example content (to be removed later)

Some content

**Some table:**

| Title 1 | Title 2 | Title 3 |
|---------|---------|---------|
| abc     | def     | ghi     |
| 123     | 456     | 789     |
| jkl     | mno     | pqr     |



Some more content in a list
* Entry 1
* Entry 2
* Entry 3

Some mermaid diagram

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

