# Google Drive Auto-Sync Setup Guide

This guide will help you set up automatic file uploads to Google Drive whenever you push changes to your resume repo.

## Step 1: Create a Google Service Account

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or use existing one)
   - Click "Select a Project" → "New Project"
   - Name it "Resume Sync" or similar
3. Enable the Google Drive API:
   - Go to "APIs & Services" → "Library"
   - Search for "Google Drive API"
   - Click "Enable"

## Step 2: Create a Service Account

1. Go to "APIs & Services" → "Credentials"
2. Click "Create Credentials" → "Service Account"
3. Fill in the details:
   - **Service account name:** `resume-sync`
   - Click "Create and Continue"
4. Grant permissions:
   - **Role:** Editor (so it can upload files)
   - Click "Continue" → "Done"

## Step 3: Generate Service Account Keys

1. In "Credentials" page, under "Service Accounts", click the email you just created
2. Go to "Keys" tab
3. Click "Add Key" → "Create new key"
4. Choose **JSON** format
5. Click "Create" - a JSON file will download
   - **Save this file safely!** You'll need the contents

## Step 4: Extract Credentials from JSON

Open the downloaded JSON file. It will look like:

```json
{
  "type": "service_account",
  "project_id": "xxx",
  "private_key_id": "xxx",
  "private_key": "-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n",
  "client_email": "xxx@xxx.iam.gserviceaccount.com",
  "client_id": "xxx",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "xxx"
}
```

**You'll need all these values for GitHub Secrets.**

## Step 5: Create a Google Drive Folder

1. Open [Google Drive](https://drive.google.com/)
2. Create a new folder (e.g., "Resume Backups")
3. Right-click → "Share"
4. Add the service account email (from JSON file as `client_email`)
5. Give it "Editor" permission
6. Copy the folder ID from the URL:
   - URL format: `https://drive.google.com/drive/folders/FOLDER_ID_HERE`
   - **Copy just the FOLDER_ID part**

## Step 6: Add GitHub Secrets

1. Go to your resume repository on GitHub
2. Click "Settings" → "Secrets and variables" → "Actions"
3. Click "New repository secret" and add these secrets:

| Secret Name | Value |
|---|---|
| `GOOGLE_PROJECT_ID` | `project_id` from JSON |
| `GOOGLE_PRIVATE_KEY_ID` | `private_key_id` from JSON |
| `GOOGLE_PRIVATE_KEY` | `private_key` from JSON (keep the `\n` escape sequences) |
| `GOOGLE_CLIENT_EMAIL` | `client_email` from JSON |
| `GOOGLE_CLIENT_ID` | `client_id` from JSON |
| `GOOGLE_CLIENT_X509_CERT_URL` | `client_x509_cert_url` from JSON |
| `GOOGLE_DRIVE_FOLDER_ID` | Folder ID from Step 5 |

⚠️ **Important:** Be careful with the `GOOGLE_PRIVATE_KEY` - keep all the newlines (`\n`) as they appear in the JSON file.

## Step 7: Test the Workflow

1. Make a small change to your resume repo (e.g., update `index.html`)
2. Commit and push to main branch
3. Go to "Actions" tab on GitHub
4. You should see "Sync Files to Google Drive" running
5. Check your Google Drive folder - the files should appear!

## How It Works

Every time you:
- Push a change to `index.html` or a PDF file
- The GitHub Action automatically triggers
- It uploads/updates the files in your Google Drive
- Both files stay in sync across platforms

## Troubleshooting

### Workflow fails with "Permission denied"
- Make sure the service account email has "Editor" access to the Drive folder
- Check that the folder ID is correct

### Private key error
- Make sure the `GOOGLE_PRIVATE_KEY` secret includes all the `\n` newline characters from the JSON file

### Files not appearing in Drive
- Check the "Actions" tab to see the workflow logs
- Verify the folder ID is correct
- Make sure you're pushing to the `main` branch

## Security Notes

- 🔒 Never share your service account JSON file
- 🔐 GitHub Secrets are encrypted and only used in Actions
- 📝 The service account is different from your personal Google account
- 🚫 It only has access to the folder you shared with it

## Disabling the Workflow

If you want to stop syncing to Google Drive:
- Go to "Actions" tab
- Click "Sync Files to Google Drive"
- Click "Disable workflow"

Or just delete the `.github/workflows/sync-to-google-drive.yml` file.

---

Once set up, you can forget about manual uploads! Your resume stays synced automatically. 🚀
