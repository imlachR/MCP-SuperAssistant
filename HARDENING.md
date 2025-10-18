# Security Hardening Tasks

This document details the necessary code modifications to remove analytics and remote configuration features from the MCP SuperAssistant extension. These changes will enhance privacy and security by preventing all communication with external, third-party services.

## Task 1: Disable Analytics

This task will prevent the extension from collecting and sending usage and demographic data to Google Analytics.

#### 1.1. Neuter the Analytics Sending Function

-   **File**: [chrome-extension/utils/analytics.ts](cci:7://file:///Users/rodrigoimlach/Documents/live/motion-central/MCP-SuperAssistant/chrome-extension/utils/analytics.ts:0:0-0:0)
-   **Action**: Replace the entire body of the [sendAnalyticsEvent](cci:1://file:///Users/rodrigoimlach/Documents/live/motion-central/MCP-SuperAssistant/chrome-extension/utils/analytics.ts:89:0-171:1) function with a single `return;` statement. This effectively disables the function without having to trace and remove every call to it.

    *Before:*
    ```typescript
    export async function sendAnalyticsEvent(name: string, params: { [key: string]: any }): Promise<void> {
      // ... original function body ...
    }
    ```

    *After:*
    ```typescript
    export async function sendAnalyticsEvent(name: string, params: { [key: string]: any }): Promise<void> {
      return;
    }
    ```

#### 1.2. Remove Host Permission

-   **File**: [chrome-extension/manifest.ts](cci:7://file:///Users/rodrigoimlach/Documents/live/motion-central/MCP-SuperAssistant/chrome-extension/manifest.ts:0:0-0:0)
-   **Action**: In the `host_permissions` array, delete the line that grants access to Google Analytics.

    *Remove this line:*
    ```typescript
    '*://*.google-analytics.com/*',
    ```

## Task 2: Disable Remote Configuration

This task ensures the extension's behavior cannot be changed remotely. The feature is already disabled by a flag, but this step makes that permanent and removes any ambiguity.

-   **File**: [chrome-extension/src/background/firebase-remote-config-api.ts](cci:7://file:///Users/rodrigoimlach/Documents/live/motion-central/MCP-SuperAssistant/chrome-extension/src/background/firebase-remote-config-api.ts:0:0-0:0)
-   **Action**: Verify that the `REMOTE_CONFIG_ENABLED` constant is set to `false`. This is the most critical step for disabling this feature.

    *Ensure this line is present and set to `false`:*
    ```typescript
    const REMOTE_CONFIG_ENABLED = false;
    ```

## Task 3: Commit and Push Your Changes

After making these changes, commit them to your fork. This creates a clean, secure baseline for your company's internal version.

```bash
git commit -am "Security Hardening: Remove analytics and remote configuration"
git push origin main