# 9. Configuration Management Policy

Ahana standardizes and automates configuration management through the use of Terraform/Ansible scripts as well as documentation of all changes to production systems and networks. Terraform and Ansible automatically configure all Ahana systems according to established and tested policies, and are used as part of our Disaster Recovery plan and process.

## 9.1 Applicable Standards

### 9.1.1 Applicable Standards from the HITRUST Common Security Framework

- 06 - Configuration Management

### 9.1.2 Applicable Standards from the HIPAA Security Rule

- 164.310(a)(2)(iii) Access Control & Validation Procedures

## 9.2 Configuration Management Policies

1. Terraform and Ansible are used to standardize and automate configuration management.
2. No systems are deployed into Ahana environments without approval of the Ahana CTO.
3. All changes to production systems, network devices, and firewalls are approved by the Ahana CTO before they are implemented to assure they comply with business and security requirements.
4. All changes to production systems are tested before they are implemented in production.
5. Implementation of approved changes are only performed by authorized personnel.
6. Tooling to generate an up-to-date inventory of systems, including corresponding architecture diagrams for related products and services, is hosted on GitLab.
   - All systems are categorized as production and utility to differentiate based on criticality.
   - The Security Officer maintains scripts to generate inventory lists on demand using APIs provided by each cloud provider.
   - These scripts are used to generate the diagrams and asset lists required by the Risk Assessment phase of Ahana's Risk Management procedures ([§4.3.1](#4.3-risk-management-procedures)).
   - After every use of these scripts, the Security Officer will verify their accuracy by reconciling their output with recent changes to production systems. The Security Officer will address any discrepancies immediately with changes to the scripts.
7. All frontend functionality (developer dashboards and portals) is separated from backend (database and app servers) systems by being deployed on separate servers or containers.
8. All software and systems are tested using unit tests and end to end tests.
9. All committed code is reviewed using pull requests to assure software code quality and proactively detect potential security issues in development.
10. Ahana utilizes development and staging environments that mirror production to assure proper function.
11. Ahana also deploys environments locally using Vagrant to assure functionality before moving to staging or production.
12. All formal change requests require unique ID and authentication.
13. Clocks are continuously synchronized to an authoritative source across all systems using NTP or a platform-specific equivalent. Modifying time data on systems is restricted.

## 9.3 Provisioning Production Systems

1. Before provisioning any systems, ops team members must file a request in the Ahana Tracking System.
   - Tracking System access requires authenticated users.
   - The CTO grants access to the Tracking System following the procedures covered in the [Access Establishment and Modification section](#7.2-access-establishment-and-modification).
2. The CTO, or an authorized delegate of the CTO, must approve the provisioning request before any new system can be provisioned.
3. Once provisioning has been approved, the ops team member must configure the new system according to the standard baseline chosen for the system's role using Ansible and Terraform.
4. Once the system has been provisioned, the ops team member must contact the security team to inspect the new system. A member of the security team will verify that the secure baseline has been applied to the new system, including (but not limited to) verifying the following items:
   - Removal of default users used during provisioning.
   - Network configuration for system.
   - Data volume encryption settings.
   - Intrusion detection and virus scanning software installed.
   - All items listed below in the operating system-specific subsections below.
5. Once the security team member has verified the new system is correctly configured, the team member must add that system to the Nessus security scanner configuration.
6. The new system may be rotated into production once the CTO verifies all the provisioning steps listed above have been correctly followed and has marked the Issue with the `Approved` state.

### 9.3.1 Provisioning Linux Systems

1. Linux systems have their baseline security configuration applied via Salt states. These baseline Salt states cover:
   - Ensuring that the machine is up-to-date with security patches and is configured to apply patches in accordance with our policies.
   - Stopping and disabling any unnecessary OS services.
   - Configuring 15-minute session inactivity timeouts.
   - Installing and configuring the ClamAV virus scanner.
   - Installing and configuring the NTP daemon, including ensuring that modifying system time cannot be performed by unprivileged users.
   - Configuring LUKS volumes for providers that do not have native support for encrypted data volumes, including ensuring that encryption keys are protected from unauthorized access.
   - Configuring authentication to the centralized LDAP servers.
   - Configuring audit logging as described in the [Auditing Policy section](#8-auditing-policy).
2. Any additional Salt states applied to the Linux system must be clearly documented by the ops team member in the DT request by specifying the purpose of the new system.

### 9.3.2 Provisioning Windows Systems

Ahana doesn't use any Windows systems

### 9.3.3 Provisioning Management Systems

Ahana uses Terraform in the cloud and has no plans to provision management systems.

## 9.4 Changing Existing Systems

1. Subsequent changes to already-provisioned systems are unconditionally handled by one of the following methods:

   - Changes to Terraform.
   - Changes to Ansible playbooks.

2. Configuration changes to Terraform or Ansible must be initiated by creating a Merge Request in Github.
   - The ops team member will create a feature branch and make their changes on that branch.
   - The ops team member must test their configuration change locally when possible, or on a development and/or staging sandbox otherwise.
   - At least one other ops team member must review the change before merging the change into the main branch.
3. In all cases, before rolling out the change to production, the ops team member must file an Issue in the DT project describing the change. This Issue must link to the reviewed Merge Request and/or include a link to the runbook.
4. Once the request has been approved by the CTO, the ops team member may roll out the change into production environments.

## 9.5 Patch Management Procedures

Ahana periodically performs security patch updates on production systems.

## 9.6 Software Development Procedures

1. All development is performed on the master branch to keep development cycles short.
   - Changes must be covered under 1) a unit test where possible, or 2) integration tests.
   - Integration tests are _required_ if unit tests cannot reliably exercise all facets of the change.
2. Developers are strongly encouraged to follow the [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) style.

## 9.7 Software Release Procedures

1. Software releases are treated as changes to existing systems and thus follow the procedure described in [§9.4](#9.4-changing-existing-systems).
