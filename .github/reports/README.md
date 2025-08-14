# Code Review Metrics Integration

This document describes the code review metrics integration added to the OpenVMM repository to track reviewer participation and identify review gaps.

## Overview

A new workflow has been added to automatically collect and analyze code review activity to answer key questions:
- Who is reviewing code in the repository?
- How many reviews is each person doing?
- Which contributors could participate more in code reviews?

## Workflow: Code Review Metrics (`code-review-metrics.yml`)

### Schedule and Triggers
- **Automatic Schedule:** Weekly on Mondays at midnight UTC
- **Manual Trigger:** Available via GitHub Actions UI with configurable time period
- **Default Analysis Period:** 30 days (customizable via manual trigger)

### Features
- Uses GitHub CLI to collect PR and review data directly from the repository
- Generates focused reports on reviewer activity and participation
- Automatically saves historical reports in `.github/reports/` directory
- Uploads artifacts with 90-day retention for long-term trend analysis
- Provides workflow summaries in GitHub Actions for quick overview
- Excludes bot accounts (GitHub Copilot, Dependabot, GitHub Actions) from analysis

### Generated Reports Include
- **Active Reviewers Table:** Shows who is reviewing code with review counts and PRs reviewed
- **Contributors Not Reviewing:** Identifies team members who have submitted code but haven't participated in reviews
- **Key Insights:** Most active reviewer, review participation rate, and engagement statistics

## Key Metrics and Insights

The workflow provides focused insights into code review participation:

### Reviewer Activity
- Who is actively reviewing code in the repository
- Number of reviews given by each reviewer
- Number of unique PRs reviewed by each person
- Most active reviewers and review volume distribution

### Team Participation
- Total number of active reviewers vs total contributors
- Review participation rate across team members
- Contributors who are submitting code but not reviewing
- Opportunities for increased review engagement

### Review Distribution
- How review workload is distributed across the team
- Average reviews per reviewer
- Balance of review participation across contributors

## Accessing Reports

### Automated Reports
- **Schedule:** Generated every Monday automatically
- **Location:** Artifacts section of GitHub Actions workflow runs
- **Retention:** 90 days for historical trend analysis
- **Format:** Markdown reports with structured data

### Manual Reports
- **Trigger:** Available in GitHub Actions → PR Statistics → Run workflow
- **Customization:** Configurable analysis period (default 30 days)
- **Use Cases:** Immediate analysis, custom time periods, special reviews

### Report Structure
- **Summary Overview:** Key statistics about reviewer activity and participation
- **Active Reviewers Table:** Who is reviewing code with review counts and PRs reviewed
- **Contributors Not Reviewing Section:** Team members who could participate more in reviews
- **Key Insights:** Most active reviewer, participation rate, and engagement metrics

## Benefits for Development Teams

### For Developers
- **See who is reviewing code** and understand review participation patterns
- **Track personal review contributions** and activity levels
- **Identify opportunities** to participate more in code reviews
- **Recognize active reviewers** contributing to code quality

### For Team Leads
- **Monitor reviewer participation** and engagement across the team
- **Balance review workload** by identifying who is reviewing and who could help more
- **Recognize review contributors** and their valuable contributions
- **Identify gaps** in review participation for team development

### For Project Managers
- **Measure review engagement** with concrete participation metrics
- **Plan review capacity** based on current reviewer activity
- **Report on team collaboration** with data-driven insights about review participation
- **Make informed decisions** about encouraging broader review participation

## Configuration and Customization

### Modifying the Schedule
To change the automatic report generation frequency:
1. Edit the `cron` expression in `.github/workflows/code-review-metrics.yml`
2. Current schedule: `'0 0 * * 1'` (weekly on Mondays)
3. Examples:
   - Daily: `'0 0 * * *'`
   - Bi-weekly: `'0 0 */14 * *'`
   - Monthly: `'0 0 1 * *'`

### Customizing Analysis Period
Default analysis covers the last 30 days, but this can be adjusted:
- **Manual runs:** Use the "days" input when triggering manually
- **Permanent change:** Modify the `default` value in the workflow file
- **Seasonal analysis:** Use longer periods (60-90 days) for quarterly reviews

### Bot Filtering
The workflow automatically excludes bot accounts from analysis:
- GitHub Copilot (`app/github-copilot`)
- Dependabot (`dependabot[bot]`)
- GitHub Actions (`github-actions[bot]`)

This ensures metrics focus on human team collaboration patterns.

## Security and Permissions

The workflow uses minimal required permissions:
- **`contents: read`** - Access repository contents
- **`pull-requests: read`** - Access PR data for analysis
- **`issues: read`** - Comprehensive repository activity analysis

All data analyzed is already available to repository contributors, and no sensitive information is exposed or stored.

## Troubleshooting

### Common Issues

#### Missing or Incomplete Reports
- **Cause:** Low review activity during analysis period
- **Solution:** Extend analysis period or check repository review activity

#### Workflow Not Running
- **Cause:** Repository inactivity (GitHub requirement for scheduled workflows)
- **Solution:** Trigger manually or ensure regular repository activity

#### No Contributors Not Reviewing
- **Cause:** All contributors are also participating in reviews
- **Result:** Report will show "All contributors are also participating in code reviews ✅"

#### Permission Errors
- **Cause:** Insufficient token permissions
- **Solution:** Verify `GITHUB_TOKEN` has required permissions (usually automatic)

### Debugging Steps
1. **Check Workflow Logs:** Review detailed logs in GitHub Actions
2. **Verify Triggers:** Ensure scheduled or manual triggers are working
3. **Review Artifacts:** Check if artifacts are being generated correctly
4. **Test Manual Run:** Try manual trigger with different parameters

## Future Enhancements

Potential improvements to consider:
- **Trend Analysis:** Track reviewer participation changes over time
- **Review Quality Metrics:** Analyze types of reviews (approvals, change requests, comments)
- **Automated Notifications:** Alert team leads about significant changes in review participation
- **Integration with Tools:** Connect with team management or recognition systems
- **Custom Metrics:** Team-specific participation goals and success measures
- **Review Balance Alerts:** Notify when review workload becomes unbalanced

## Getting Started

1. **Workflow is Active:** The code review metrics workflow is already configured and will run automatically
2. **Manual Trigger:** Go to Actions → Code Review Metrics → Run workflow for immediate analysis
3. **Review Reports:** Check workflow run artifacts for generated reports
4. **Monitor Participation:** Regular reports will help track reviewer engagement and identify opportunities

---

*For questions about code review metrics or issues with the workflow, check the GitHub Actions runs or create an issue in the repository.*