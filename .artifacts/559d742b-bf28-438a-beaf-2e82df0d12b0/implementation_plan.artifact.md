# Fix Atomic Age Font Visibility

The font "Atomic Age" is not appearing because of a parsing issue in `ResourcesCompat` while loading the downloadable font XML. The logcat indicates `Failed to find font-family tag`, which often occurs when `AppCompat` components (using `ResourcesCompat`) expect downloadable font attributes in the `app` namespace rather than the `android` namespace, even on newer API levels.

## User Review Required

> [!IMPORTANT]
> Downloadable fonts require an active internet connection and Google Play Services to be installed and configured on the device or emulator. Please ensure your device has internet access and Google Play Store support.

## Proposed Changes

### [Resources]

#### [MODIFY] [atomic_age.xml](file:///C:/Users/18pie/OneDrive/Documents/College Work/Year 3/Sem2/OSC/UI Practice/app/src/main/res/font/atomic_age.xml)
Update the font family definition to use the `app` namespace for provider attributes. This ensures compatibility with `ResourcesCompat` and fixes the parsing error.

#### [MODIFY] [activity_main.xml](file:///C:/Users/18pie/OneDrive/Documents/College Work/Year 3/Sem2/OSC/UI Practice/app/src/main/res/layout/activity_main.xml)
Add `app:fontFamily` to the `TextView` to ensure the `AppCompat` inflation correctly handles the downloadable font.

## Verification Plan

### Automated Tests
- Run the app and check for `ResourcesCompat` errors in logcat.
- The build already passes, ensuring XML syntax is correct.

### Manual Verification
- Deploy the app to a device with Google Play Services.
- Verify that the "Atomic Age" font is applied to the welcome message.
