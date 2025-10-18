# Internal Fork Setup Guide

This document provides instructions for setting up a secure, self-hosted fork of the MCP SuperAssistant Chrome extension. Following these steps is crucial for maintaining a custom, secure version for internal company use.

## Why Fork?

A **fork** is a new repository under your organization's control that is a copy of the original. This is superior to a simple `git clone` because it provides:

-   **A Centralized "Master" Copy**: Your fork becomes the official source of truth for your company's version.
-   **Team Collaboration**: All team members can clone, push to, and pull from your fork.
-   **Ability to Pull Updates**: You can easily pull bug fixes and security updates from the original ("upstream") project into your version.

## Step-by-Step Instructions

1.  **Fork the Repository**
    Go to the original project's GitHub page and click the **Fork** button. Choose your company's GitHub organization as the destination for the new repository.

2.  **Clone Your Fork**
    On your local machine, clone the new repository you just forked. Replace `YOUR_ORGANIZATION` with your GitHub username or organization name.

    ```bash
    git clone [https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git](https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git)
    ```

3.  **Configure the "Upstream" Remote**
    Navigate into your new local repository directory. Add the original repository as a remote named `upstream`. This is the key step that allows you to pull in future updates.

    ```bash
    cd MCP-SuperAssistant
    git remote add upstream [https://github.com/srbhptl39/MCP-SuperAssistant.git](https://github.com/srbhptl39/MCP-SuperAssistant.git)
    ```

4.  **Verify the Configuration**
    Run `git remote -v` to ensure both `origin` (your fork) and `upstream` (the original project) are configured correctly. The output should look like this:

    ```
    origin    [https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git](https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git) (fetch)
    origin    [https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git](https://github.com/YOUR_ORGANIZATION/MCP-SuperAssistant.git) (push)
    upstream  [https://github.com/srbhptl39/MCP-SuperAssistant.git](https://github.com/srbhptl39/MCP-SuperAssistant.git) (fetch)
    upstream  [https://github.com/srbhptl39/MCP-SuperAssistant.git](https://github.com/srbhptl39/MCP-SuperAssistant.git) (push)
    ```

Your repository is now correctly set up.