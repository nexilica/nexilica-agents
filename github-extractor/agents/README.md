# GitHub Extractor Agent - User Guide

## Files Created

- `github-extractor.md` - Complete agent configuration

## How to Use the Agent

### Method 1: Direct Invocation

You can invoke the agent directly in your Claude Code conversations using:

```
/github-extractor
```

This will activate the specialized agent that follows all defined rules.

### Method 2: Automatic Invocation

Claude Code can automatically invoke this agent when you:
- Ask about GitHub repositories
- Request analysis of issues or pull requests
- Query commit history or contributors
- Need to extract data from GitHub
- Ask about releases, branches, or tags

### Method 3: Generation with Claude (Recommended for Customizations)

If you want to modify or regenerate the agent:

1. Run `/agents` in Claude Code
2. Select "generate with claude (recommended)"
3. Describe the modifications you want
4. Claude will generate a new version

## Main Functionality

### 1. Repository Analysis

The agent can search for and analyze repositories based on:
- Programming language
- Star count and popularity metrics
- Topics and tags
- Activity patterns
- License type
- Creation and update dates

**Output includes**: Description, statistics, license, primary language, activity metrics, and health indicators.

### 2. Issue Investigation

Comprehensive issue tracking and analysis:
- Search issues by status, labels, assignees
- Track resolution patterns and timelines
- Identify trends in bug reports and feature requests
- Analyze community feedback patterns
- Monitor issue lifecycle and milestones

### 3. Pull Request Analysis

Deep dive into PR workflows:
- Code review process examination
- Merge patterns and velocity
- Contributor collaboration networks
- Review comments and approval workflows
- PR quality metrics and bottlenecks

### 4. Commit History Analysis

Track development patterns:
- Commit frequency and patterns
- Contributor activity and specializations
- Code change trends
- Development velocity metrics
- Key contributor identification

### 5. Release Tracking

Monitor and report on releases:
- Version numbers and release notes
- Release assets and downloads
- Publication dates and frequency
- Adoption patterns

### 6. Content Retrieval

Extract file contents from repositories:
- README files and documentation
- Configuration files
- Source code analysis
- License and contributing guidelines

### 7. Contributor Insights

Analyze contribution patterns:
- Top contributors identification
- Contribution frequency and consistency
- Areas of expertise and specialization
- Collaboration networks

### 8. Branch and Tag Management

Track repository structure:
- Active development branches
- Branch naming patterns
- Tag patterns for versioning
- Release management workflows

## Example Usage Scenarios

### Example 1: Analyze Repository Activity

```
User: Can you analyze the recent activity on facebook/react?

Agent: I'll analyze the facebook/react repository...

[Agent provides]:
### Repository: facebook/react
🔗 https://github.com/facebook/react

**Overview**:
- Description: [...]
- Language: JavaScript
- Stars: [count] | Forks: [count]
- Recent activity metrics
- Key contributors
- Recent issues and PRs

**Insights**:
[Detailed analysis of patterns, trends, and notable characteristics]
```

### Example 2: Issue Summary

```
User: Show me open bugs in microsoft/vscode

Agent: I'll search for open bug issues in microsoft/vscode...

[Agent provides]:
### Bug Issues Summary for microsoft/vscode

**Overview**:
- Total Open Bugs: [count]
- Recent Activity: [analysis]
- Average Resolution Time: [duration]

**Notable Bugs**:
1. [Bug title] (#123) - 🔗 [link]
   [Description and impact]

**Insights**:
[Pattern analysis and recommendations]
```

### Example 3: Contributor Analysis

```
User: Who are the top contributors to tensorflow/tensorflow in the last 6 months?

Agent: I'll analyze recent contributor activity for tensorflow/tensorflow...

[Agent provides]:
### Top Contributors (Last 6 Months)

1. **[Contributor Name]** (@username)
   - Commits: [count]
   - Focus Areas: [specialization]
   - 🔗 [GitHub profile]

[Additional contributors with metrics and insights]

**Contribution Patterns**:
[Analysis of collaboration, commit frequency, and trends]
```

### Example 4: Release Information

