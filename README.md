# Strapi
This repo is for reproducing this bug: https://github.com/strapi/strapi/issues/9239 (I wish it wouldn't happen...)

Was initialized with command:

`yarn create strapi-app my-project-3.5.2 --quickstart`

Super Admin:
```
thebit@i.ua
Qwerty123
```
## Steps to reproduce
1. git clone https://github.com/TheBit/strapi-issue-9239.git
1. cd my-project-3.5.2
1. yarn install
1. yarn build
1. yarn develop
1. open http://localhost:1337/graphql
1. send query:
```
{
  page(id: 1) {
    title
    uiComponents {
      __typename
      ... on ComponentItemsItemsListBroken {
        defaultCategory {
          name
          items {
            item {
              name
            }
          }
        }
        categories {
          broken_category {
            name
            items {
              item {
                name
              }
            }
          }
        }
      }
      ... on ComponentItemsItemsListFixed {
        defaultCategory {
          name
          items {
            name
          }
        }
        categories {
          fixed_category {
            name
            items {
              name
            }
          }
        }
      }
    }
  }
}
```
8. see the response:
```
{
  "data": {
    "page": {
      "title": "Homepage",
      "uiComponents": [
        {
          "__typename": "ComponentItemsItemsListBroken",
          "defaultCategory": {
            "name": "Sedan",
            "items": null
          },
          "categories": [
            {
              "broken_category": {
                "name": "Crossover",
                "items": null
              }
            },
            {
              "broken_category": {
                "name": "Sedan",
                "items": null
              }
            }
          ]
        },
        {
          "__typename": "ComponentItemsItemsListFixed",
          "defaultCategory": {
            "name": "Crossover",
            "items": [
              {
                "name": "Toyota RAV4"
              },
              {
                "name": "Subaru Forester"
              }
            ]
          },
          "categories": [
            {
              "fixed_category": {
                "name": "Sedan",
                "items": [
                  {
                    "name": "Toyota Camry"
                  }
                ]
              }
            },
            {
              "fixed_category": {
                "name": "Crossover",
                "items": [
                  {
                    "name": "Toyota RAV4"
                  },
                  {
                    "name": "Subaru Forester"
                  }
                ]
              }
            }
          ]
        }
      ]
    }
  }
}
```
