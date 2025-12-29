# Public Teams With Private Team Features

This project delivers a hybrid Microsoft Teams architecture that allows organization‑wide transparency while still protecting department‑specific confidential content. Each department receives a **Public Team** that anyone in the organization can join, paired with a **Secure** folder accessible only to that department’s members.

This structure mirrors the experience of walking up to a department’s area in a physical office—open, visible, and collaborative—while still maintaining strict control over sensitive files.

---

## Overview

The core objectives of this project were:

- Create a **Public Team** for every department.
- Provide each department with a **private, encrypted Secure folder**.
- Support hierarchical departments with multiple divisions.
- Automate access control using Microsoft 365 groups.
- Enforce encryption using sensitivity labels and Cloud App policies.
- Train administrators to maintain the structure long‑term.

The result is a scalable, secure, and user‑friendly Teams environment that balances openness with confidentiality.

---

## Phase 1: Creating Public Teams With Department‑Only Secure Spaces

I began by creating a Public Team for each department based on a curated list provided by project stakeholders. These Teams served as open collaboration spaces where anyone in the organization could join, view documentation, and interact with the department.

To support private departmental work, I created a **Secure** folder under the General channel of each Team. This folder was intended to be accessible only to the department’s internal members.

### Handling Hierarchical Departments

Some departments had multiple divisions (for example, a main “Finance” Team with several sub‑units). For these cases, I created additional channels to represent each division.

Because the root Team was public:

- Anyone could join the department’s Team.
- Division‑level documentation remained visible.
- Sensitive content stayed isolated inside the Secure folder.

---

## Phase 2: Restricting Secure Folder Access Using M365 Groups

Although the Secure folder existed inside a public Team, it needed to be accessible only to the appropriate department members. To accomplish this, I created dedicated Microsoft 365 groups for each department or division using a consistent naming convention (e.g., `Division‑Benefits`).

To ensure these groups functioned strictly as permission containers, I disabled:

- Teams functionality  
- Visibility in the Global Address List  
- External email delivery  
- User notifications when added to the group  

After creating each group, I navigated to the Secure folder’s permissions and removed all existing groups except **Owner**. I then added the newly created M365 group for that department or division.

This ensured that:

- The Team remained public  
- The General channel remained open  
- The Secure folder was restricted to authorized members only  

This structure provided a clean separation between public collaboration and private departmental work.

---

## Phase 3: Enforcing Security Through Sensitivity Labels and Cloud App Policies

To ensure the Secure folders were truly secure, we implemented **sensitivity labels with encryption**. Although the label was originally designed for detecting social security numbers, we used it specifically for its encryption capabilities.

### Automated Labeling With Cloud App Policies

I created a Cloud App policy that detects when a folder named **Secure** is created anywhere in the tenant. When detected, the policy either:

- Automatically applies the designated sensitivity label, or  
- Allows an administrator to manually add the folder to the policy, depending on the storage location (SharePoint or OneDrive)

For this project, I built a SharePoint‑specific policy that automatically encrypts supported Microsoft file types (such as XLSX, DOCX, and PDF) inside the Secure folder. The sensitivity label is applied at the folder level, and the Cloud App policy enforces encryption on all eligible content within it.

### Administrator Training and Ongoing Management

To ensure long‑term sustainability, I trained administrators on:

- How to add new Secure folders to the policy  
- How to manage policy allocation limits  
- How to handle deleted or replaced folders previously included in the policy  

This ensured the Secure folder model could scale across departments without requiring engineering intervention for every update.

---

## Outcome

This project delivered a hybrid model that combined:

- Public transparency  
- Department‑level privacy  
- Automated encryption  
- Scalable governance  

Departments gained a secure workspace without losing the benefits of open collaboration, and administrators gained a repeatable, maintainable structure for future growth.

---

## Future Enhancements

Potential next steps for expanding this architecture include:

- Automating M365 group creation with PowerShell  
- Auto‑provisioning Secure folders during Team creation  
- Expanding Cloud App policies to support additional file types  
- Implementing lifecycle policies for Secure folder content  

---

## Notes

- All Secure folders rely on sensitivity labels for encryption.  
- M365 groups used for permissions are hidden and non‑collaborative by design.  
- Administrators must maintain Cloud App policy mappings as new departments or divisions are added.
