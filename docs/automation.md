# Automation

This repository uses GitHub Actions with a GitHub App to automate the item submission, listing, and removal processes.

## Setup

For detailed setup instructions, see [GitHub App Setup](github-app-setup.md).

**Requirements:**
- A GitHub App with appropriate permissions (Contents, Pull Requests, Issues)
- GitHub App ID stored as repository variable: `GH_APP_AUTOMATION_APP_ID`
- GitHub App private key stored as repository secret: `GH_APP_AUTOMATION_APP_PRIVATE_KEY`

## Workflows

### Item Creation Workflow

**Workflow:** `.github/workflows/create-item.yml`
**Name:** "On Issue - Create Item"
**Trigger:** Issue opened or labeled with `new-item`
**Purpose:** Automate item submission

**Process:**
1. Parses the issue body to extract item details
2. Downloads images from URLs or GitHub-uploaded attachments
3. Creates item JSON file following the schema
4. Creates a new branch with the item and images
5. Generates a Pull Request
6. Comments on the issue with the PR link
7. Adds `processed` label to the issue

**Labels used:**
- `new-item`: Triggers the workflow
- `pending-review`: Applied when issue is created
- `processed`: Applied after PR is created
- `invalid`: Applied if parsing fails

### Listing Creation Workflow

**Workflow:** `.github/workflows/create-listing-issue.yml`
**Name:** "On PR Merge - Create Listing Issue"
**Trigger:** PR with `new-item` label merged to main
**Purpose:** Create tracking issue for marketplace listing

**Process:**
1. Detects when an item PR is merged
2. Extracts item details from the merged JSON file
3. Creates a "listing-needed" issue with item details and images
4. Assigns the issue to the repository owner

For details on the listing process, see [Listing Workflow](listing-workflow.md).

### Listing Validation Workflow

**Workflow:** `.github/workflows/validate-listing.yml`
**Name:** "On Comment - Validate Listing URL"
**Trigger:** Comment on `listing-needed` issue with "Listing URL:"
**Purpose:** Validate marketplace listing

**Process:**
1. Extracts the listing URL from the comment
2. Fetches the listing page content
3. Checks for the item ID marker (`#!#item-id#!#`)
4. Creates a PR to update the item with listing details
5. Adds `listing-verified` label

### Listing Issue Closure Workflow

**Workflow:** `.github/workflows/close-listing-issue.yml`
**Name:** "On PR Merge - Close Listing Issue"
**Trigger:** PR with `listing-validated` label merged to main
**Purpose:** Close the listing-needed issue

**Process:**
1. Extracts the issue number from the PR body
2. Adds a completion comment to the issue
3. Closes the issue

### Validate Existing Listings Workflow

**Workflow:** `.github/workflows/validate-existing-listings.yml`
**Name:** "Nightly - Validate All Listings"
**Trigger:** Scheduled (nightly at 2:00 AM UTC) or manual dispatch
**Purpose:** Periodically validate all marketplace listings

**Process:**
1. Finds all items with status `listed` and a `listingUrl`
2. For each item:
   - Fetches the marketplace listing page
   - Checks if the page exists (HTTP 200)
   - Verifies the item ID marker (`#!#item-id#!#`) is still present
3. For invalid listings:
   - Creates a new "listing-needed" issue with `listing-expired` label
   - Updates item status to `available`
   - Removes listing URL and listed date
4. Creates a PR with all status updates
5. Comments on the PR with details about invalid listings

**Why this is needed:**
- Marketplace listings may be removed or expired
- Items may be sold on the marketplace but not removed from repository
- Links may become broken over time
- Ensures the repository stays synchronized with marketplace status

**Schedule:**
- Runs automatically every night at 2:00 AM UTC
- Can be triggered manually from the Actions tab

### Item Removal Workflow

**Workflow:** `.github/workflows/remove-item.yml`
**Name:** "On Issue - Remove Item"
**Trigger:** Issue opened or labeled with `remove-item`
**Purpose:** Automate item removal

**Process:**
1. Parses the issue body to extract item ID
2. Validates that the item file exists
3. Reads the item to find associated images
4. Creates a PR to delete the item and images
5. Comments on the issue with the PR link
6. Adds `processed` or `invalid` label

### Remove Issue Closure Workflow

**Workflow:** `.github/workflows/close-remove-issue.yml`
**Name:** "On PR Merge - Close Remove Issue"
**Trigger:** PR with `remove-item` label merged to main
**Purpose:** Close the remove-item issue

**Process:**
1. Extracts the issue number from the PR body
2. Adds a completion comment to the issue
3. Closes the issue

## Labels

The automation system uses several labels to track workflow states:

| Label | Purpose |
|-------|---------|
| `new-item` | Triggers item creation workflow |
| `remove-item` | Triggers item removal workflow |
| `listing-needed` | Item needs marketplace listing |
| `listing-verified` | Listing URL has been validated |
| `listing-expired` | Previous listing is no longer valid (used with listing-needed) |
| `listing-validation` | Applied to PRs that update item status from validation |
| `pending-review` | Awaiting manual review |
| `processed` | Automation completed successfully |
| `invalid` | Validation failed (e.g., item not found, parsing error) |

## Error Handling

Each workflow includes error handling:

- **Validation errors**: Adds `invalid` label and comments on the issue with the error
- **Missing data**: Comments on the issue with details about what's missing
- **Network errors**: Fails gracefully and logs the error
- **Permission errors**: Fails with clear error message about GitHub App permissions

## Security

- All workflows use GitHub App authentication for better security
- Private key is stored as a repository secret
- Workflows run in isolated environments
- Only maintainers can merge PRs created by automation

## Troubleshooting

### Workflow not triggering
- Check that labels are spelled correctly
- Verify the GitHub App is installed on the repository
- Check workflow permissions in repository settings

### Authentication errors
- Verify `GH_APP_AUTOMATION_APP_ID` variable is set
- Verify `GH_APP_AUTOMATION_APP_PRIVATE_KEY` secret is set correctly
- Check that the private key includes header/footer lines
- Ensure the GitHub App has the required permissions

### PR creation fails
- Check that the GitHub App has "Contents" and "Pull requests" write permissions
- Verify the default branch is `main`

For more troubleshooting help, see the individual workflow files or [GitHub App Setup](github-app-setup.md).
