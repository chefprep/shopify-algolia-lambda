# Shopify / Algolia Integration
This Module is a deep integration with Shopify and Algolia allowing you to rank, facet and replicate products including multi location inventory

This module deploys to AWS Lambda

<img src="https://logos-world.net/wp-content/uploads/2020/11/Shopify-Logo-700x394.png" alt="alt text" width="100">
<img src="https://user-images.githubusercontent.com/5952918/144704417-5bf94916-de01-4261-8f49-7b4a27fa38cb.png" alt="alt text" width="100">

## Install

You'll need serverless to run this and a AWS account or other provider
```bash
npm install -g serverless
```

## Config
set a `.env` file

```bash
SWELL_STORE_ID=***
SWELL_SECRET_KEY=***
TODO
```

## Algolia Config

Update the Algolia config (`algolia.config.json`) to what you need for your project.

| Field                   | Description                                                                          |
| ------------- | ------------- |
| `defaultRanking`        | The ranking of your default index `ALGOLIA_INDEX`                                    |
| `rankings`              | The individual rankings for using sort, will create a seperate replica per ranking |
| `searchableAttributes`  | Algolia searchable Attributes                                                        |
| `attributesForFaceting` | Algolia Facetable Attributes                                                         |

```json
{
  "defaultRanking": ["desc(name)"],
  "rankings": [
    {
      "suffix": "price_desc",
      "ranking": [
        "desc(price)"
      ]
    },
    {
      "suffix": "price_asc",
      "ranking": [
        "desc(price)"
      ]
    }
  ],
  "searchableAttributes": ["name"],
  "attributesForFaceting": ["attribute.brand", "categories"]
}
```

## Quick Start
The commands below will deploy the serverless function to AWS then create the indexes

```bash
sls deploy
sls invoke --function init
sls invoke --function reindex
```

`sls invoke --function init` will create the replicas based on your `algolia.config.json`
`sls invoke --function reindex` will pull all the products into Algolia


### Install webhooks on Shopify

TODO
