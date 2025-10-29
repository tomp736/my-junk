# Items for Sale

A repository for managing and listing items for sale, with automated workflows for submissions, marketplace listings, and removals.

## Quick Start

### Add an Item
1. Go to [Issues](../../issues/new/choose)
2. Select "Submit New Item for Sale"
3. Fill out the form
4. Submit - a PR will be created automatically

### Remove an Item
1. Go to [Issues](../../issues/new/choose)
2. Select "Remove Item from Sale"
3. Enter the Item ID
4. Submit - a PR will be created automatically

## Features

- ✅ **Automated item submission** via GitHub Issues
- ✅ **Automatic image downloading** and storage
- ✅ **Bilingual support** (English/Polish) for item content
- ✅ **Marketplace listing tracking** with validation
- ✅ **Automated item removal** workflow
- ✅ **Pull Request automation** for all changes

## Directory Structure

```
my-junk/
├── items/              # JSON files containing item listings
├── images/             # Product images and media files
├── docs/               # Documentation
├── .github/
│   ├── ISSUE_TEMPLATE/ # Issue templates for submissions
│   └── workflows/      # GitHub Actions automation
```

## Documentation

- **[Usage Guide](docs/usage.md)** - How to add and remove items
- **[Workflows](docs/workflows.md)** - Visual workflow diagrams
- **[Automation](docs/automation.md)** - Detailed automation documentation
- **[Listing Workflow](docs/listing-workflow.md)** - Marketplace listing process
- **[GitHub App Setup](docs/github-app-setup.md)** - Setting up authentication
- **[Item Schema](docs/item-schema.json)** - JSON schema for items

## Example

See [`items/example-item.json`](items/example-item.json) for a sample item listing.

## How It Works

1. **Submit** - User creates an issue with item details
2. **Validate** - GitHub Action validates and processes the submission
3. **PR Created** - Automated Pull Request is generated
4. **Review** - Maintainer reviews and merges the PR
5. **Listed** - Item is added/removed from repository
6. **Track** - Marketplace listing workflow begins (for new items)

For detailed workflow diagrams, see [Workflows Documentation](docs/workflows.md).

## Contributing

Please use the GitHub issue templates to ensure all required information is provided and to maintain consistency across listings.
