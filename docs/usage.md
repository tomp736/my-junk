# Usage Guide

This guide explains how to add and remove items from the repository.

## Adding Items

### Method 1: Submit via GitHub Issues (Recommended)

1. Click on the "Issues" tab in this repository
2. Click "New Issue"
3. Select "Submit New Item for Sale"
4. Fill out the form with your item details in both English and Polish
5. Submit the issue

**What happens next:**

Once you submit the issue, a GitHub Action will automatically:
- Parse your submission and create a JSON file
- Download any images you provided
- Create a new branch for the item
- Generate a Pull Request with the item details
- Comment on your issue with the PR link

The item will be added to the repository once the PR is reviewed and merged by a maintainer.

After the item is added, a "listing-needed" issue will be automatically created. See [Listing Workflow](listing-workflow.md) for details on creating marketplace listings.

### Method 2: Direct Commit

If you prefer to commit directly:

1. Create a new JSON file in the `items/` directory
2. Follow the item schema template (see `docs/item-schema.json`)
3. Add corresponding images to the `images/` directory
4. Reference images using relative paths in the item listing
5. Submit a Pull Request

**Example:**

See `items/example-item.json` for a sample item listing.

## Removing Items

### Submit via GitHub Issues

1. Click on the "Issues" tab in this repository
2. Click "New Issue"
3. Select "Remove Item from Sale"
4. Enter the Item ID of the item you want to remove
5. Select a reason for removal (Sold, No longer available, etc.)
6. Submit the issue

**What happens next:**

Once you submit the issue, a GitHub Action will automatically:
- Validate that the item exists
- Create a Pull Request to remove the item and its images
- Comment on your issue with the PR link

The item will be removed from the repository once the PR is reviewed and merged by a maintainer. The issue will close automatically after the PR is merged.

## Item Schema

Each item listing must follow the schema defined in `docs/item-schema.json`.

### Required Fields

- `id`: Unique identifier (e.g., "tefal-blender-001")
- `title`: Object with `en` and `pl` properties for English and Polish titles
- `description`: Object with `en` and `pl` properties for descriptions
- `price`: Numeric price value
- `currency`: Currency code (PLN, EUR, USD, GBP, CAD, AUD)
- `condition`: Item condition (new, like-new, good, fair, poor)
- `category`: Category (e.g., electronics, furniture, clothing)
- `status`: Current status (available, listed, pending, sold, removed)

### Optional Fields

- `images`: Array of image paths
- `location`: Where the item is available
- `tags`: Array of tags for searching
- `listingUrl`: URL to marketplace listing
- `listedDate`: Date when listed on marketplace
- `datePosted`: Date when added to repository

### Bilingual Content

All text fields (title, description) must be provided in both English and Polish:

```json
{
  "title": {
    "en": "Tefal Blender",
    "pl": "Blender Tefal"
  },
  "description": {
    "en": "High-powered blender in excellent condition",
    "pl": "Mocny blender w doskonałym stanie"
  }
}
```

## Currency

Items are typically priced in Polish Złoty (PLN), but other currencies (EUR, USD, GBP, CAD, AUD) are also supported.

## Tips

- Use descriptive item IDs (e.g., "tefal-blender-001" instead of "item-001")
- Provide high-quality images
- Be detailed in your descriptions
- Keep both English and Polish descriptions synchronized
- Use relevant tags for better searchability
