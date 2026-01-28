# Online Student Enrollment Automation (Zapier + Google Sheets + Email)

## Overview

This case demonstrates an automated onboarding workflow for **online students** at a higher-education institution. The goal was to reduce manual coordination between academic operations and IT by automatically triggering enrollment communications and tracking onboarding status as soon as student data is entered or updated.

The workflow was designed and implemented using **Zapier**, **Google Sheets**, and **email automation**, with initial plans to include **Zoom registration** as part of the onboarding process.



## Problem Statement

Online programs require fast, accurate onboarding so students receive timely access to course resources and communications. In many institutions, this process is still manual:

* Staff monitor spreadsheets for new enrollments
* Emails are sent individually or in batches
* Status updates are tracked inconsistently
* Errors are hard to detect or recover from

This creates delays, missed communications, and unnecessary operational overhead.



## Initial Design (Planned Architecture)

### **Trigger**

* New row added or existing row updated in Google Sheets (`Online_Student_Enrollments`)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%201.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%202.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%203.png?raw=true)

### **Planned Actions**

#### 1. Register student for a Zoom session (orientation or class)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%204.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%205.png?raw=true)
#### 2. Send enrollment confirmation email

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%206.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%207.png?raw=true)
#### 3. Update enrollment status in the spreadsheet

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%208.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%209.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%2010.png?raw=true)

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%2011.png?raw=true)

#### 4. Log timestamp for audit and follow-up


## Implementation Challenge & Debugging

During implementation, I discovered that **Zoom meeting registration was not enabled** for the target meeting, which caused the Zoom action to fail during testing.

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%2012.png?raw=true)

### How this was handled:

* Confirmed the failure was not related to authentication or API permissions
* Identified that Zoom meeting settings prevented registration actions
* Removed the Zoom registration step after validation
* Adjusted the workflow to preserve a stable, production-ready automation

This decision prioritized **reliability and correctness** over forcing an incomplete integration.



## Final Working Solution (Published Zap)

The published Zap implements a **fully functional and fault-tolerant workflow**:

### Trigger

* **New or updated row** in the Google Sheets enrollment table

### Actions

1. **Send registration email** to the student confirming enrollment and next steps
2. **Lookup the same row** using previous data inputs to ensure correct record targeting
3. **Update a field in the original table** (e.g., Enrollment Status or Processed Timestamp) to prevent duplicate processing

This creates a closed-loop system where:

* Every enrollment is acknowledged
* Processing status is visible at a glance
* Repeat triggers are safely avoided

![](https://github.com/joesghub/itsm_support_cases/blob/main/zapier/imgs/zap%2013.png?raw=true)


## Key Design Decisions

* Used row lookups instead of relying solely on trigger payloads to ensure data consistency
* Explicitly updated the source spreadsheet to create idempotent behavior
* Removed fragile integrations once root cause was identified
* Published only after end-to-end testing confirmed stable execution



## Tools Used

* **Zapier**
* **Google Sheets**
* **Email automation (Zapier Email / Gmail)**
* **Zoom (initial integration tested, not included in final Zap)**



## Evidence & Documentation

This repository includes **13 screenshots** documenting:

* Trigger configuration
* Action setup
* Failed Zoom registration test
* Successful email delivery
* Row lookup logic
* Field updates in the source spreadsheet
* Final Zap publish confirmation

These screenshots serve as both **proof of implementation** and **debugging memory**.



## Outcome

* Eliminated manual monitoring of enrollment spreadsheets
* Ensured every new or updated enrollment triggers a consistent response
* Created a reusable automation pattern suitable for other academic workflows
* Demonstrated structured debugging and decision-making under real platform constraints



## Next Steps

* Re-enable Zoom registration once meeting settings support automated registration
* Extend workflow to include calendar invites or LMS provisioning
* Apply the same pattern to hybrid and interdepartmental use cases


