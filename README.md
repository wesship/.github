# wesship Organization - GitHub Copilot + MCP Server Workflows

Welcome to the wesship organization! This repository contains organization-wide templates, configurations, and workflows designed to enhance development productivity through GitHub Copilot and MCP (Model Context Protocol) Server integration.

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have the following installed and configured:

- **GitHub Account** with access to wesship organization
- **GitHub Copilot** subscription (Individual or Business)
- **Git** (version 2.20 or higher)
- **Node.js** (version 16 or higher) - for npm-based projects
- **Visual Studio Code** or **GitHub Codespaces** (recommended)

### Required Extensions

Install these VS Code extensions for the optimal development experience:

1. **GitHub Copilot** (`GitHub.copilot`)
2. **GitHub Copilot Chat** (`GitHub.copilot-chat`)
3. **GitHub Pull Requests and Issues** (`GitHub.vscode-pull-request-github`)
4. **GitLens** (`eamodio.gitlens`)
5. **MCP Client** (if available) - for MCP server integration

```bash
# Install via VS Code CLI
code --install-extension GitHub.copilot
code --install-extension GitHub.copilot-chat
code --install-extension GitHub.vscode-pull-request-github
code --install-extension eamodio.gitlens
```

## 🔧 Setup Guide

### 1. Authentication Setup

#### GitHub Authentication
```bash
# Configure Git with your GitHub credentials
git config --global user.name "Your Name"
git config --global user.email "your.email@wesship.com"

# Set up GitHub CLI (optional but recommended)
gh auth login
```

#### GitHub Copilot Authentication
1. Open VS Code
2. Sign in to GitHub when prompted by Copilot
3. Verify authentication: `Ctrl+Shift+P` → "GitHub Copilot: Check Status"

### 2. MCP Server Configuration

The MCP server enhances GitHub Copilot with organization-specific context and automation. Our configuration is located at `mcp-server.config.yaml`.

#### Key Features Enabled:
- **Issue Triage**: Automatic labeling and assignment
- **PR Automation**: Reviewer assignment and conflict detection  
- **Code Quality**: Automated suggestions and security scanning
- **Workflow Integration**: Seamless GitHub Actions integration

#### Local Development Setup
```bash
# Clone this repository to access configurations
git clone https://github.com/wesship/.github.git
cd .github

# Copy configurations to your project (if needed)
cp mcp-server.config.yaml /path/to/your/project/
cp copilot-agent-profile.json /path/to/your/project/
```

## 📋 Templates and Workflows

### Issue Templates

We provide standardized issue templates to ensure consistent reporting:

- **🐛 Bug Report** (`.github/ISSUE_TEMPLATE/bug_report.yml`)
  - Steps to reproduce
  - Expected vs actual behavior
  - System information
  - Screenshots/logs

- **✨ Feature Request** (`.github/ISSUE_TEMPLATE/feature_request.yml`)
  - Problem statement and motivation
  - Proposed solution
  - Alternative approaches
  - Acceptance criteria

### Pull Request Template

Our PR template (`.github/PULL_REQUEST_TEMPLATE.md`) includes:
- Clear description and related issues
- Type of change classification
- Testing checklist
- Reviewer guidelines
- Security and performance considerations

### Creating Issues and PRs

```bash
# Create a new branch for your work
git checkout -b feature/your-feature-name

# Make your changes and commit
git add .
git commit -m "feat: add new feature"

# Push and create PR
git push origin feature/your-feature-name
gh pr create --template
```

## 🤖 GitHub Copilot Best Practices

### Code Generation

1. **Write Clear Comments**: Copilot works best with descriptive comments
   ```javascript
   // Create a function that validates email addresses using regex
   function validateEmail(email) {
     // Copilot will suggest implementation
   }
   ```

2. **Use Descriptive Function Names**: Help Copilot understand intent
   ```python
   def calculate_monthly_recurring_revenue(subscriptions):
       # Copilot will suggest business logic
   ```

3. **Provide Context**: Include relevant imports and type definitions
   ```typescript
   import { User } from './types';
   
   // Function to create user profile with validation
   async function createUserProfile(userData: User): Promise<UserProfile> {
   ```

### Chat and Assistance

Use GitHub Copilot Chat for:
- **Code Explanation**: `@copilot explain this function`
- **Bug Fixing**: `@copilot help me fix this error`
- **Testing**: `@copilot generate tests for this class`
- **Refactoring**: `@copilot refactor this code to be more performant`
- **Documentation**: `@copilot write documentation for this API`

