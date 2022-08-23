---
title: "SCIM Definitions, Concepts, and Use Cases (v.New)"
abbrev: "SCIM Definitions, Concepts, and Use Cases (v.New)"
docname: draft-dingle-scim-use-cases-00
category: info

ipr: trust200902
area: TODO
workgroup: SCIM
keyword: [Internet-Draft, SCIM]

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs]

author:
 -
    name: Pamela Dingle
    organization: Microsoft
    email: XXX

normative: 

informative: 


--- abstract

This document provides high-level concepts and scenarios that illustrate how the SCIM 2.0 protocol and schema work together, and how they can be extended, by discussing common terms, concepts and scenarios. This document will be updated over time as new extensions and changes to the specifications evolve.

// TODO: add status of this memo later

--- middle

# Introduction

(To-Do)

## Conventions and Definitions

{::boilerplate bcp14-tagged}

## IANA Considerations

(To-Do)


# Terminology
// can any of these terms be referenced from IETF 1392 or any other authoritative source?
URIs as defined in [rfc3986]
REST HTTP method sematincs as defined in section-4.3 of [rfc7231]
Usage of Additional HTTP Status Codes as defined in [rfc6585]

## SCIM Protocol (SCIM API)
An application-level protocol for managing resources defined by SCIM Schemas using a subset of RESTful HTTP methods such as GET, PUT, POST, PATCH and DELETE.

## SCIM Resource
A unique entity that can be managed via RESTful command to a SCIM API, and defined by pre-defined schema. SCIM standardizes two types of resource (Users and Groups) by default and provides an extension mechanism to add new resource types.

## SCIM Schema
Describes the allowable contents of a resource type, defined by a set of schema URIs. Properties of resource attributes include type, mutability, cardinality, and returnability.

## SCIM Service Provider (SCIM Server)
A role in the SCIM protocol whereby standard endpoints are made available to clients who make SCIM protocol requests. Endpoints include /Users, /Groups, /Schema, /ServiceProviderConfig and /Me.

## SCIM Client
A protocol role in which the service provider is actively called to either push or pull resource information from standardized endpoints using standardized HTTP methods. XXX

SCIM clients make RESTful calls to service providers, targeting standardized endpoints and using standardized HTTP methods. XXX

A role in the SCIM protocol held by the actor making calls to API endpoints made available by SCIM service providers.

## User Lifecycle Management
A business process where the relationships and attributes of people are accurately maintained over time, and potentially across digital domains and resources. User Lifecycle Management processes can be automated or driven by administrators, delegated administrators or the people themselves. 
//TODO: check in IDpro glossary

## Group Management
A business process where resources with commonalities are bundled together and referred to as a single resource. This bundle of resources itself becomes a resource with a lifecycle and a membership that must be maintained over time.

## Provisioning
The process of creating an identity in a target system based on certain conditions. Examples of provisioning include JIT (just in time) provisioning and zero-day de-provisioning. //TODO: move de-provisioning to its own definition
// Is bootstrapping a synonym?

## De-provisioning
//TODO

## Synchronization
The process of causing a set of data or files to remain identical in more than one location.

## Event
An action or activity that may trigger a SCIM flow. Examples of events might include a change in an upstream HR system, a user submitting a self-service profile change, or a risk detection system discovering an account takeover. // Can we reference IETF Metconf event notifications (RFC 5277)
//Is there a SET definition  of event?

## Source of Authority (SOA)
A designation given to an entity that is authoritative for a given attribute. For example HR could be the source of authority for a user's home address, while an email system could be the SOA for a user's email address.

## Pagination

(To-Do)

## Attribute
An attribute is a property of a resource that describes the resource in some way. Attributes are defined within a SCIM schema, where rules for the content of the attribute are defined.

## Identifier
An identifier is an attribute that acts as a label or name of a resource, distinguished from others within a given context. 

# Concepts

## Cardinality, Mutability and Uniqueness

(To-Do)

## Relationships between Resources
A resource can be affiliated with another resources in different ways. Examples of relationships could be a "manager" relationship where one user reports to another user in the organization's heirarchy, or a "member" relationship where a user or other resource type is part of the membership of a group. Relationships are represented by schema attributes, and can have different complexity and cardinality.

