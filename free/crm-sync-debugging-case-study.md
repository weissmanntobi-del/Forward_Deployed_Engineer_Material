# Case Study: Debugging a CRM Sync Failure in Production

## Overview

This case study shows how a Forward Deployed Engineer might approach a real-world customer problem:

> “The CRM sync worked perfectly in the demo, but now it is failing in production.”

This is one of the most common types of problems in customer-facing engineering.

In a demo environment, everything often looks clean and predictable.

In production, the system meets real customer data, real API limits, real user behavior, real permissions, and real business pressure.

That is where Forward Deployed Engineers are tested.

---

## The Scenario

A B2B SaaS company built an AI-powered lead enrichment feature.

The product takes lead data from a customer’s internal application, enriches it with AI-generated insights, and syncs the result into Salesforce.

During the demo, the integration worked well.

The customer saw:

- Lead records enriched successfully
- AI-generated summaries added to CRM fields
- Account information updated correctly
- No visible errors
- Fast sync performance

The customer approved the pilot and asked to move the integration into production.

But after going live, the sync started failing.

---

## Customer Message

The customer sends this message:

> “The CRM sync worked in the demo, but now production is failing for many records. Our sales team depends on this data for tomorrow’s pipeline review. Can you fix it urgently?”

This is not only a technical problem.

It is also a customer trust problem.

The Forward Deployed Engineer needs to debug the issue, reduce customer anxiety, communicate clearly, and create a reliable fix.

---

## Initial Symptoms

The team observes the following problems:

| Symptom | Description |
|---|---|
| Failed API calls | Some Salesforce API requests fail |
| Partial sync | Some records sync successfully while others fail |
| Poor error messages | The system only says `Sync failed` |
| Slow performance | Large sync batches take too long |
| Customer pressure | Sales leadership needs the data urgently |
| Environment mismatch | Demo worked, production fails |

At first glance, the issue looks like a simple integration bug.

But production issues are rarely that simple.

---

## Why the Demo Worked

The demo worked because the environment was controlled.

The demo used:

- Clean sample data
- Small number of records
- Known field values
- Stable API credentials
- Limited sync volume
- No real user pressure
- No production validation complexity

The demo proved that the happy path worked.

But production tested the unhappy paths.

---

## Why Production Failed

Production introduced realities that were not visible during the demo.

### 1. Messy Data

Some real customer records had:

- Missing company names
- Invalid email addresses
- Empty phone numbers
- Unexpected country values
- Duplicate records
- Very long text fields
- Special characters
- Inconsistent capitalization
- Invalid CRM field formats

Example:

```json
{
  "lead_id": "L-10291",
  "company": "",
  "email": "john@@example",
  "country": "Deutschland",
  "crm_owner_id": null
}