# 🖥️ Remote Desktop Login Authorization Troubleshooting Guide

---

## 📘 Overview

This document provides step-by-step instructions to resolve the common Remote Desktop error:

> **“The connection was denied because the user account is not authorized for remote login.”**

This issue typically occurs when the user is not part of the required Remote Desktop or security groups, or when Remote Desktop Services are not properly configured.

---

## ⚙️ Root Cause

One or more of the following issues may cause the remote login failure:

1. The user is **not a member of the Remote Desktop Users group**.
2. The user is **not granted permission** in the local security policy.
3. The **Remote Desktop Services** configuration is incorrect.

---

## 🧩 Resolution Steps

### **Step 1: Verify Remote Desktop Users Group Membership**

1. On the target server or computer, **right-click** `This PC` → select **Manage**.
2. Navigate to:

   ```
   Computer Management > Local Users and Groups > Users
   ```
3. Locate the affected user (e.g., **Xitiz Basnet**).
4. Double-click the username and open the **Member Of** tab.
5. Check if **Remote Desktop Users** is listed.

   * If **not listed**, follow these steps:

     * Click **Add** → **Advanced** → **Find Now**.
     * Select **Remote Desktop Users** → **OK** → **OK**.
6. Confirm the user now appears as part of **Remote Desktop Users**.
7. Click **Apply** → **OK**.

---

### **Step 2: Add User to Security Policy**

1. On the desktop, press **Windows + S** and search for **Local Security Policy**.
2. Navigate to:

   ```
   Security Settings > Local Policies > User Rights Assignment
   ```
3. Locate and double-click **Allow log on through Remote Desktop Services**.
4. Select **Add User or Group** → **Advanced** → **Find Now**.
5. Choose the relevant user (e.g., **Xitiz Basnet**) → **OK** → **OK**.
6. Apply the changes and click **OK** again.

---

### **Step 3: Verify Remote Desktop Services Configuration**

1. Search for **Services** from the Start Menu and open it.
2. Locate **Remote Desktop Services**.
3. Right-click → **Properties**.
4. Ensure **Startup type** is set to **Manual** (or **Automatic** if your policy requires).
5. Go to the **Log On** tab.
6. Ensure **This account** is set to `Network Service`.

   * If it is not:

     * Click **Browse** → **Advanced** → **Find Now**.
     * Select **Network Service** → **OK** → **OK**.
7. Click **Apply** → **OK** to save the configuration.

---

## 🔁 Final Step

1. **Restart the computer or server.**
2. Once restarted, the user should be able to connect via Remote Desktop successfully.

---

## ✅ Verification

After completing the above steps:

* The user should be listed under **Remote Desktop Users**.
* The user should appear in **Local Security Policy → Allow log on through Remote Desktop Services**.
* The **Remote Desktop Services** should be running with the correct configuration.

---

## 🧠 Notes

* Always ensure RDP access complies with your organization’s **security policy**.
* Apply **least privilege** principles when granting remote login permissions.
* Document every change in your IT maintenance log or Git commit for traceability.

---

