# Bug Fix Proposal Document - Bug Ignorance

### 1. Title
**Bug Title**: App Navigates to Home Page After Returning from Background When Opening Report from Notification, Instead of Staying on the Current Page After File Download Completion

**Version**: 1.0

**Date**: February 7, 2025

---

### 2. Objective
The objective of this document is to propose ignoring the bug where the app navigates to the home page after returning from the background when opening a report from a notification. This bug occurs only on devices running Android versions lower than 12, while it works as expected on Android 12+ and on iPhone/iPad.

---

### 3. Reason for Ignoring the Bug
The bug occurs only on older Android versions (below Android 12) and does not affect the functionality or user experience on newer Android versions and iOS devices. Since Android 12+ devices and iOS devices behave as expected, the issue is limited to a small user base with older Android versions. Addressing the issue for such a specific case may not be a priority given the overall usage distribution.

---

### 4. Scope
- **Included**:  
    - Ignoring the bug and determining that no immediate action is required to fix it.
    - No changes will be made to the current navigation logic for this specific bug.
- **Not Included**:  
    - Any investigation into backward compatibility with Android versions below 12.
    - No changes to the app's behavior or navigation logic unless a broader impact is identified.

---

### 5. Reason for Not Fixing
- **Limited User Impact**: The bug only affects users on older Android versions (below Android 12), which represent a decreasing percentage of the user base. Users on these devices will still be able to use the app, with the only issue being navigation behavior.
- **Platform Updates**: Android 12 and above have already improved behavior related to background/foreground transitions, and iOS devices do not exhibit this issue.

---


### 6. Testing Plan
No further testing is required since the issue will not be fixed. Testing efforts will continue to focus on ensuring the app works well on Android 12+ and iOS devices.



