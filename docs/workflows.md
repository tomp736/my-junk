# Workflow Diagrams

Visual representation of the automated workflows in this repository.

## Adding Items Workflow

This diagram shows the complete process from item submission to marketplace listing.

```mermaid
flowchart TD
    Start([User Creates Issue]) --> A[Submit New Item for Sale]
    A -->|Issue Created| B[On Issue - Create Item]
    B --> C{Parse Issue Data}
    C --> D[Download Images]
    D --> E[Create Item JSON]
    E --> F[Create Branch & PR]
    F --> G[Comment on Issue with PR Link]

    G --> H{Maintainer Reviews PR}
    H -->|Merge| I[Item Added to Repository]
    H -->|Request Changes| J[Update Issue]
    J --> H

    I --> K[On PR Merge - Create Listing Issue]
    K --> L[Create listing-needed Issue]

    L --> M[Owner Creates Marketplace Listing]
    M --> N[Include #!#item-id#!# marker]
    N --> O[Add Comment: Listing URL]

    O --> P[On Comment - Validate Listing URL]
    P --> Q{Validate Listing}
    Q -->|Valid| R[Add listing-verified Label]
    Q -->|Invalid| S[Comment Error on Issue]
    S --> O

    R --> T[Create Validation PR]
    T --> U{Maintainer Merges PR}
    U -->|Merge| V[Update Item with Listing URL]

    V --> W[On PR Merge - Close Listing Issue]
    W --> X[Close listing-needed Issue]
    X --> End([Complete])

    style Start fill:#90EE90
    style End fill:#90EE90
    style B fill:#87CEEB
    style K fill:#87CEEB
    style P fill:#87CEEB
    style W fill:#87CEEB
    style Q fill:#FFB6C1
    style H fill:#FFB6C1
    style U fill:#FFB6C1
```

## Removing Items Workflow

This diagram shows the process for removing an item from the repository.

```mermaid
flowchart TD
    Start([User Creates Issue]) --> A[Remove Item from Sale]
    A -->|Issue Created| B[On Issue - Remove Item]
    B --> C{Validate Item Exists}
    C -->|Not Found| D[Comment Error & Add invalid Label]
    C -->|Found| E[Delete Item & Images]
    E --> F[Create Branch & PR]
    F --> G[Comment on Issue with PR Link]

    G --> H{Maintainer Reviews PR}
    H -->|Merge| I[Item Removed from Repository]
    H -->|Request Changes| J[Update Issue]
    J --> H

    I --> K[On PR Merge - Close Remove Issue]
    K --> L[Close remove-item Issue]
    L --> End([Complete])

    style Start fill:#90EE90
    style End fill:#90EE90
    style B fill:#87CEEB
    style K fill:#87CEEB
    style C fill:#FFB6C1
    style H fill:#FFB6C1
    style D fill:#FF6B6B
```

## Workflow States

### Item Creation States

1. **Issue Created** - User submits new item via issue template
2. **Parsing** - Workflow extracts item details and downloads images
3. **PR Created** - Automated PR with item JSON and images
4. **Under Review** - Maintainer reviews the PR
5. **Merged** - Item added to repository
6. **Listing Needed** - Tracking issue created for marketplace listing
7. **Listing Created** - Owner creates marketplace listing
8. **Validation** - System validates listing URL
9. **Complete** - Item fully listed and tracked

### Item Removal States

1. **Issue Created** - User submits removal request via issue template
2. **Validation** - Workflow checks if item exists
3. **PR Created** - Automated PR to delete item and images
4. **Under Review** - Maintainer reviews the PR
5. **Merged** - Item removed from repository
6. **Complete** - Issue closed automatically

## Validating Existing Listings Workflow

This diagram shows the automated nightly validation of marketplace listings.

```mermaid
flowchart TD
    Start([Scheduled: Nightly 2AM UTC]) --> A[Nightly - Validate All Listings]
    A --> B[Find All Items with status='listed']
    B --> C{For Each Item}

    C --> D[Fetch Listing URL]
    D --> E{Page Exists?}

    E -->|No - 404| F[Mark as Invalid]
    E -->|Yes| G{Marker Present?}

    G -->|No| F
    G -->|Yes| H[Listing Valid ✓]

    F --> I[Create listing-needed Issue]
    I --> J[Add listing-expired Label]
    J --> K[Update Item Status to 'available']
    K --> L[Remove Listing URL]

    H --> M{More Items?}
    L --> M

    M -->|Yes| C
    M -->|No| N{Any Invalid?}

    N -->|Yes| O[Create PR with Status Updates]
    N -->|No| P[All Listings Valid ✓]

    O --> Q[Add Comment with Details]
    Q --> R{Maintainer Reviews PR}
    R -->|Merge| S[Status Updates Applied]
    S --> End([Complete])

    P --> End

    style Start fill:#90EE90
    style End fill:#90EE90
    style A fill:#87CEEB
    style H fill:#90EE90
    style P fill:#90EE90
    style E fill:#FFB6C1
    style G fill:#FFB6C1
    style N fill:#FFB6C1
    style R fill:#FFB6C1
    style F fill:#FF6B6B
```

### Validation States

1. **Scheduled Run** - Workflow triggers at 2:00 AM UTC (or manually)
2. **Find Items** - Searches for all items with status "listed" and a listing URL
3. **Validation Loop** - For each item, checks if listing is still valid
4. **Valid Check** - Verifies page exists (HTTP 200) and marker is present
5. **Invalid Handling** - Creates listing-needed issue and updates item status
6. **PR Creation** - If any invalid listings found, creates PR with status changes
7. **Complete** - Validation cycle finishes

**Schedule:**
- Runs automatically every night at 2:00 AM UTC
- Can be triggered manually from GitHub Actions tab

## Color Legend

- 🟢 **Green**: Start/End points or success states
- 🔵 **Blue**: Automated GitHub Actions
- 🌸 **Pink**: Decision points requiring review or validation
- 🔴 **Red**: Error/invalid states

## Related Documentation

- [Usage Guide](usage.md) - How to add and remove items
- [Automation](automation.md) - Detailed automation documentation
- [Listing Workflow](listing-workflow.md) - Marketplace listing process
- [GitHub App Setup](github-app-setup.md) - Setting up authentication
