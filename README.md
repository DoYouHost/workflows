# DoYouHost Workflows

Repository containing reusable GitHub Actions workflows for ESPHome projects and firmware management.

## 🔄 Available Workflows

### 1. Build (`build.yml`)
Workflow for building ESPHome firmware with various configurations.

**Inputs:**
- `files` (required) - Newline separated list of files to build
- `esphome-version` - Version of ESPHome to use (default: `latest`)
- `release-summary` - Summary of the release
- `release-url` - URL to the release notes
- `release-version` - Version of the release
- `combined-name` - Name to combine all files into a single manifest
- `debug` - Enable verbose debug output (default: `false`)

**Outputs:**
- `version` - Generated firmware version

### 2. Upload to R2 (`upload-to-r2.yml`)
Workflow for uploading firmware to Cloudflare R2.

**Inputs:**
- `directory` (required) - Target directory on R2

### 3. Upload to GitHub Release (`upload-to-gh-release.yml`)
Workflow for creating GitHub Release with firmware.

**Inputs:**
- `version` (required) - Release version
- `description` - Release description
- `prerelease` - Whether this is a prerelease (default: `false`)

**Secrets:**
- `PAT_TOKEN` (optional) - Personal Access Token for creating releases

### 4. Promote R2 (`promote-r2.yml`)
Workflow for promoting firmware between channels (beta/production) on R2.

**Inputs:**
- `version` (required) - Firmware version to promote
- `directory` (required) - Target directory
- `channel` - Target channel: "beta" or "production" (default: `beta`)
- `manifest-filename` - Manifest filename (default: `manifest-beta.json`)

## 🔧 Required Secrets

For full workflow functionality, configure the following secrets in your repository:

### Cloudflare R2
- `CF_ACCOUNT_ID` - Cloudflare account ID
- `CF_ACCESS_KEY_ID` - R2 access key
- `CF_SECRET_ACCESS_KEY` - R2 secret access key
- `CF_BUCKET_NAME` - R2 bucket name

### GitHub Releases (optional)
- `PAT_TOKEN` - Personal Access Token with release creation permissions

## 🛠️ Environments

Workflows use GitHub environments for different channels:
- `beta` - Beta channel
- `production` - Production channel

## 📋 Dependabot

The repository is configured with Dependabot to automatically update GitHub Actions weekly.
