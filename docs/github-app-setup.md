# GitHub App Setup Guide

This guide explains how to create and configure a GitHub App to automate item submissions.

## Step 1: Create a GitHub App

1. Go to your GitHub account settings:
   - Click your profile picture → **Settings**
   - Scroll down to **Developer settings** (left sidebar)
   - Click **GitHub Apps** → **New GitHub App**

2. Fill out the form:
   - **GitHub App name**: `My Junk Item Automation` (or any unique name)
   - **Homepage URL**: Your repository URL (e.g., `https://github.com/tomp736/my-junk`)
   - **Webhook**: Uncheck "Active" (we don't need webhooks)
   - **Permissions**:
     - Repository permissions:
       - **Contents**: Read and write (to create branches and commit files)
       - **Pull requests**: Read and write (to create PRs)
       - **Issues**: Read and write (to comment on issues)
   - **Where can this GitHub App be installed?**: Select "Only on this account"

3. Click **Create GitHub App**

## Step 2: Generate a Private Key

1. After creating the app, scroll down to **Private keys**
2. Click **Generate a private key**
3. A `.pem` file will be downloaded - keep this safe!

## Step 3: Install the GitHub App

1. In your GitHub App settings, click **Install App** (left sidebar)
2. Click **Install** next to your account
3. Select **Only select repositories**
4. Choose the `my-junk` repository
5. Click **Install**

## Step 4: Get the App ID and Installation ID

1. **App ID**:
   - Go to your GitHub App settings
   - The App ID is shown at the top (e.g., `123456`)

2. **Installation ID**:
   - Go to your installed app: `https://github.com/settings/installations`
   - Click **Configure** on your app
   - Look at the URL: `https://github.com/settings/installations/[INSTALLATION_ID]`
   - Copy the installation ID from the URL

## Step 5: Add Variable and Secret to Your Repository

1. Go to your repository: `https://github.com/tomp736/my-junk`
2. Click **Settings** → **Secrets and variables** → **Actions**

3. **Add Variable** (click the "Variables" tab):
   - Click **New repository variable**
   - Name: `GH_APP_AUTOMATION_APP_ID`
   - Value: Your App ID (from Step 4)
   - Click **Add variable**

4. **Add Secret** (click the "Secrets" tab):
   - Click **New repository secret**
   - Name: `GH_APP_AUTOMATION_APP_PRIVATE_KEY`
   - Value: The entire contents of the `.pem` file (including the `-----BEGIN RSA PRIVATE KEY-----` and `-----END RSA PRIVATE KEY-----` lines)
   - Click **Add secret**

**Why do we need the private key?**
- The private key proves that you control the GitHub App (like a password)
- GitHub uses it to verify that API requests are really coming from your app
- Even if someone knows your App ID, they can't impersonate your app without the private key
- The action automatically uses this to generate temporary installation tokens

## Step 6: Update and Test

The workflow has been updated to use the GitHub App authentication. Push the changes and test by creating a new issue!

## Troubleshooting

- **"Resource not accessible by integration"**: Check that the GitHub App has the correct permissions
- **"Bad credentials"**: Verify that the private key is correctly copied (including header/footer lines)
- **"Installation not found"**: Make sure the app is installed on the repository

## Security Notes

- The private key is sensitive - never commit it to the repository
- Keep the `.pem` file secure and backed up
- You can revoke and regenerate the private key at any time from the GitHub App settings
- The GitHub App only has access to repositories where it's installed
