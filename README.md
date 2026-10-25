# QAcart Todo Maestro Tests

This repository contains end-to-end mobile UI tests for the QAcart Todo Android app using Maestro.

The suite covers:
- Authentication flows (login and registration)
- Todo creation and validation
- Plan upgrade flows
- Plan cancellation scenarios

## Project structure

- `Maestro/config.yaml` - Maestro configuration
- `Maestro/Flows/` - reusable flow definitions
- `Maestro/Tests/` - individual test cases
- `Maestro/scripts/utils.js` - helper script used by the tests
- `.github/workflows/maestro-cloud.yml` - GitHub Actions workflow for running the suite in Maestro Cloud

## App under test

The tests target the Android app:
- `com.qacart.todo_app`

## Prerequisites

Before running the tests locally, make sure you have:
- Android Studio and an emulator or a physical Android device
- The Android app installed on the target device/emulator
- Maestro CLI installed

Install Maestro CLI:

```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
```

Verify installation:

```bash
maestro --version
```

## Running tests locally

Start an Android emulator or connect a device, then run:

```bash
maestro test ./Maestro/Tests
```

You can also run a single test file:

```bash
maestro test ./Maestro/Tests/auth/login-test.yaml
maestro test ./Maestro/Tests/todos/add-todo-test.yaml
```

To run a specific flow or a subset of tests, use the corresponding YAML file under `Maestro/Tests/`.

## CI/CD

This project includes a GitHub Actions workflow that:
1. Downloads the APK for the app under test
2. Uploads it to Maestro Cloud
3. Executes the tests defined in the `Maestro/` workspace

The workflow is defined in:
- `.github/workflows/maestro-cloud.yml`

Required repository secrets:
- `MAESTRO_CLOUD_API_KEY`
- `MAESTRO_PROJECT_ID`

## Notes

- The Maestro configuration disables Android animations for more stable UI automation.
- Flow files are stored under `Maestro/Flows/` and reused in test files to keep test scenarios readable and maintainable.
