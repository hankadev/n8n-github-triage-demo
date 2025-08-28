# n8n GitHub Triage Demo

An automated GitHub issue triage system using n8n workflows and AI classification. This system automatically categorizes new GitHub issues with appropriate labels based on their content.

## Overview

This project demonstrates how to build an intelligent GitHub issue triage system that:

1. **Enforces consistent labeling** - Automatically applies "needs-triage" label to all new issues
2. **AI-powered classification** - Uses AI to analyze issue content and suggest appropriate labels
3. **Automated workflow** - Runs daily to process and categorize issues awaiting triage

## System Architecture

### GitHub Actions Workflow
- **Trigger**: Automatically runs when new issues are opened
- **Function**: Adds "needs-triage" label to all new issues
- **Purpose**: Ensures all new issues are marked for AI classification

### n8n Workflow
- **Trigger**: Daily cron job (with manual execution option for testing)
- **Process**:
  - Fetches all open issues with "needs-triage" label
  - Sends issue content to AI for classification
  - Applies appropriate labels based on AI response
  - Removes "needs-triage" label
  - Optionally adds AI-generated summary as comment

## AI Classification System

The AI analyzes issue titles and descriptions to provide structured classification:

### Output Format
```json
{
  "type": "bug | enhancement | question | documentation | tech-debt",
  "priority": "priority: high | priority: medium | priority: low",
  "complexity": "good-first-issue | regular | complex",
  "summary": "<short summary of the issue in less than 50 words>"
}
```

### Classification Rules

#### Issue Types
- **bug**: Broken functionality or unexpected behavior
- **enhancement**: Feature requests or improvements
- **question**: User inquiries or clarification requests
- **documentation**: Documentation-related issues
- **tech-debt**: Refactoring, internal cleanup, maintenance tasks

#### Priority Levels
- **priority: high**: Critical or urgent issues requiring immediate attention
- **priority: medium**: Important but not urgent issues
- **priority: low**: Minor, trivial, or cosmetic issues

#### Complexity Levels
- **good-first-issue**: Simple, well-defined issues easy for new contributors (styling, copy changes, small fixes). Priority is NOT high.
- **regular**: Standard issues that require some experience or understanding of the codebase
- **complex**: Difficult issues that may involve multiple components, advanced knowledge, or high-risk changes

## Setup Instructions

### Prerequisites
- GitHub repository with Issues enabled
- n8n instance (cloud or self-hosted)
- GitHub Personal Access Token with repo permissions

### GitHub Actions Setup

The GitHub Actions workflow is automatically triggered and requires no additional setup beyond having the workflow file in your repository.

### n8n Workflow Setup

- **Build the n8n workflow** following the diagram shown in `images/workflow.png`
- **Configure GitHub credentials** in n8n with your Personal Access Token
- **Set up the AI node** with your preferred AI service (OpenAI, Anthropic, etc.)
- **Configure the cron trigger** for execution (daily, weekly or as needed)
- **Test the workflow** using the manual trigger option

#### Building the Workflow

Refer to the workflow diagram in `images/workflow.png` to recreate the complete workflow structure. The diagram shows all the necessary nodes and their connections for the automated GitHub issue triage system.

## Project Structure

```
n8n-github-triage-demo/
├── README.md                       # Project documentation
├── prompt.txt                      # AI prompt template for issue classification
├── images/                         # Project screenshots and visual documentation
│   ├── before-running-workflow.png # Screenshot showing issues before workflow execution
│   ├── after-running-workflow.png  # Screenshot showing issues after workflow execution
│   └── workflow.png                # n8n workflow diagram
└── .github/
    └── workflows/
        └── add-needs-triage-label.yml  # GitHub Actions workflow
```

## Benefits

- **Consistent labeling** across all issues
- **Reduced manual triage** workload for maintainers
- **Better issue organization** and prioritization
- **Improved contributor experience** with clear categorization
- **Scalable solution** that works with high issue volumes

## Customization

The system can be easily customized by:
- Modifying the AI prompt in `prompt.txt`
- Adjusting label categories and priorities
- Changing the cron schedule in n8n
- Adding additional classification criteria

## License

This project is provided as-is for demonstration purposes.