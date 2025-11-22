# Repo/ Agents Catalog

**Quick reference for GitHub repository management and analysis agents.**

---

## 🎯 Quick Start

### Available Agents (1)

Repo/ currently contains **1 specialized agent** for GitHub data extraction:

**github-extractor**: Expert GitHub data analyst for comprehensive repository insights

**No orchestrator yet** - as more Repo agents are added, consider creating `repo-workflow-orchestrator`.

---

## 📋 Task → Agent Quick Reference

| Your Task | Call This Agent | Capabilities |
|-----------|----------------|--------------|
| **Analyze GitHub repository** | `github-extractor` | Complete repo analysis |
| **Track issues and PRs** | `github-extractor` | Issue/PR metrics and patterns |
| **Monitor releases** | `github-extractor` | Release tracking and versioning |
| **Analyze contributors** | `github-extractor` | Contributor insights and collaboration |
| **Search repositories** | `github-extractor` | Repository discovery and comparison |
| **Extract repository files** | `github-extractor` | README, docs, config, source code |

---

## 📦 Available Agent

### github-extractor

**Purpose**: Expert GitHub data analyst for comprehensive repository insights

**What it does**:
- **Repository Analysis**: Search and analyze repos by language, stars, topics, activity
- **Issue Investigation**: Track issue status, labels, milestones, resolution patterns
- **Pull Request Analysis**: Examine code review processes, merge patterns, PR velocity
- **Commit History**: Analyze commit patterns, contributor activity, development velocity
- **Release Tracking**: Monitor releases, version numbers, release notes, assets
- **Content Retrieval**: Extract file contents (README, docs, config, source code)
- **Contributor Insights**: Identify top contributors, expertise areas, collaboration networks
- **Comprehensive Reporting**: Structured output with insights and direct GitHub links

**Input**:
- GitHub repository URL or owner/repo format
- Search queries (repositories, issues, PRs, code)
- Specific analysis requests (contributors, releases, etc.)

**Output**:
- Structured analysis reports with:
  - Repository metadata and statistics
  - Issue/PR summaries with trends
  - Contributor activity breakdown
  - Release history with notes
  - Code structure overview
  - Direct GitHub links for verification
  - Actionable insights and recommendations

**When to use**:
- Researching repositories before using or contributing
- Analyzing project health and activity metrics
- Monitoring issue resolution and PR workflows
- Tracking contributor patterns and collaboration
- Gathering release information and version history
- Extracting repository documentation and files
- Comparing multiple repositories or projects

**Typical analyses include**:
- Repository health indicators (recent activity, open vs closed issues)
- Development velocity (commits per week, PR merge time)
- Community engagement (contributor count, issue response time)
- Code quality signals (test coverage mentions, CI/CD presence)
- Release cadence and versioning patterns
- Popular topics and language breakdown
- Fork and star trends

**File**: `github-extractor.md`

---

## 🔄 Common Workflow Patterns

### Pattern 1: Repository Evaluation Before Use
```
github-extractor
    ↓
Analyze repo health metrics
    ↓
Check recent activity and issues
    ↓
Review contributor patterns
    ↓
[User decides: use/contribute/fork/skip]
```

### Pattern 2: Project Health Monitoring
```
github-extractor (periodic)
    ↓
Track issue resolution rate
    ↓
Monitor PR merge velocity
    ↓
Analyze contributor retention
    ↓
Generate health report
```

### Pattern 3: Multi-Repo Comparison
```
github-extractor (repo 1)
    ↓
github-extractor (repo 2)
    ↓
github-extractor (repo 3)
    ↓
[Compare metrics across repos]
    ↓
Recommendation report
```

### Future Pattern: Complete Repo Management
```
[When more Repo agents exist]

github-extractor (discovery)
    ↓
repo-issue-manager (issue triage and tracking)
    ↓
repo-pr-reviewer (automated PR review)
    ↓
repo-release-generator (release notes and versioning)
    ↓
repo-documenter (README and wiki updates)
```

---

## 📁 Output Locations

Agent writes to: **`project-context/Repo/{repo-name}/`**

```
project-context/
└── Repo/
    └── analyzed-repository/
        ├── repo_analysis.md          ← github-extractor
        ├── contributor_insights.md   ← github-extractor
        ├── issue_summary.md          ← github-extractor
        ├── pr_analysis.md            ← github-extractor
        ├── release_history.md        ← github-extractor
        └── _project_metadata.json    ← Tracking info
```

---

## 💡 Tips for Claude Code

### When to Use github-extractor

**Use when**:
- User provides GitHub repository URL
- User asks to "analyze repository", "check project health"
- User requests "find repositories about [topic]"
- User needs "contributor analysis", "issue tracking"
- User wants to "compare repositories"
- Before cloning/forking unknown repositories
- Monitoring existing projects

### Capabilities Breakdown

**Repository Search**:
- Find repos by language, stars, topics, activity
- Filter by organization, user, or global search
- Sort by relevance, stars, forks, updated date

**Issue Analysis**:
- Open vs closed issue ratio
- Average time to close
- Most common labels
- Milestone progress
- Stale issues identification

**PR Analysis**:
- Merge rate and average time
- Review patterns
- Contributor participation
- Failed vs successful PRs

**Contributor Insights**:
- Top contributors by commits
- Contribution frequency
- Expertise areas (files/modules)
- New vs veteran contributors

**Release Tracking**:
- Version numbering patterns
- Release frequency
- Breaking changes identification
- Asset downloads (if available)

### Future Expansion Suggestions

Consider adding to Repo/:
1. **repo-issue-tracker**: Automated issue triage and labeling
2. **repo-pr-reviewer**: Automated code review for PRs
3. **repo-release-manager**: Release notes generation and versioning
4. **repo-health-monitor**: Periodic health checks with alerts
5. **repo-workflow-orchestrator**: Coordinate repository management tasks

---

## 🎓 Examples for Claude Code

### Example 1: User Asks About a Repository

**Your decision**:
```
User: "Analyze the FastAPI repository on GitHub"
  ↓
Read Repo/agents/README.md
  ↓
Task = GitHub repo analysis → github-extractor
  ↓
Call: /github-extractor with "fastapi/fastapi"
  ↓
Return comprehensive analysis with health metrics
```

### Example 2: User Wants to Find Repositories

**Your decision**:
```
User: "Find Python web frameworks with >10k stars"
  ↓
Read Repo/agents/README.md
  ↓
Task = repo search → github-extractor
  ↓
Call: /github-extractor with search query
  ↓
Return list of matching repos with comparisons
```

### Example 3: User Tracks Project Issues

**Your decision**:
```
User: "What's the status of issues in my-org/my-repo?"
  ↓
Read Repo/agents/README.md
  ↓
Task = issue analysis → github-extractor
  ↓
Call: /github-extractor focusing on issues
  ↓
Return issue summary with trends
```

---

## 🔗 Related Documentation

- **Agent details**: See `github-extractor.md` in this directory
- **Creating new Repo agents**: See `../../meta-agent.md`
- **Atomic architecture**: See `../../README.md`

---

**Last Updated**: 2025-11-22
**Agent Count**: 1
**Category**: Repository Management & Analysis
**Platform**: GitHub (MCP GitHub Server integration)