```
User: What are the latest releases for nodejs/node?

Agent: I'll fetch the recent releases for nodejs/node...

[Agent provides]:
### Recent Releases for nodejs/node

**Latest Release**: v[X.Y.Z]
- Published: [date]
- Release Notes: [summary]
- 🔗 [Release link]

**Previous Releases**:
[List with dates and key changes]

**Release Patterns**:
[Analysis of release frequency and versioning]
```

## Key Features

### ✅ Comprehensive Data Extraction
Uses all available GitHub MCP tools to gather complete information from repositories, issues, PRs, commits, and more.

### ✅ Intelligent Analysis
Goes beyond raw data to provide meaningful insights, identify patterns, and highlight significant trends.

### ✅ Structured Reporting
Presents information in clear, well-organized formats with:
- Section headers and logical organization
- Tables and lists for metrics
- Direct GitHub links to resources
- Context and interpretation

### ✅ Multi-Source Integration
Combines data from multiple GitHub resources for comprehensive analysis when needed.

### ✅ Proactive Insights
Identifies notable characteristics, patterns, and anomalies even when not explicitly requested.

## Agent Rules

The agent follows these core principles:

1. ✅ **Always Provide Context**: Never present raw data without interpretation and insights
2. ✅ **Include Direct Links**: All GitHub resources include properly formatted links
3. ✅ **Structured Output**: Uses consistent formatting with clear sections and headers
4. ✅ **Comprehensive Analysis**: Combines multiple data sources when appropriate
5. ✅ **Pattern Recognition**: Identifies trends, anomalies, and significant characteristics
6. ✅ **Error Transparency**: Clearly communicates limitations, access restrictions, or missing data

## Output Format Standards

The agent uses consistent formatting:

- **Dates**: Clear, readable format with context (e.g., "Last updated 3 days ago")
- **Numbers**: Both absolute values and contextual interpretation
- **Links**: Direct GitHub URLs formatted as 🔗 [link text]
- **Sections**: Logical organization from most to least important
- **Metrics**: Include relevant timeframes and comparisons

## Best Practices

### When to Invoke the Agent

- Researching repositories before using or contributing
- Monitoring project health and activity
- Analyzing issue resolution patterns
- Evaluating PR workflows and quality
- Tracking contributor activity and collaboration
- Gathering release information
- Extracting repository documentation

### Communicating with the Agent

**Clear and Specific:**
```
✅ "Analyze the open issues labeled 'bug' in owner/repo"
✅ "Show me commit activity for owner/repo in the last month"
✅ "Compare the release frequency of owner/repo1 and owner/repo2"
```

**To Avoid:**
```
❌ "Tell me about GitHub" (too vague)
❌ "Show me everything about this repo" (overly broad)
```

**Effective Requests:**
```
✅ "What are the top 5 most active repositories in the Python ecosystem?"
✅ "Analyze the PR review process for facebook/react"
✅ "Show me the recent contributor trends for tensorflow/tensorflow"
```

## Troubleshooting

### Agent doesn't activate automatically

- Use direct invocation: `/github-extractor`
- Verify the file is in `.claude/agents/`

### Private repository access issues

- The agent can only access public repositories or those you have access to
- Check your GitHub authentication in Claude Code

### Rate limiting errors

- GitHub API has rate limits
- The agent will inform you if limits are reached
- Wait a few minutes before retrying

### Incomplete data

- The agent will acknowledge when data is limited or unavailable
- It will explain what information is accessible and what isn't

## Customization

To modify the agent behavior:

1. Open `.claude/agents/github-extractor.md`
2. Modify the YAML frontmatter to change:
   - `model`: Model to use (sonnet, opus, haiku)
   - `color`: Agent color in the UI
3. Modify the markdown content to change:
   - Analysis depth and focus areas
   - Output formatting preferences
   - Specific GitHub features to prioritize

## Support

For issues or questions:
- Consult official documentation: https://code.claude.com/docs/en/sub-agents.md
- Use `/help` in Claude Code
- Ask Claude Code directly about the agent's behavior

---

**Agent Version**: 1.0
**Model**: Sonnet
**GitHub API**: Uses GitHub MCP Server tools
**Created**: 2025-11-21
