# Google Play Data Safety Form

This guide ensures that your integration of the Trophée SDK meets **Google Play Store** compliance requirements.

&#x20;Follow the steps below to ensure your implementation is fully compliant and ready for deployment.<br>

Below is the **data table** for Data Collected and their purpose served in the Trophée SDK:

| **Category**         | **Data Collected**                                     | **Purpose**                 | **Shared?** | **Retention & Security** |
| -------------------- | ------------------------------------------------------ | --------------------------- | ----------- | ------------------------ |
| **App Activity**     | `ApplicationBundle`                                    | Analytics & Performance     | ❌ No        | ✅ Encrypted, 12 months   |
| **Device IDs**       | `deviceUniqueIdentifier`, `AdvertisingId`              | Ad Personalization          | ✅ Yes (Ads) | ✅ Encrypted, 12 months   |
| **Device Info**      | `deviceModel`, `deviceType`, `os_version`, `userAgent` | SDK Optimization            | ❌ No        | ✅ Encrypted, 12 months   |
| **User Information** | `ip`                                                   | Fraud Prevention & Security | ❌ No        | ✅ Encrypted, 6 months    |



### **Google Play Data Safety Form (Pre-Filled Template for Trophée SDK)**

#### **1. Does your app collect or share any of the required user data types?**

✅ **Yes**

***

#### **2. Is all user data collected, processed, and handled securely?**

✅ **Yes, all sensitive data is encrypted in transit and stored securely.**

***

#### **3. Do you share user data with third parties?**

✅ **Yes, for advertising and analytics purposes.**

* We share data only with **authorized third-party ad networks and analytics providers**.
* Users can opt-out of personalized ads via **Google Ads settings** or our in-app consent preferences.

***

### **4. Data Types Collected by Trophée SDK (See Above Mentioned Table)**&#x20;

### **5. Is this data collected for required functionality or optional features?**

✅ **Some data is necessary for core SDK functionality, while others enhance ad targeting and analytics.**

| **Required Data**                                      | **Purpose**                                        |
| ------------------------------------------------------ | -------------------------------------------------- |
| `deviceUniqueIdentifier`, `AdvertisingId`              | Required for ad personalization & tracking         |
| `deviceModel`, `os_version`, `os`, `ApplicationBundle` | Required for SDK optimization & game compatibility |
| `ip`                                                   | Used for security and fraud detection              |

***

### **6. Does the app allow users to request data deletion?**

✅ **Yes, users can request data deletion via the Trophée privacy policy page or in-app settings.**



**Additional Compliance:**

* Implement **Google Consent Mode** for GDPR and CCPA compliance.
* Allow **data deletion requests** via the privacy policy.

## **Best Practices for SDK Integration**

### &#x20;**Installing Trophée SDK**

**Implementation Steps:**

1. **Import the latest SDK** into your project.
2. **Initialize the SDK** with required permissions.
3. **Run performance tests** after integration.

### **Implementing Ads & Monetization**

**Implementation Steps:**

1. **Set up ad placements** in-game.
2. **Run A/B tests for ad optimization**.

### **Compliance Submission Process**

**Implementation Steps:**

1. **Upload SDK version for review**.
2. **Address flagged issues before going live**.



***