// group members can be users, groups or other resources
// need a better definition of what a human managerial relationship

## Data Directionality

## JIT Provisioning
Just in time provisioning is a case where a new resource is created in a new domain only at the time it is needed - this is often contrasted to a synchronization process where users are created in advance of any need. JIT provisioning can save licensing costs as well as ensuring least privilege.
//is there a use case where a group is ever JIT provisioned?
//most commonly JIT provisioning happens during federation, which isn't a SCIM operation. should this be discussed at all?

## Self-Service
Self-service authorizes the end user affiliated with a given resource to alter certain attributes. Examples include an Enterprise user resetting their own password, or a consumer user changing their profile data.

## API Security
The measures that a SCIM Service Provider takes to secure its endpoints.  This includes authorizing client access as discussed in RFC 7644 Section 2 as Authentication and Authorization but also includes API throttling, use of secure transports, and other evolving security measures.

## Account Linking & Reconciliation
Using a shared identifier between systems to identify two different resources in two different systems that represent the same entity. For systems where there may be existing data not originating from the SCIM client, an attribute that has a value known by both systems is typically needed.
// Do we even need this and are they significantly different from each other?

## Hard & Soft Object Deletion
Two different concepts of state of deletion of objects. Hard deletion results in a resource being permanently, irrecoverably deleted from the service provider's directory. Soft deletion results in the resource being deleted from active visibility and consideration of things like attribute uniqueness, but in a manner where it can be restored back from deletion at a later point.



# Use Cases: Currently Ratified
//Should explain both data directions
## Listing & Displaying Resources
 * Client gets attributes of a specific resource
 * Client gets a list of all groups

## Search & Query
 * Client gets the first name attribute of every user with a last name of "Smith"

## Automated Setup
* Schema Negotiation
* Auto Discovery (schema, resource types, extensions)
* Client Registration/security

## Replace new member in million-member group
* Client uses PATCH to add/remove/replace member to group
* Client doesn't use PUT for large groups due to need to list all members in request

## Create new resource type to represent new types of identity data
* Create new resources (/departments, /contacts) and a new schema to support them.

//Are these more features than use cases?
## Create new Schema Extension 
 * SCIM Service Provider creates a new schema file and URI for an existing resource type
// are these more features than use cases?

## User Lifecycle Management

##     Bootstrap (Provisioning)
 * Client pushes a user population to a new SCIM Service Provider
 * SCIM Server makes a user population available to a new SCIM Client to pull 

##     Incremental Data Collection
 * Client pushes or pulls only the new atttributes or new users since a given date or event

##     Reconciliation of data sources
 * Client compares internal data source to SCIM output to find discrepancies

## Massive Dataset Maintenance

##     Bulk Attribute Update

###    Pagination
* Splitting apart a set of results from a client query into more than one part that must be retrieved via subsequent API calls. 




# Use Cases - Future WG work

## IOT manage change of ownership - 
// Proposed by Antoine
- changing authority that manages keys
- 

## Business Scenarios
//rationale: should be LESS geeky than Use Cases

## SaaS App writes multi-tenant integration to get data from any cloud platform
* schema discovery, initial bootstrap, reconciliation


## Progressive Profiling
* Mobile app GETs existing data for user, detect missing information, initiate workflow that initiates a POST

## User Self-Service
* tooling for a profile self-service page calls /Me

## Bulk Address Change
* Organization with 100,000 users moves buildings. Filter results by old building name and return only the identifier. Then run bulk PATCH against each returned id

## Migration
 * An organization is moving from a legacy system to a modern system and needs to populate the new system with users and groups.

## Provisioning of Identity for Digital Twins
* A system discovers or is informed of the existance of real world items and required a unique identifier to be provisioned for that item to act as a unique digital identity for that real world item or entitiy.  This case is quite commonly encountered in supply chain use cases, especially those connected to supply chain entity or product verification and deduplication and in cases involving intelligent agents that may act as simulatated analogs to real world entities. see https://datatracker.ietf.org/doc/draft-zhou-nmrg-digitaltwin-network-concepts/ 