# Website Security Scanning with OWASP ZAP

A GitHub Actions workflow that automatically performs security scans on web applications using OWASP ZAP (Zed Attack Proxy).

## Overview

This repository contains a CI/CD pipeline that uses OWASP ZAP to perform comprehensive security testing on web applications. The workflow runs automatically on pushes and pull requests to the main branch, and can also be triggered manually.

## Features

- **Automated Security Scanning**: Runs OWASP ZAP full scan on target web applications
- **CI/CD Integration**: Integrates seamlessly with GitHub Actions
- **Pull Request Checks**: Automatically scans code changes before merging
- **Manual Triggers**: Can be run on-demand via workflow_dispatch
- **Security Reports**: Generates detailed security reports as GitHub issues

## Workflow Configuration

The workflow is configured in [.github/workflows/blank.yml](.github/workflows/blank.yml) and includes:

- **Trigger Events**:
  - Push to `main` branch
  - Pull requests to `main` branch
  - Manual workflow dispatch

- **ZAP Configuration**:
  - Uses `zaproxy/action-full-scan@v0.12.0`
  - Docker image: `ghcr.io/zaproxy/zaproxy:stable`
  - Target URL: `https://anuraj.dev/`
  - Command options: `-a` (includes AJAX spider)

## Setup

1. Fork or clone this repository
2. Update the target URL in the workflow file:
   ```yaml
   target: 'https://your-website.com/'
   ```
3. Commit and push the changes
4. The workflow will run automatically on push

## Usage

### Automatic Scanning

The workflow runs automatically when:
- Code is pushed to the main branch
- A pull request is opened or updated targeting the main branch

### Manual Scanning

To run a manual scan:
1. Go to the **Actions** tab in your repository
2. Select **Web Security Scanning** workflow
3. Click **Run workflow**
4. Choose the branch and click **Run workflow**

## Understanding the Results

After the scan completes:
- A new issue will be created in the repository with the scan results
- The issue will contain:
  - Identified vulnerabilities
  - Risk levels (High, Medium, Low, Informational)
  - Recommendations for fixing issues

## Customization

You can customize the scan by modifying the `cmd_options` parameter:

- `-a`: Include AJAX spider (enabled by default)
- `-j`: Use JSON format for the report
- `-l`: Set minimum alert level (PASS, IGNORE, INFO, WARN, FAIL)
- `-r`: Generate HTML report
- `-w`: Generate Markdown report

Example:
```yaml
cmd_options: '-a -j -l WARN'
```

## Requirements

- GitHub repository with Actions enabled
- `GITHUB_TOKEN` (automatically provided by GitHub Actions)
- Publicly accessible target website or appropriate network configuration

## About OWASP ZAP

OWASP ZAP (Zed Attack Proxy) is one of the world's most popular free security tools. It helps find security vulnerabilities in web applications during development and testing.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Resources

- [OWASP ZAP Documentation](https://www.zaproxy.org/docs/)
- [ZAP GitHub Action](https://github.com/zaproxy/action-full-scan)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
