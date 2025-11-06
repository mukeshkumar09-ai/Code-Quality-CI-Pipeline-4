# Code Quality CI Pipeline

A simple CI pipeline that checks code quality using ESLint and Jenkins.

## Setup Instructions

1. Install Jenkins on your server
2. Install required Jenkins plugins:
   - NodeJS Plugin
   - Email Extension Plugin

3. In Jenkins:
   - Create a new Pipeline job
   - Configure Git repository URL
   - Set the pipeline script to use the Jenkinsfile from SCM

4. Configure NodeJS in Jenkins:
   - Go to Manage Jenkins > Global Tool Configuration
   - Add NodeJS installation named 'Node'

5. Local Development:
```bash
# Install dependencies
npm install

# Run linting locally
npm run lint
```

## Features

- Automated ESLint checks on every push
- Email notifications for build status
- Quality badge generation (PASS/FAIL)

## Badge

The quality badge will be generated as a JSON file that can be hosted and used with badge services like shields.io.