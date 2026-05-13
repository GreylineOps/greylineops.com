---
date: "2026-05-13T01:00:00-07:00"
title: "CMMC and Cloud Services: What FedRAMP, Shared Responsibility, and CUI in the Cloud Actually Mean for Small DIB Businesses"
description: "Using cloud services to store or process CUI? Here's what CMMC actually requires, how FedRAMP fits in, what 'shared responsibility' means in practice, and the common mistakes small DIB contractors make."
---

# CMMC and the Cloud: What Small Defense Contractors Actually Need to Know

_Posted by GreylineOps | Cybersecurity & Compliance_

---

A lot of small defense contractors have moved to the cloud over the last few years — Microsoft 365 for email and collaboration, cloud file storage, maybe some SaaS tools for project management or engineering work. It's convenient, cost-effective, and usually better-managed than running your own servers.

The problem is that most of those businesses haven't thought carefully about what happens when **Controlled Unclassified Information (CUI) touches a cloud service**. And under CMMC, that question matters a lot.

This post cuts through the confusion around cloud services, FedRAMP authorization, and shared responsibility — so you understand exactly what you're on the hook for before an assessor starts asking.

---

## The Core Issue: Not All Cloud Services Are Created Equal for CUI

When CUI lives in the cloud, you're not just responsible for your own security practices — you're also responsible for choosing cloud services that meet the government's security requirements.

DFARS 252.204-7012, the clause that appears in most defense contracts involving CUI, requires that cloud services used to process, store, or transmit CUI meet **security requirements equivalent to FedRAMP Moderate**.

That's not optional language. If you're using a cloud service for CUI that doesn't meet this standard, you have a compliance gap — regardless of how well-configured everything else in your environment is.

---

## What Is FedRAMP, and Why Does It Matter?

**FedRAMP (Federal Risk and Authorization Management Program)** is the federal government's standardized process for authorizing cloud services. A cloud provider that achieves FedRAMP authorization has had its security controls independently assessed against NIST SP 800-53 baselines.

There are three impact levels:

- **FedRAMP Low** — for non-sensitive data
- **FedRAMP Moderate** — the baseline for most CUI
- **FedRAMP High** — for the most sensitive government data
  For DIB contractors, **FedRAMP Moderate** is the relevant standard. If a cloud service you're using to handle CUI doesn't have at least FedRAMP Moderate authorization, it doesn't meet the requirements under DFARS 7012.

The good news: major platforms have done this work. **Microsoft 365 GCC** (Government Community Cloud) is FedRAMP Moderate authorized. So is **Microsoft Azure Government**, **AWS GovCloud**, and **Google Workspace for Government**. The challenge for small businesses is that these are different products than the standard commercial versions — and they come with different configurations, pricing, and feature sets.

Standard Microsoft 365 Business Premium? **Not FedRAMP authorized.** Google Workspace standard? **Not FedRAMP authorized.** That distinction trips up a lot of small contractors.

---

## The Shared Responsibility Model: What It Actually Means

Cloud providers love to talk about "shared responsibility." Here's what that means in plain terms.

The cloud provider is responsible for securing **the infrastructure** — the physical data centers, the networking hardware, the hypervisor layer, the underlying platform services. They handle that.

You are responsible for securing **everything you put on top of that infrastructure** — your data, your user accounts, your configurations, your access controls, and your compliance with regulations like CMMC.

The mistake small businesses make is assuming that because a cloud service is FedRAMP authorized, they're automatically compliant. They're not. FedRAMP authorization means the platform _can_ be used for CUI in a compliant way — it doesn't mean your specific deployment _is_ compliant.

Here's a simple example. Microsoft 365 GCC is FedRAMP Moderate authorized. But if you configure it with:

- No multi-factor authentication
- Sharing permissions that allow external access to CUI files
- No audit logging enabled
- Guest access turned on in Teams
  ...then your deployment is non-compliant regardless of the platform's authorization status. The security controls that CMMC requires — MFA, access control, audit logging, CUI handling procedures — still have to be implemented _by you_, in your tenant configuration.

---

## What CMMC Actually Requires for Cloud Services

At **CMMC Level 2**, the relevant controls come from NIST SP 800-171. Several of them directly govern how cloud services must be configured and managed:

