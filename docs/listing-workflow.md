# Listing Workflow

This document explains the automated listing workflow for items in the repository.

## Overview

The listing workflow ensures that items added to the repository are listed on marketplaces and that the listings are properly tracked and validated.

## Workflow Steps

### 1. Item Added to Repository

When a new item PR is merged:
- A GitHub Action automatically creates a "listing-needed" issue
- The issue contains all item details including the unique item ID
- The issue is assigned to the repository owner

### 2. Create Marketplace Listing

The repository owner (or assigned person) must:
1. Create a listing on a marketplace
2. **IMPORTANT:** Include the item ID marker in the listing description: `#!#item-id#!#`
   - Example for item "tefal-blender-001": `#!#tefal-blender-001#!#`
   - You can put it anywhere in the description (beginning, middle, or end)
   - The marker can be on its own line or mixed with other text
3. Publish the listing

### 3. Submit Listing URL

Once the listing is live:
1. Add a comment to the listing issue with the URL
2. Use the format: `Listing URL: https://...`
3. The validation will start automatically - no need to close the issue

**Example comment:**
```
Listing URL: https://example.com/your-listing
```

### 4. Automatic Validation

When the URL is submitted, the system will:
- Check for the item ID marker in the listing
- Update the item status to `listed`
- Create a PR with listing details

### 5. PR Merge and Completion

After validation PR is merged:
- Issue closes automatically
- Item shows as listed

## Status Values

- `available` - Not yet listed
- `listed` - Has verified listing
- `pending` - Sale in progress
- `sold` - Completed sale
- `removed` - Listing removed

## Troubleshooting

If validation fails:
- Check URL format: `Listing URL: https://...`
- Verify marker `#!#item-id#!#` in listing
- Ensure listing is publicly accessible
