# 📋 QA TESTING DOCUMENT

**Project Name:** FusionPay Retail Revamp
**Date:** July 31, 2025
**Prepared By:** Lead QA Engineer (AI Simulation)

---

## 🎯 Testing Summary & Strategy

This QA effort follows a blended Agile strategy combining:

* **User Acceptance Testing (UAT)** – for user story coverage
* **Regression Testing** – to protect core functionality
* **API Validation** – verifying request/response contract
* **Performance Checks** – focused on the payment gateway
* **Exploratory Testing** – targeting edge workflows

---

## 🖥️ Systems Under Test

* ✅ **Microsoft Dynamics D365 (Finance + Inventory Modules)**
* ✅ **Cloud-hosted POS (Tablet + Web Kiosk)**
* ✅ **FusionPay API Gateway**
* ✅ **Mobile App (iOS/Android hybrid)**
* ✅ **Azure Functions handling scheduled inventory jobs**

---

## 🧯 Known Pain Points

* Intermittent 504s from FusionPay API under load
* Item duplication bug during POS returns
* UI freezes on low-memory Android tablets
* Environment parity mismatch between staging and prod
* Incorrect tax logic when combining discounts + returns

---

## 🔧 Patch Notes

* **Patch 5.4.1**

  * Updated `/pay/auth` endpoint schema
  * Improved token refresh on mobile
  * Fixed async race condition in scheduler job
  * Patch impact: Payment timeout handling, backend schema v4.3

---

## 🧾 User Stories

1. **As a cashier**, I want to issue returns from POS so that customers can receive timely refunds.
2. **As a mobile app user**, I want to securely authenticate so that my saved wallet loads on login.
3. **As an inventory manager**, I want item syncs to reflect real-time stock so that I avoid overselling.
4. **As a support analyst**, I want logs to be human-readable so that I can triage issues faster.
5. **As a regional finance lead**, I want VAT to reflect jurisdiction so that tax audit risks are reduced.

---

## 🧪 Test Cases

### Story 1: POS Returns

| Test Case ID | Test Description                             | Expected Result                         | Pass/Fail | Comments |
| ------------ | -------------------------------------------- | --------------------------------------- | --------- | -------- |
| TC-001       | Valid item barcode scanned for return        | Item loads, refund shown, return logged |           |          |
| TC-002       | Barcode not found                            | Error: “Item not eligible for return”   |           |          |
| TC-003       | Return initiated without supervisor override | Permission error message shown          |           |          |
| TC-004       | Return >30 days old                          | Blocked per policy                      |           |          |
| TC-005       | API call logs in `POST /return/initiate`     | Status 200, refund payload correct      |           |          |

---

## 🛠 Bug Reproduction Template

```markdown
**Bug ID:** RET-502  
**Environment:** Android POS v3.8  
**Steps to Reproduce:**
1. Open POS app
2. Scan return barcode
3. Tap refund → UI freezes

**Expected:** Refund screen loads  
**Actual:** App stalls for 15+ seconds

**Screenshot/Logs Attached:** Yes
```

---

## 🖋️ Approval Block

| Role               | Name             | Signature | Date |
| ------------------ | ---------------- | --------- | ---- |
| Project Manager    | Jackson Teague   |           |      |
| QA Lead            | Maurice McDonald |           |      |
| IT Director        | Hina Desai       |           |      |
| Executive Approver | Lars Nyström     |           |      |

---

## 🧠 Format Notes (Markdown)

* This document is GitHub-readable
* Can be rendered in pull requests for review
* Easily convertible to `.docx` or `.pdf` using Pandoc
* If exporting to Jira or TestRail, copy test case rows to spreadsheet

---

Would you like me to now:

* Save this as `qa-docs/versions/v1.0.1/qa-testing-plan.md`?
* Push it to your repo with a PR and assign reviewers?
* Generate a `.csv`, `.docx`, or `.pdf` version for sharing?

Let me know how you'd like to proceed.
