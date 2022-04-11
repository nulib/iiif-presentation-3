# IIIF Presentation API 3.0

A place to mock together Northwestern works and collections as [IIIF Presentation API 3.0](https://iiif.io/api/presentation/3.0/) shapes.

## Common Assumptions

### Internationalization

International Strings have a language of `none` unless we have a metadata mechanism for determining this.

https://iiif.io/api/presentation/3.0/#label

```json
{
  "label": {
    "none": ["Pantalone classico"]
  },
  "metadata": [
    {
      "label": { "none": ["Alternate Title"] },
      "value": { "none": ["Fava"] }
    }
  ]
}
```

### Behavior

We do not include behavior until we have have method for determining this. Clients SHOULD interpret our omission of `behavior` on IIIF resources as `individuals`

https://iiif.io/api/presentation/3.0/#behavior

_Individuals_

> Valid on Collections, Manifests, and Ranges. For Collections that have this behavior, each of the included Manifests are distinct objects in the given order. For Manifests and Ranges, the included Canvases are distinct views, and should not be presented in a page-turning interface. **This is the default layout behavior if not specified.** Disjoint with unordered, continuous, and paged.

## Manifest

### items

...

### label

...

### logo

...

### metadata

All manifests SHOULD include a `metadata` property with an array of items for each distinct metadata label, e.g., Alternate Title, Subject, and Genre. We SHOULD omit **Rights Statement** and **Terms of Use** and instead use `rights` and `requiredStatement` for these respectively. We MAY also want to consider including data currently under _Find This Item_ such as **Box Number** and **Folder Name** within the `metadata` property.

https://iiif.io/api/presentation/3.0/#metadata

```json
{
  "metadata": [
    {
      "label": { "none": ["Alternate Title"] },
      "value": { "none": ["Fava"] }
    },
    {
      "label": { "none": ["Creator"] },
      "value": { "none": ["Fava, Antonio, 1949-"] }
    },
    {
      "label": { "none": ["Date"] },
      "value": { "none": ["2012"] }
    },
    {
      "label": { "none": ["Department"] },
      "value": {
        "none": ["Charles Deering McCormick Library of Special Collections"]
      }
    },
    {
      "label": { "none": ["Dimensions"] },
      "value": { "none": ["18 x 15 x 16 cm"] }
    },
    {
      "label": { "none": ["Genre"] },
      "value": { "none": ["comic masks"] }
    },
    {
      "label": { "none": ["Location"] },
      "value": { "none": ["Reggio Emilia"] }
    },
    {
      "label": { "none": ["Materials"] },
      "value": { "none": ["1 mask : grey leather, elastic, fiber"] }
    },
    {
      "label": { "none": ["Subject"] },
      "value": {
        "none": [
          "Masks",
          "Commedia dell'arte",
          "Italian drama (Comedy)",
          "Pantaloon (Fictitious character)"
        ]
      }
    }
  ]
}
```

Distinct values relating to each label should itemized in an array.

```json
{
  "label": { "none": ["Subject"] },
  "value": {
    "none": [
      "Masks",
      "Commedia dell'arte",
      "Italian drama (Comedy)",
      "Pantaloon (Fictitious character)"
    ]
  }
}
```

### partOf

All manifests SHOULD include a `partOf` property as all our published works are a part of a collection having a dereferencable IIIF Collection `id`. We MAY also choose to extend out properties in `partOf`to provide minimal contextual information about a work's parent collection -- doing so could limit number of requests on IIIF Collection resources that may have large items length. Proposed properties include: `label`, `summary`, `homepage`, and `thumbnail`.

https://iiif.io/api/presentation/3.0/#partof

```json
{
  "partOf": [
    {
      "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/collections/iiif-image-collection",
      "type": "Collection",
      "label": { "none": ["Commedia dell'Arte: The Masks of Antonio Fava"] },
      "summary": {
        "none": [
          "The Commedia dell'Arte, the famous improvisational theatre style born in Renaissance Italy, remains a major influence in today's theatre. Antonio Fava is an actor, comedian, author, director, musician, mask maker and Internationally renowned Maestro of Commedia dell'Arte."
        ]
      },
      "homepage": [
        {
          "id": "https://dc.library.northwestern.edu/collections/c373ecd2-2c45-45f2-9f9e-52dc244870bd",
          "type": "Text",
          "label": {
            "none": ["Commedia dell'Arte: The Masks of Antonio Fava"]
          },
          "format": "text/html"
        }
      ],
      "thumbnail": [
        {
          "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/180682c9-dfaf-4881-b7b6-1f2f21092d4f/full/200,/0/default.jpg",
          "type": "Image",
          "format": "image/jpeg",
          "service": [
            {
              "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/180682c9-dfaf-4881-b7b6-1f2f21092d4f",
              "profile": "http://iiif.io/api/image/2/level2.json",
              "type": "ImageService2"
            }
          ],
          "width": 200,
          "height": 200
        }
      ]
    }
  ]
}
```

### provider

...

### requiredStatement

All manifests MUST include a `requiredStatement` with a `label` of **Attribution** and a `value` of **Courtesy of Northwestern University Libraries**. If a work also has a distinct **Terms of Use** value, this SHOULD also be appended to the `value` array.

https://iiif.io/api/presentation/3.0/#requiredstatement

_Default_

```json
{
  "requiredStatement": {
    "label": {
      "none": ["Attribution"]
    },
    "value": {
      "none": ["Courtesy of Northwestern University Libraries"]
    }
  }
}
```

_Terms of Use_

```json
{
  "requiredStatement": {
    "label": {
      "none": ["Attribution"]
    },
    "value": {
      "none": [
        "Courtesy of Northwestern University Libraries",
        "These images are from material in the collections of the Charles Deering McCormick Library of Special Collections of Northwestern University Libraries, and are provided for use by its students, faculty and staff, and by other researchers visiting this site, for research consultation and scholarly purposes only. Further distribution and/or any commercial use of the images from this site is not permitted."
      ]
    }
  }
}
```

### rights

We SHOULD include the dereferenceable URI from a work's Rights Statement.

https://iiif.io/api/presentation/3.0/#rights

> The value MUST be drawn from the set of Creative Commons license URIs, the RightsStatements.org rights statement URIs, or those added via the extension mechanism.

```json
{
  "rights": "http://rightsstatements.org/vocab/InC/1.0/"
}
```

### seeAlso

We SHOULD include a `seeAlso` property that references the API endpoint which end-users can interact with.

https://iiif.io/api/presentation/3.0/#seealso

```json
{
  "seeAlso": [
    {
      "id": "https://dc.library.northwestern.edu/api/items/7298fdce-adc1-4501-9e14-9e8bd985e149",
      "type": "Dataset",
      "label": {
        "none": ["Northwestern University Libraries Digital Collections API"]
      },
      "format": "application/json",
      "profile": "https://dc.library.northwestern.edu/api/items/context.json"
    }
  ]
}
```

### summary

...

### thumbnail

...

# Collection

### partOf

Collections MAY include a `partOf` property if we decide to create a top-level collection of collections.
https://iiif.io/api/presentation/3.0/#partof

Examples of top-level collections.

- Bodleian
  https://iiif.bodleian.ox.ac.uk/iiif/collection/top
- National Library of Scotland
  https://view.nls.uk/collections/top.json
