---
name: conversation-summary
description: Summarize the current conversation and create a private GitHub gist. Use when the user asks to summarize the conversation, create a gist of the chat, or save the conversation summary.
---

# Conversation Summary & Gist Creator

This skill summarizes the current conversation and creates a private GitHub gist with the summary.

## Instructions

Follow these steps when this skill is invoked:

1. **Analyze the conversation**: Review all messages exchanged in the current conversation from the beginning.

2. **Create a structured summary** that includes:
   - **Title**: A brief, descriptive title for the conversation
   - **Overview**: 2-3 sentence summary of what was discussed
   - **Key Topics**: Bulleted list of main topics or tasks covered
   - **Actions Taken**: List of concrete actions, changes, or solutions implemented
   - **Outcomes**: Results achieved or current status
   - **Next Steps**: Any pending tasks or follow-up items (if applicable)

3. **Format the summary** in clear Markdown format with appropriate headers and structure.

4. **Create the gist**:
   - Generate a unique temporary filename using timestamp: `/tmp/conversation-summary-$(date +%Y%m%d%H%M%S).md`
   - Save the summary to this temporary file
   - Create a meaningful, searchable description (one sentence) based on the conversation title or key topics
   - Use the GitHub CLI to create a secret gist: `gh gist create /tmp/conversation-summary-TIMESTAMP.md --desc "MEANINGFUL_DESCRIPTION"`
   - Description should be short, include context keywords, and help find the gist in future searches
   - Example: "Built Claude Code skill for conversation summaries with race condition fixes"
   - Note: Gists are secret (private) by default; use `-p` or `--public` to make them public
   - Clean up the temporary file after the gist is created

5. **Report to the user**:
   - Show a brief version of the summary
   - Provide the gist URL for access
   - Confirm that the gist is private

## Notes

- GitHub CLI (`gh`) is always installed and authenticated - no need to check
- Keep the summary concise but comprehensive
- Use professional, clear language in the summary
