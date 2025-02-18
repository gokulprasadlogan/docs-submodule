# Bug Fix Proposal Document

## Title: Add Version Information in Profile Pop-up

## Issue Summary
- The profile pop-up does not display the app version on the following devices:
  - Android Mobile
  - Android Tablet
  - iPhone
  - iPad 13
  - iPad 11

## Steps to Reproduce
1. Open the app on any of the mentioned devices.
2. Navigate to the profile section.
3. Open the profile pop-up.
4. Observe that the app version is missing.

## Expected Behavior
- The profile pop-up should display the app version on all the specified devices.

## Actual Behavior
- The app version is missing from the profile pop-up.

## Root Cause Analysis
- The profile pop-up component does not currently include a version information field.
- The version retrieval logic is not implemented in the UI.
- The issue occurs across multiple devices, indicating a missing feature rather than a device-specific bug.

## Proposed Fix
- Fetch the app version from the AppVersion coponent used for Auto Update Feature.
- Display the app version in the profile pop-up UI.(Code available in Swami Feeds project)
- Ensure proper alignment and visibility across all screen sizes.

## Affected Components
- MenuFooter    
- ButtomMoreMenuList

## Definition of Done
- [ ] The app version is displayed in the profile pop-up.
- [ ] The fix is tested on the following devices:
  - [ ] Android Mobile
  - [ ] Android Tablet
  - [ ] iPhone
  - [ ] iPad 13
  - [ ] iPad 11
- [ ] The version information is correctly aligned and visible.
- [ ] No UI distortions or overlaps occur due to the change.
- [ ] Code is reviewed and merged into the main branch.
- [ ] A new build is generated and verified.

## Test Cases
| Test Case ID | Description | Expected Result | Status |
|-------------|-------------|----------------|--------|
| TC-001 | Open profile pop-up on Android Mobile | Version is displayed | Pending |
| TC-002 | Open profile pop-up on Android Tablet | Version is displayed | Pending |
| TC-003 | Open profile pop-up on iPhone | Version is displayed | Pending |
| TC-004 | Open profile pop-up on iPad 13 | Version is displayed | Pending |
| TC-005 | Open profile pop-up on iPad 11 | Version is displayed | Pending |

## Risks and Mitigation
- **Risk**: UI misalignment on different screen sizes.
  - **Mitigation**: Ensure responsive design and thorough testing.
- **Risk**: Version retrieval might not work correctly on some devices.
  - **Mitigation**: Test version fetching on all targeted platforms.

