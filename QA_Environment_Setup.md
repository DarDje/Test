
## 1. Installing Flutter SDK and Preparing the Local Environment

### Description

To get started, a QA engineer needs to set up a working environment to run and test a Flutter application. This includes installing the SDK (Software Development Kit), configuring the PATH environment variable, and verifying that all dependencies are properly installed.

### Detailed Steps

**Step 1. Download the Flutter SDK**

1. Visit the official Flutter website: [flutter.dev](https://flutter.dev).
2. Select your operating system (Windows, macOS, or Linux).
3. Click the Download button and download the Flutter SDK archive (usually a .zip file).

**Tip:**

* For Windows: Extract the archive to `C:\src\flutter` (recommended).
* For macOS/Linux: Choose any convenient directory, for example, `~/development/flutter`.


**Step 2. Extract the SDK Archive**

* For Windows: Use the built-in Windows File Explorer (Right-click → Extract All...) or WinRAR/7-Zip.
* For macOS/Linux: Open a terminal and run:

```bash
unzip flutter_macos_3.x.x-stable.zip
```


**Step 3. Set the PATH Environment Variable**
Why is this important?
So you can run Flutter commands from anywhere in the terminal or command prompt.

**For Windows:**

1. Press Win + R, type `sysdm.cpl`, and press Enter.
2. Go to the Advanced tab and click **Environment Variables**.
3. Find the **Path** variable and click **Edit**.
4. Add the new path, for example: `C:\src\flutter\bin`.
5. Click **OK**.

**For macOS/Linux:**

1. Open a terminal.
2. Run the following command (assuming Flutter is in `~/development/flutter`):

```bash
export PATH="$PATH:`pwd`/flutter/bin"
```

To make this PATH change permanent, add this line to your shell configuration file (`~/.bash_profile` or `~/.zshrc` for Zsh):
Example:

```bash
echo 'export PATH="$PATH:$HOME/development/flutter/bin"' >> ~/.bash_profile
source ~/.bash_profile
```


**Step 4. Verify the Installation**

1. In the terminal or command prompt, run:

```bash
flutter doctor
```

This command checks your Flutter installation and shows the status of all necessary components.

**Example output:**

```
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 3.x.x)
[✓] Android toolchain - develop for Android devices
[✓] Xcode - develop for iOS and macOS (on Mac)
[✓] Chrome - develop for the web
[✓] Android Studio
[✓] Connected device (1 available)
```


**Step 5. Verify All Dependencies**
Ensure that all items in the `flutter doctor` output have a green checkmark `[✓]`.
If any items are marked with `[✗]`, follow the console instructions to install the missing components.

What to check:

* Flutter SDK
* Dart SDK
* Android Studio (for Android)
* Xcode (for macOS/iOS)
* Connected devices (emulators or physical devices).


### Documentation for This Step

What to include:

* A screenshot of the terminal or command prompt showing the output of:

```bash
flutter doctor
```

* A screenshot of the `.bash_profile`, `.zshrc`, or Windows PATH with the added Flutter path.
  Example:

```bash
export PATH="$PATH:$HOME/development/flutter/bin"
```

### Tips

* It’s a good idea to note the Flutter SDK version (for example, 3.10.5).
* If you’re using macOS, make sure that Xcode and Command Line Tools are installed; otherwise, iOS tests may not run.
* If the PATH variable doesn’t work right away, restart the terminal or your computer.

## 2. Setting Up the Android Emulator

### Description

The Android Emulator allows you to test your app on a virtual device without using a physical smartphone. This is especially useful for QA when verifying functionality across different Android versions and devices.


### Detailed Steps

### Step 1. Install Android Studio

If you don’t have Android Studio installed:

1. Download the installer from the official site: [developer.android.com/studio](https://developer.android.com/studio).
2. Follow the on-screen instructions to install the software.
ё

### Step 2. Launch Android Studio

1. Open Android Studio.
2. Navigate to Tools → AVD Manager.
   AVD Manager is the tool used to create and manage emulators.


### Step 3. Create a Virtual Device (Emulator)

1. Click Create Virtual Device.
2. Choose a device model (e.g., Pixel 5).
3. Click Next.


### Step 4. Select an Android System Image

1. In the list of available versions, select a current image, such as:

* API Level 33 (Android 13)
* Choose the one labeled "Recommended."

2. Click Download and wait for the download to complete.
3. Click Next.


### Step 5. Configure the Device Parameters

1. Set the emulator’s parameters:

* RAM: at least 2048 MB (2 GB).
* Resolution: 1080x2340 (default for Pixel 5).
  Other settings can remain at default.

2. Click Finish.


### Step 6. Launch the Emulator

1. In AVD Manager, click the green Run button.
2. Wait for the device to fully boot.
   The first launch may take longer—this is normal.

You can also launch the emulator from the terminal:

```bash
emulator -avd Pixel_5_API_33
```


### Step 7. Verify Device Connectivity

1. Open the terminal.
2. Run:

```bash
flutter devices
```

Your emulator should appear in the list of connected devices.


### Documentation:

What to include:

* Screenshots of the AVD Manager settings window.
* The name of the created device and Android version (API Level).
  Example: Pixel\_5\_API\_33.


## 3. Setting Up the iOS Simulator (for macOS)

### Description

The iOS Simulator lets you test your app on Apple devices without using a physical device.


### Detailed Steps

### Step 1. Make Sure Xcode Is Installed

If you don’t have Xcode installed:

1. Download it from the App Store.
2. Launch Xcode and wait for all components to load.


### Step 2. Download the Latest Simulator

1. In Xcode, go to Preferences (Cmd + ,) → Components tab.
2. In the list of simulators, select one, for example:

* iOS 16+ (iPhone 14)

3. Click Download and wait for the installation to finish.


### Step 3. Launch the iOS Simulator

1. In Xcode, navigate to Xcode → Open Developer Tool → Simulator.
2. A simulator window should open with your chosen device.


### Step 4. Verify Device Connectivity

1. Open the terminal.
2. Run:

```bash
flutter devices
```

Your iOS Simulator should appear in the list of connected devices.


### Documentation:

What to include:

* Screenshot of the Xcode Preferences (Components tab).
* The iOS Simulator version (e.g., iOS 16).


## 4. Setting Up Testing Frameworks

### Description

Flutter supports both unit tests (checking individual functions) and integration tests (checking the app as a whole).


### Detailed Steps

### Step 1. Add Dependencies in `pubspec.yaml`

Open the `pubspec.yaml` file and add:

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  integration_test:
    sdk: flutter
```

Don’t forget to run:

```bash
flutter pub get
```


### Step 2. Run Unit Tests

Run the following command:

```bash
flutter test
```


### Step 3. Configure Integration Tests

1. In the project root, create a folder called `integration_test`.
2. Add an example test file:

```dart
import 'package:integration_test/integration_test.dart';
import 'package:flutter_test/flutter_test.dart';

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('Sample test', (tester) async {
    // Example test scenario
  });
}
```


### Step 4. Run Integration Tests

```bash
flutter test integration_test/
```

### Documentation:

What to include:

* Sample `pubspec.yaml` file.
* Sample test template.
* Screenshots or terminal output.

## 5. Setting Up Patrol or Maestro

### Description

These tools help automate end-to-end testing.

### Steps for Patrol

1. Install the dependency:

```bash
dart pub add patrol
```

2. Build the app:

```bash
dart run patrol build ios/android
```

3. Run the tests:

```bash
dart run patrol test
```


### Steps for Maestro

1. Download the Maestro CLI:

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```

2. Create a `maestro.yaml` file:

```yaml
flows:
  - name: Login Flow
    steps:
      - tapOn: "Login"
      - inputText: "username" into: "Username Field"
      - inputText: "password" into: "Password Field"
      - tapOn: "Submit"
```

3. Run the tests:

```bash
maestro test
```

### Documentation:

What to include:

* Example `maestro.yaml` file.
* Screenshots of successful test runs.
* Output logs.

---

## Script to Run Tests Across Multiple Devices

```bash
#!/bin/bash
# Flutter test script

echo "Starting Android Emulator..."
emulator -avd Pixel_5_API_33 &

sleep 30  # Wait for the emulator to boot

echo "Running unit tests..."
flutter test

echo "Running integration tests..."
flutter test integration_test/

# (Optional) Run Patrol
# dart run patrol test

# (Optional) Run Maestro
# maestro test

echo "Testing complete."
```

---

## List of Tools, Dependencies, and Versions

| Tool/Library        | Version               |
| ------------------- | --------------------- |
| Flutter SDK         | 3.x.x (latest stable) |
| Dart SDK            | 3.x.x                 |
| Android Studio      | Flamingo (or latest)  |
| Xcode               | 15.x.x                |
| Android Emulator    | API 33                |
| iOS Simulator       | iOS 16+               |
| Patrol              | Latest                |
| Maestro             | Latest                |
| Node.js (for CI/CD) | 18.x                  |

---

Note:
It’s recommended to store documentation in your QA repository in folders like:

* `docs/environment-setup/`
* `docs/test-cases/`
* `docs/scripts/`


## CI/CD Documentation for Flutter QA

**Goal**
Ensure automatic execution of tests after each commit or pull request to improve transparency and reduce manual QA efforts.

**Recommended Pipeline Structure (GitLab CI/CD)**
Example `.gitlab-ci.yml`:

```yaml
stages:
  - build
  - test
  - deploy

variables:
  FLUTTER_CHANNEL: "stable"

before_script:
  - apt-get update && apt-get install -y curl git unzip xz-utils zip libglu1-mesa
  - git clone https://github.com/flutter/flutter.git -b $FLUTTER_CHANNEL
  - export PATH="$PATH:`pwd`/flutter/bin"
  - flutter doctor

build_app:
  stage: build
  script:
    - flutter pub get
    - flutter build apk

unit_tests:
  stage: test
  script:
    - flutter test

integration_tests:
  stage: test
  script:
    - flutter drive --target=test_driver/app.dart

# (Optional) Run Patrol
patrol_tests:
  stage: test
  script:
    - dart run patrol test

# (Optional) Run Maestro
maestro_tests:
  stage: test
  script:
    - maestro test
```

**Recommendations:**

* Configure artifacts to store test reports:

```yaml
artifacts:
  paths:
    - test_reports/
  when: always
```

* Add notifications (Slack, Email) to notify the team of test results.
* For macOS CI, consider using GitHub Actions (macOS runner) or Bitrise.

## 2. Test Report Templates

### Manual Test Report Template

| Test ID | Test Name                    | Steps to Reproduce                                           | Expected Result                        | Actual Result | Status (Pass/Fail) | Notes       |
| ------- | ---------------------------- | ------------------------------------------------------------ | -------------------------------------- | ------------- | ------------------ | ----------- |
| TC01    | Login with valid credentials | 1. Open app <br> 2. Enter login/password <br> 3. Tap "Login" | User successfully logs in              | PASS/FAIL     | PASS               | —           |
| TC02    | Login error                  | 1. Open app <br> 2. Enter invalid data <br> 3. Tap "Login"   | Error message "Invalid login/password" | FAIL          | FAIL               | App crashes |


### Automated Test Report Template

| Test ID | Test Name         | Environment | Device/Emulator  | Result | Logs                        | Screenshots                      |
| ------- | ----------------- | ----------- | ---------------- | ------ | --------------------------- | -------------------------------- |
| ATC01   | Unit Tests        | GitLab CI   | Android Emulator | PASS   | logs/unit\_tests.log        | screenshot/unit\_tests.png       |
| ATC02   | Integration Tests | GitLab CI   | iOS Simulator    | FAIL   | logs/integration\_tests.log | screenshot/integration\_fail.png |
| ATC03   | Patrol Tests      | GitLab CI   | Android Emulator | PASS   | logs/patrol.log             | —                                |


## 3. Example Real-World Test Cases with Checklists

### Manual Testing Checklist Example

| Checklist ID | Description                        | Status    |
| ------------ | ---------------------------------- | --------- |
| CL01         | App installation and launch        | Completed |
| CL02         | UI correctness (fonts, colors)     | Completed |
| CL03         | New user registration              | Completed |
| CL04         | Login with valid credentials       | Completed |
| CL05         | Login with invalid credentials     | Completed |
| CL06         | Language switching (if applicable) | Pending   |
| CL07         | Handling of network disconnection  | Pending   |
| CL08         | Offline mode check                 | Pending   |



### Example Test Cases (Manual + Automated)

| Test ID | Test Name                    | Type   | Priority | Steps                                  | Expected Result               |
| ------- | ---------------------------- | ------ | -------- | -------------------------------------- | ----------------------------- |
| TC01    | Valid login                  | Manual | High     | Enter valid credentials, tap "Login"   | User is logged into the app   |
| TC02    | Invalid login                | Manual | High     | Enter invalid credentials, tap "Login" | Error message displayed       |
| TC03    | Screen navigation check      | Manual | Medium   | Switch between Home, Profile, Settings | Screens switch without errors |
| ATC01   | Unit tests                   | Auto   | High     | Run `flutter test`                     | All tests pass                |
| ATC02   | Integration tests            | Auto   | High     | Run `flutter drive`                    | All tests pass                |
| ATC03   | E2E tests via Patrol/Maestro | Auto   | Medium   | Run `patrol test` or `maestro test`    | All tests pass                |



* CI/CD documentation is ready (GitLab, GitHub Actions, Bitrise).
* Test report templates are ready (manual and automated).
* Checklists and example test cases are ready.

