# Syncing Remote Documentation File Paths with Nextra

This guide explains how to automate the process of fetching and synchronizing documentation file paths from remote GitHub repositories for use in a Nextra-based docs site. This is useful for referencing or integrating upstream documentation, and ensures your docs remain up-to-date with external sources.

## Overview

The `/nextra-remote-filepaths` directory contains scripts and data files for fetching lists of documentation file paths from specific commits or branches of remote GitHub repositories. These file lists are then available for use in your Nextra site or build process.

## How It Works

1. **Script:** `nextra-remote-filepaths/fetch.js` uses Nextra's `fetchFilePathsFromGitHub` utility to fetch file paths from remote GitHub repos.
2. **Output:** The script writes the results as JSON files (e.g., `graphql-yoga.json`, `graphql-eslint.json`) in the same directory.
3. **Usage:** These JSON files can be imported or referenced by your docs site to display, link, or otherwise use the remote documentation structure.

## Reference Code

### `nextra-remote-filepaths/fetch.js`
```js
import { fetchFilePathsFromGitHub } from 'nextra/fetch-filepaths-from-github'

fetchFilePathsFromGitHub({
  user: 'dotansimha',
  repo: 'graphql-yoga',
  // last commit with v2 source docs
  branch: '291daaaf3921b2ab875d988b7a7880ee277f247e',
  docsPath: 'website/src/pages/v2/',
  outputPath: './nextra-remote-filepaths/graphql-yoga.json'
})

fetchFilePathsFromGitHub({
  user: 'B2o5T',
  repo: 'graphql-eslint',
  branch: '34b722a2a520599ce06a4ddcccc9623b76434089',
  docsPath: 'website/src/pages/docs/',
  outputPath: './nextra-remote-filepaths/graphql-eslint.json'
})
```

### Example Output (`graphql-yoga.json`)
```json
[
  "website/src/pages/v2/README.md",
  "website/src/pages/v2/getting-started.md",
  ...
]
```

## Step-by-Step Instructions

1. **Install Dependencies**
   Make sure you have the required Nextra utility installed (typically as part of your Nextra site):
   ```bash
   npm install nextra
   # or
   pnpm add nextra
   ```

2. **Run the Fetch Script**
   Execute the script to fetch the latest file paths from the remote repositories:
   ```bash
   node ./nextra-remote-filepaths/fetch.js
   ```
   This will update the JSON files in the `nextra-remote-filepaths` directory.

3. **Use the JSON Files**
   Import or read these files in your Nextra site as needed. Example:
   ```js
   import yogaFilePaths from './nextra-remote-filepaths/graphql-yoga.json';
   // Use yogaFilePaths to generate sidebar, links, etc.
   ```

## Notes
- The script pins to specific commit hashes for reproducibility and stability.
- You can add more repositories or adjust the script for other sources as needed.
- Always review and update the commit hashes to sync with upstream changes when desired.

---

For more advanced usage or troubleshooting, see the Nextra documentation or the comments in `fetch.js`.
