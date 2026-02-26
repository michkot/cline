# How to Use the MR Text

This repository now contains `MR_TEXT.md` - a comprehensive pull request description prepared according to the Cline project's pull request template.

## What's Included

The MR text document contains:

1. **Related Issue Section**: Placeholder for the GitHub issue number (currently `#XXXX`)
2. **Description**: Detailed explanation of the changes
   - Problem statement
   - Solution overview
   - Impact analysis
3. **Test Procedure**: Comprehensive testing approach and verification steps
4. **Type of Change**: Categorization checkboxes (Bug fix + New feature)
5. **Pre-flight Checklist**: Confirmation of readiness
6. **Screenshots**: Note about applicability (N/A for this backend change)
7. **Additional Notes**: Technical details, rationale, and compatibility information

## What This PR Does

This PR adds support for respecting the `SHELL` environment variable on Windows (win32) platforms. The key changes are:

- **Modified Files**:
  - `src/core/prompts/system-prompt/components/system_info.ts` - Added `getEffectiveShell()` function
  - `src/integrations/terminal/standalone/StandaloneTerminalProcess.ts` - Added `getDefaultShell()` method

- **Behavior Change**:
  - Windows shell detection now checks `process.env.SHELL` first before falling back to `COMSPEC` or `cmd.exe`
  - This allows users with Git Bash, Cygwin, MSYS2, or other alternative shells to use their preferred shell
  - Maintains full backward compatibility

## How to Use This Text

### Option 1: Copy to PR Description
1. Open the pull request on GitHub
2. Copy the contents of `MR_TEXT.md`
3. Paste into the PR description field
4. **Important**: Replace `#XXXX` with the actual issue number if there is one, or use "N/A" for small fixes

### Option 2: Use as Reference
- Use the document as a reference when filling out the GitHub PR template
- Ensure all sections are addressed with the information provided

## Before Submitting

Make sure to:
- [ ] Replace `#XXXX` with the actual GitHub issue number (or indicate N/A if no issue exists for this small enhancement)
- [ ] Verify all information is accurate
- [ ] Confirm tests are passing
- [ ] Review the [contributor guidelines](https://github.com/cline/cline/blob/main/CONTRIBUTING.md)

## Notes

- The MR text follows the template at `.github/pull_request_template.md`
- All sections are complete and ready to use
- The description emphasizes the minimal, surgical nature of the changes
- Backward compatibility is clearly documented
- Test coverage is explained comprehensively
