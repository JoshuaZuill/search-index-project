# Product Search and Analytics Demo

A JavaScript portfolio project exploring product data transformation, search integration and behavioural analytics with Algolia.

The project connects catalogue data with an interactive search interface. Its focus is the work behind a useful search experience: preparing records, applying business rules, capturing user interactions and tuning relevance.

## Project scope

### Catalogue transformation

The data workflow starts with the product catalogue in `data/`. A category-specific promotion illustrates how a business requirement can be expressed as a predictable transformation:

- Identify products in the camera category.
- Reduce their original prices by 20%.
- Round each discounted price down to the nearest whole number.
- Preserve the remaining product information for indexing.

For example, an original price of `149.99` becomes `119` after the discount and rounding. Always transform from the original source data so repeated imports do not compound the discount.

### Search integration

Algolia provides the search index used by the frontend. The intended data flow is:

```text
Source catalogue → Data transformation → Algolia index → Search interface
                                                              ↓
                                                     Interaction events
                                                              ↓
                                                       Algolia Insights
```

### Interaction analytics

Click and conversion events connect search results with user actions. The project scope includes using Algolia Insights to explore how these signals can support search analysis and personalisation.

Useful validation questions include whether events identify the correct product, distinguish clicks from conversions and retain the context of the originating search.

### Search relevance

Relevance work focuses on helping users find appropriate products through searchable attributes, filters and ranking choices. Evaluate changes against representative queries and expected results, rather than relying on a single successful search.

## Run the frontend locally

### Prerequisites

- Node.js and npm compatible with the repository's package configuration
- An Algolia application and search index
- The environment values described in `.env.example`

### Setup

1. Clone the repository and open its root directory.
2. Copy the environment template:

   ```sh
   cp .env.example .env
   ```

3. Set the application ID, appropriate API key and index name using the variable names already provided in `.env.example`.
4. Install dependencies and start the frontend:

   ```sh
   npm install
   npm start
   ```

Use the local URL printed by the development server. The catalogue must be imported into the configured index before it can appear in search results. The import command depends on the repository's data-processing script and is separate from starting the frontend.

## Configuration and credentials

Use a search-only key for browser-side search. Keep write-capable or administrative credentials in the server-side data-import environment. An environment variable bundled into frontend JavaScript is visible to users and must not contain a secret.

Keep local credentials out of version control. When deploying, configure the corresponding environment values in the hosting provider and confirm which values are included in the client bundle.

## Reviewing the project

The most useful areas to inspect when reviewing the JavaScript are:

- **Data handling:** category matching, numeric transformations and preservation of record structure.
- **API integration:** preparing records, sending data and handling unsuccessful operations.
- **Event handling:** connecting UI actions to analytics events without duplicate or misleading signals.
- **Configuration:** separating runtime settings from application logic.
- **Communication:** making the data flow and business rules understandable to another developer.

## Validation checklist

- Confirm that only the target category receives the promotion.
- Compare transformed prices with the original catalogue and the rounding rule.
- Check that non-target records and product identifiers remain intact.
- Verify that indexed products are returned by representative searches.
- Inspect click and conversion events for the correct product and search context.
- Review relevance changes against a small, repeatable set of queries.
- Confirm that no privileged credentials are exposed in the browser or committed files.

## Deployment

Deploy the frontend using a host compatible with the repository's framework and build configuration, such as Netlify or Vercel. Use the build command and output directory defined by the project rather than assuming defaults. Configure the Algolia environment values on the host and verify search and event behaviour after deployment.