| Control           | What It Requires                             | Cloud Implication                                                                           |
| ----------------- | -------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **3.1.1 / 3.1.2** | Limit system access; enforce least privilege | Users should only have access to CUI they need; admin accounts should be tightly controlled |
| **3.3.1 / 3.3.2** | Create and retain audit logs                 | Logging must be enabled in your cloud tenant and logs retained per policy                   |
| **3.5.3**         | Multi-factor authentication                  | MFA required on all accounts that access CUI — no exceptions                                |
| **3.13.1**        | Boundary protection                          | CUI cloud environments should be segmented from non-CUI systems                             |
| **3.13.16**       | Protect CUI at rest                          | Encryption at rest must be enabled for CUI storage                                          |

Beyond these, DFARS 7012 adds a specific requirement: if a cloud service is involved in a cyber incident affecting CUI, you must be able to **preserve images of your cloud environment** and provide them to DoD within 72 hours of a request. That means your cloud provider needs to support that capability — and you need to know how to execute it.

---

## The GCC vs. GCC High Question

If you're using Microsoft 365, this is a question you'll face: **GCC or GCC High?**

**Microsoft 365 GCC** is designed for federal, state, and local government contractors. It's FedRAMP Moderate authorized and meets the baseline for most DIB contractors handling standard CUI.

**Microsoft 365 GCC High** is designed for contractors working with more sensitive data — particularly data subject to ITAR (International Traffic in Arms Regulations) or EAR (Export Administration Regulations). It's FedRAMP High authorized and includes additional controls around data residency and access by Microsoft personnel.

The practical question: if your CUI includes export-controlled technical data, engineering drawings, or program information under ITAR/EAR, you may be required to use GCC High rather than GCC. This is something to confirm with your contracting officer and verify in your contract language.

GCC High is meaningfully more expensive than GCC, and it limits some third-party integrations. Many small businesses either don't know they need it — or know they need it and are hoping no one asks. Under a C3PAO assessment, someone will ask.

---

## Common Cloud Compliance Mistakes

**Using standard commercial Microsoft 365 or Google Workspace for CUI.** The standard commercial versions of these platforms are not FedRAMP authorized. If CUI lives in a standard M365 or Google Workspace tenant, that's a compliance gap.

**Assuming FedRAMP authorization means you're done.** Authorization means the platform is eligible for compliant use. Your configuration still has to implement the required controls.

**No CUI labeling or handling policies for cloud files.** CUI that gets uploaded to SharePoint or OneDrive needs to be labeled, access-controlled, and governed by a documented handling policy. Most small businesses have none of this in place.

**Sharing CUI with external users via cloud platforms.** Guest access, external sharing links, and collaboration features are useful — and easy to misconfigure in ways that expose CUI to people who shouldn't have it. Assessors will check sharing settings.

**Not retaining or reviewing audit logs.** Cloud platforms generate extensive audit logs, but they're often not configured for the right retention period, not exported to a SIEM, and not being reviewed by anyone. All three of those are findings.

**Using SaaS tools without checking their authorization status.** Project management tools, file transfer services, video conferencing platforms — if CUI passes through them, their authorization status matters. Many popular SaaS tools have no FedRAMP authorization at all.

---

## A Practical Starting Point

If you're not sure where your cloud environment stands, here are the four questions to ask right now:

1. **Which cloud services does CUI touch?** Map it out. Email, file storage, collaboration tools, any SaaS platform where CUI might be uploaded or discussed.
2. **Does each of those services have at least FedRAMP Moderate authorization?** Check the [FedRAMP marketplace](https://marketplace.fedramp.gov) — it's publicly searchable.
3. **Is your tenant configuration actually implementing the required controls?** MFA, logging, access controls, encryption settings. Don't assume — verify.
4. **Do you have documented policies for CUI handling in cloud environments?** Your SSP needs to describe this. If there's no written policy, that's a gap before you even look at the technical controls.

---

## The Bottom Line

The cloud isn't inherently a CMMC problem — plenty of small DIB contractors run compliant cloud environments. But "compliant" requires more than picking the right platform. It requires the right product tier (GCC, not commercial M365), the right configuration (MFA, logging, access controls actually turned on), and the right documentation (policies, procedures, and SSP language that reflect how CUI actually moves through your environment).

If your cloud environment was set up by a general IT provider without CMMC in mind, there's a reasonable chance it has gaps. The time to find those gaps is before a C3PAO assessment — not during one.

---

_This post is for informational purposes. CMMC requirements and assessment standards continue to evolve. If you're ready to evaluate your specific compliance posture, [GreylineOps](https://GreylineOPS.com) is a CMMC-specialized RPO built for small DIB businesses — [reach out for a readiness consultation](/pre-qual/) and we'll help you figure out exactly where you stand._