### Copilot CLI Commands

```bash
# Ask for help with git commands
gh copilot suggest "undo last commit"

# Get shell command suggestions
gh copilot suggest "find large files in directory"

# Explain complex commands
gh copilot explain "docker run -it --rm -v $(pwd):/app node:16"
```

## 🔒 Security Guidelines

### Code Security

1. **Never commit secrets**: Use environment variables and `.env.example` files
2. **Review Copilot suggestions**: Always review generated code for security issues
3. **Use organization patterns**: Follow established security patterns in the codebase
4. **Enable security scanning**: Ensure GitHub security features are enabled

### Sensitive Data Handling

```bash
# Use environment variables for sensitive data
export DATABASE_URL="your-database-url"
export API_KEY="your-api-key"

# Never commit these patterns:
*.env
*.key
*.pem
*secret*
*password*
```

### MCP Server Security

- Configured secret scanning patterns
- Automatic dependency vulnerability detection
- Code quality gates with security thresholds
- Integration with GitHub security advisories

## 🎯 Sample Automation Commands

### Issue Management

```bash
# Create bug report with template
gh issue create --template bug_report.yml

# Create feature request
gh issue create --template feature_request.yml

# List issues assigned to you
gh issue list --assignee @me

# Close issue with reference
gh issue close 123 --comment "Fixed in PR #456"
```

### Pull Request Workflows

```bash
# Create PR with template
gh pr create --template

# Request specific reviewers
gh pr create --reviewer @wesship/dev-team

# Auto-merge after reviews
gh pr merge --auto --squash

# Check PR status
gh pr status
```

### Automated Code Quality

```bash
# Run linting (configured in MCP server)
npm run lint

# Run tests with coverage
npm run test:coverage

# Security audit
npm audit

# Check for outdated dependencies
npm outdated
```

## 🔄 Development Workflow

### Standard Workflow

1. **Create Issue**: Use appropriate template
2. **Create Branch**: `git checkout -b type/description`
3. **Develop with Copilot**: Leverage suggestions and chat
4. **Write Tests**: Use Copilot to generate test cases
5. **Create PR**: Use template and link to issues
6. **Code Review**: Automated and manual review process
7. **Merge**: Automated merge after approvals

### MCP Server Integration Points

- **Issue Creation**: Auto-labeling and assignment
- **PR Creation**: Automatic reviewer assignment based on files changed
- **Code Review**: Quality gates and security checks
- **Merge**: Automated workflows and notifications

## 🛠 Troubleshooting

### Common Issues

1. **Copilot Not Working**
   ```bash
   # Check Copilot status
   gh copilot status
   
   # Reload VS Code window
   Ctrl+Shift+P → "Developer: Reload Window"
   ```

2. **MCP Server Issues**
   - Check `mcp-server.config.yaml` syntax
   - Verify GitHub App permissions
   - Review webhook configurations

3. **Template Issues**
   - Ensure templates are in correct directories
   - Check YAML syntax for issue templates
   - Verify markdown formatting for PR template

### Getting Help

- **Internal**: Create issue using bug report template
- **GitHub Copilot**: [GitHub Support](https://support.github.com/)
- **MCP Server**: Check configuration documentation
- **Organization**: Contact `@wesship/dev-team`

## 📚 Additional Resources

### Documentation
- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [VS Code GitHub Integration](https://code.visualstudio.com/docs/editor/github)

### Learning Resources
- [GitHub Copilot Best Practices](https://github.blog/2023-06-20-how-to-write-better-prompts-for-github-copilot/)
- [AI-Powered Development Workflows](https://github.blog/2023-10-30-the-architecture-of-todays-llm-applications/)

### Community
- Organization discussions in `wesship/.github`
- Internal Slack: `#dev-general`, `#github-copilot`
- Weekly office hours: Fridays 3-4 PM EST

## 📈 Metrics and Feedback

We track the following metrics to improve our workflows:
- Copilot suggestion acceptance rate
- PR review time reduction
- Issue resolution time
- Code quality improvements
- Developer satisfaction

Provide feedback through:
- Issues in this repository
- Internal surveys
- Team retrospectives
- Direct feedback to `@wesship/dev-team`

---

## 🤝 Contributing

To improve these templates and configurations:

1. Fork this repository
2. Create a feature branch
3. Make your improvements
4. Submit a PR with detailed description
5. Participate in the review process

Your contributions help make our development workflows more efficient and enjoyable for everyone!

---

**Happy coding with GitHub Copilot and MCP Server! 🚀**