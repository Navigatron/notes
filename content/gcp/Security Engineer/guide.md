---
title: Professional Cloud Security Engineer Certification Exam Guide
---

[Home](../../../index.md) > [GCP](../index.md) > [Professional Security Engineer](./index.md) > Professional Cloud Security Engineer Certification Exam Guide

---

# Professional Cloud Security Engineer Certification Exam Guide

1. Configuring access within a cloud solution environment
	1. Configuring Cloud Identity. Considerations include:
		1. Managing Cloud Identity
		2. Configuring Google Cloud Directory Sync
		3. Managing super administrator account
		4. Automating user lifecycle management process
		5. Administering user accounts and groups programmatically
	2. Managing service accounts. Considerations include:
		1. Protecting and auditing service accounts and keys
		2. Automating the rotation of user-managed service account keys
		3. Identifying scenarios requiring service accounts
		4. Creating, authorizing, and securing service accounts
		5. Securely managing API access management
		6. Managing and creating short-lived credentials
	3. Managing authentication. Considerations include:
		1. Creating a password policy for user accounts
		2. Establishing Security Assertion Markup Language (SAML)
		3. Configuring and enforcing two-factor authentication
	4. Managing and implementing authorization controls. Considerations include:
		1. Managing privileged roles and separation of duties
		2. Managing IAM permissions with basic, predefined, and custom roles
		3. Granting permissions to different types of identities
		4. Understanding difference between Cloud Storage IAM and ACLs
		5. Designing identity roles at the organization, folder, project, and resource level
		6. Configuring Access Context Manager
	5. Defining resource hierarchy. Considerations include:
		1. Creating and managing organizations
		2. Designing resource policies for organizations, folders, projects, and resources
		3. Managing organization constraints
		4. Using resource hierarchy for access control and permissions inheritance
		5. Designing and managing trust and security boundaries within Google Cloud projects
2. Configuring network security
	1. Designing network security. Considerations include:
		1. Configuring network perimeter controls (firewall rules; Identity-Aware Proxy (IAP))
		2. Configuring load balancing (global, network, HTTP(S), SSL proxy, and TCP proxy load balancers)
		3. Identifying Domain Name System Security Extensions (DNSSEC)
		4. Identifying differences between private versus public addressing
		5. Configuring web application firewall (Google Cloud Armor)
		6. Configuring Cloud DNS
	2. Configuring network segmentation. Considerations include:
		1. Configuring security properties of a VPC network, VPC peering, Shared VPC, and firewall rules
		2. Configuring network isolation and data encapsulation for N tier application design
		3. Configuring app-to-app security policy
	3. Establishing private connectivity. Considerations include:
		1. Designing and configuring private RFC1918 connectivity between VPC networks and Google Cloud projects (Shared VPC, VPC peering)
		2. Designing and configuring private RFC1918 connectivity between data centers and VPC network (IPsec and Cloud Interconnect)
		3. Establishing private connectivity between VPC and Google APIs (Private Google Access, Private Google Access for on-premises hosts, Private Service Connect)
		4. Configuring Cloud NAT
3. Ensuring data protection
	1. Protecting sensitive data. Considerations include:
		1. Inspecting and redacting personally identifiable information (PII)
		2. Configuring pseudonymization
		3. Configuring format-preserving substitution
		4. Restricting access to BigQuery datasets
		5. Configuring VPC Service Controls
		6. Securing secrets with Secret Manager
		7. Protecting and managing compute instance metadata
	2. Managing encryption at rest. Considerations include:
		1. Understanding use cases for Google default encryption, customer-managed encryption keys (CMEK), customer-supplied encryption keys (CSEK), Cloud External Key Manager (EKM), and Cloud HSM
		2. Creating and managing encryption keys for CMEK, CSEK, and EKM
		3. Applying Google's encryption approach to use cases
		4. Configuring object lifecycle policies for Cloud Storage
		5. Enabling confidential computing
4. Managing operations in a cloud solution environment
	1. Building and deploying secure infrastructure and applications. Considerations include:
		1. Automating security scanning for Common Vulnerabilities and Exposures (CVEs) through a CI/CD pipeline
		2. Automating virtual machine image creation, hardening, and maintenance
		3. Automating container image creation, verification, hardening, maintenance, and patch management
	2. Configuring logging, monitoring, and detection. Considerations include:
		1. Configuring and analyzing network logs (firewall rule logs, VPC flow logs, packet mirroring)
		2. Designing an effective logging strategy
		3. Logging, monitoring, responding to, and remediating security incidents
		4. Exporting logs to external security systems
		5. Configuring and analyzing Google Cloud audit logs and data access logs
		6. Configuring log exports (log sinks, aggregated sinks, logs router)
		7. Configuring and monitoring Security Command Center (Security Health Analytics, Event Threat Detection, Container Threat Detection, Web Security Scanner)
5. Ensuring compliance
	1. Determining regulatory requirements for the cloud. Considerations include:
		1. Determining concerns relative to compute, data, and network
		2. Evaluating security shared responsibility model
		3. Configuring security controls within cloud environments
		4. Limiting compute and data for regulatory compliance
		5. Determining the Google Cloud environment in scope for regulatory compliance

---

[Home](../../../index.md) > [GCP](../index.md) > [Professional Security Engineer](./index.md) > Professional Cloud Security Engineer Certification Exam Guide
