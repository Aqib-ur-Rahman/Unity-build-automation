# DevOps Assessment – Unity GitHub Actions Pipeline

## Overview
This repository contains a GitHub Actions CI pipeline for building a Unity Android project.

The pipeline:
- triggers on push to `main`
- supports manual execution through `workflow_dispatch`
- builds both APK and AAB outputs
- uploads build artifacts to GitHub Actions
- sends Slack notifications after the workflow completes
- securely handles Unity license, Android signing, and Slack webhook through GitHub Secrets

## Pipeline Architecture
The workflow is located at:

`.github/workflows/unity-android-build.yml`

Main stages:
1. Checkout repository
2. Cache Unity Library folder
3. Decode Android keystore from GitHub Secret
4. Build Android APK
5. Build Android AAB
6. Upload APK and AAB as GitHub Actions artifacts
7. Send Slack notification with repository, branch, commit hash, and workflow run link
8. Cleanup temporary keystore file

## Required GitHub Secrets
The following repository secrets are required:

- UNITY_LICENSE
- UNITY_EMAIL
- UNITY_PASSWORD
- ANDROID_KEYSTORE
- ANDROID_KEYSTORE_PASS
- ANDROID_KEY_ALIAS
- ANDROID_KEY_ALIAS_PASS
- SLACK_WEBHOOK_URL

## Setup Instructions
1. Add the required GitHub Secrets in:
   Settings → Secrets and variables → Actions

2. Ensure the Unity project exists under:
   `unity-project/`

3. Push to the `main` branch or manually trigger the workflow from:
   Actions → Unity Android CI → Run workflow

## Build Outputs
Artifacts are stored in a structured directory:

- Builds/Android/APK/
- Builds/Android/AAB/

Uploaded GitHub Actions artifacts:
- android-apk
- android-aab

## Design Decisions
- Used `ubuntu-latest` to match the assessment requirement
- Pinned Unity version for reproducibility
- Used `game-ci/unity-builder` for reliable Unity CI builds
- Stored secrets in GitHub Secrets for secure handling
- Used Base64-encoded keystore secret for Android signing
- Uploaded APK and AAB with `actions/upload-artifact`
- Added Slack notification for build visibility
- Added Unity Library caching as a performance optimization


## Estimated Completion Time
Estimated completion time: 6–8 hours

This included:
- repository and workflow setup
- Unity project preparation
- Unity license activation troubleshooting
- Android signing setup
- artifact generation and upload
- Slack integration
- debugging and validation
