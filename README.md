# IIIF Presentation API 3.0

A place to mock together Northwestern works and collections as [IIIF Presentation API 3.0](https://iiif.io/api/presentation/3.0/) shapes.

- [Manifest](#manifest)
- [Collection](#collection)
- [Notes](#notes)
- [Omitted Properties](#omitted-properties)

## Manifest

A IIIF resource representing a work.

[Pantalone classico](https://dc.library.northwestern.edu/items/7298fdce-adc1-4501-9e14-9e8bd985e149) was selected as an example work for mocking a IIIF Manifest.

- [GitHub Example](https://github.com/nulib/iiif-presentation-3/blob/main/manifest/image-work-multi-canvas-1.json)
- [API Example](https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1)
- [View in Mirador](https://projectmirador.org/embed/?iiif-content=https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1)

---

### label

All manifests MUST include a label as an International String derived from the work's **title**. If a work does not have a title, an empty entry should be used, ex: `"{ label": "none": [""] }`.

https://iiif.io/api/presentation/3.0/#label

```json
{
  "label": {
    "none": ["Pantalone classico"]
  }
}
```

### summary

All manifests SHOULD include a `summary` as an International String derived from the work's **description**.

https://iiif.io/api/presentation/3.0/#summary

```json
{
  "summary": {
    "none": [
      "\"Magnifico\" - that is, great, grand, generous - means the exact opposite in this character, since the Commedia dell'Arte Magnifico is decidedly avaricious. But besides this extremely human defect, the Magnifico represents the highest authority in the family. He is the one who is in charge of not only the economy and finances, but also the destiny of the household and all who live there. He decides whether or not..."
    ]
  }
}
```

### metadata

All manifests SHOULD include a `metadata` property with an array of items for each distinct metadata label, e.g., Alternate Title, Subject, and Genre. We SHOULD omit **Rights Statement** and **Terms of Use** and instead use `rights` and `requiredStatement` for these respectively. We MAY also want to consider including data currently under _Find This Item_ such as **Box Number** and **Folder Name** within the `metadata` property. We MAY also want to represent **Work Type** as within `metadata`.

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
    },
    {
      "label": { "none": ["Work Type"] },
      "value": { "none": ["Image"] }
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

### thumbnail

All works with a representative image SHOULD include a `thumbnail` on their manifest. These SHOULD use the IIIF Image API URI and the include the corresponding `service` array.

```json
{
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
```

### homepage

All manifests SHOULD include a `homepage` property with the arrayed object having an `id` referencing the URL on the Northwestern University Libraries Digital Collections website. The `label` property SHOULD mirror the work title.

https://iiif.io/api/presentation/3.0/#homepage

```json
{
  "homepage": [
    {
      "id": "https://dc.library.northwestern.edu/items/7298fdce-adc1-4501-9e14-9e8bd985e149",
      "type": "Text",
      "label": { "none": ["Pantalone classico"] },
      "format": "text/html"
    }
  ]
}
```

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

### logo

We SHOULD include a `logo` property on a Manifest. The Libraries and RDC likely SHOULD host a permanant location of this web resource. If we choose to, we MAY want to provide the Northwestern Logo wordmark via a IIIF image service. Note that logo on a Manifest is the only currently for a logo to render in Mirador 3 -- and the `provider` logo is ignored.

> It is recommended that a IIIF Image API service be available for this image for other manipulations such as resizing.

https://iiif.io/api/presentation/3.0/#logo

```json
{
  "logo": [
    {
      "id": "https://www.northwestern.edu/brand/images/wordmark/wordmark-vert.jpg",
      "type": "Image",
      "format": "image/jpeg",
      "width": 400,
      "height": 210
    }
  ]
}
```

### provider

Manifests SHOULD include a `provider` property with an entry having `id`, `type`, `label`, `homepage`, and `logo`. Viewers such a Mirador will represent this information when presenting a manifest helping attribute providing insitutions when manifests are accessed _in the wild_.

https://iiif.io/api/presentation/3.0/#provider

```json
{
  "provider": [
    {
      "id": "https://www.library.northwestern.edu/",
      "type": "Agent",
      "label": {
        "none": ["Northwestern University Libraries"]
      },
      "homepage": [
        {
          "id": "https://dc.library.northwestern.edu/",
          "type": "Text",
          "label": {
            "none": ["Northwestern University Libraries Digital Collections"]
          },
          "format": "text/html"
        }
      ],
      "logo": [
        {
          "id": "https://www.northwestern.edu/brand/images/wordmark/wordmark-vert.jpg",
          "type": "Image",
          "format": "image/jpeg",
          "width": 400,
          "height": 210
        }
      ]
    }
  ]
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

### items

All works should contain at least one fileset that will correspond to a Canvas in the `items` property of a manifest. Each canvas will include an `Annotation` with a `"motivation": "painting"`. The `body` of this object should have a corresponding `type` of **Image**, **Sound**, or **Video**. A IIIF Image API URI and a corresponding service array should be used to serve **Image** resources.

```json
{
  "items": [
    {
      "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/0",
      "type": "Canvas",
      "width": 3780,
      "height": 4440,
      "label": {
        "none": ["Front"]
      },
      "items": [
        {
          "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/0/page/0",
          "type": "AnnotationPage",
          "items": [
            {
              "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/0/page/0/annotation/0",
              "type": "Annotation",
              "motivation": "painting",
              "target": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/0",
              "body": {
                "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/180682c9-dfaf-4881-b7b6-1f2f21092d4f/full/600,/0/default.jpg",
                "type": "Image",
                "format": "image/jpeg",
                "service": [
                  {
                    "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/180682c9-dfaf-4881-b7b6-1f2f21092d4f",
                    "profile": "http://iiif.io/api/image/2/level2.json",
                    "type": "ImageService2"
                  }
                ],
                "width": 3780,
                "height": 4440
              }
            }
          ]
        }
      ]
    },
    {
      "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/1",
      "type": "Canvas",
      "width": 5010,
      "height": 4396,
      "label": {
        "none": ["Left"]
      },
      "items": [
        {
          "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/1/page/0",
          "type": "AnnotationPage",
          "items": [
            {
              "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/1/page/0/annotation/0",
              "type": "Annotation",
              "motivation": "painting",
              "target": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/1",
              "body": {
                "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/b6359e7f-070c-4c86-aee1-515e5b6604e2/full/600,/0/default.jpg",
                "type": "Image",
                "format": "image/jpeg",
                "service": [
                  {
                    "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/b6359e7f-070c-4c86-aee1-515e5b6604e2",
                    "profile": "http://iiif.io/api/image/2/level2.json",
                    "type": "ImageService2"
                  }
                ],
                "width": 5010,
                "height": 4396
              }
            }
          ]
        }
      ]
    },
    {
      "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/2",
      "type": "Canvas",
      "width": 7230,
      "height": 5428,
      "label": {
        "none": ["Right"]
      },
      "items": [
        {
          "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/2/page/0",
          "type": "AnnotationPage",
          "items": [
            {
              "id": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/2/page/0/annotation/0",
              "type": "Annotation",
              "motivation": "painting",
              "target": "https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/items/iiif-image-manifest-1/canvas/2",
              "body": {
                "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/ca2acc2b-df00-4c6d-8373-ab6d5af17714/full/600,/0/default.jpg",
                "type": "Image",
                "format": "image/jpeg",
                "service": [
                  {
                    "id": "https://iiif.stack.rdc.library.northwestern.edu/iiif/2/ca2acc2b-df00-4c6d-8373-ab6d5af17714",
                    "profile": "http://iiif.io/api/image/2/level2.json",
                    "type": "ImageService2"
                  }
                ],
                "width": 7230,
                "height": 5428
              }
            }
          ]
        }
      ]
    }
  ]
}
```

## Collection

A IIIF resource representing a collection.

[Commedia dell'Arte: The Masks of Antonio Fava](https://dc.library.northwestern.edu/collections/c373ecd2-2c45-45f2-9f9e-52dc244870bd) was selected as an example collection for mocking a IIIF Collection.

- [GitHub Example](https://github.com/nulib/iiif-presentation-3/blob/main/collection/image-works.json)
- [API Example](https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/collections/iiif-image-collection)
- [View in Mirador](https://projectmirador.org/embed/?iiif-content=https://acw5dcf49d.execute-api.us-east-1.amazonaws.com/dev/collections/iiif-image-collection)

---

tbd.

### partOf

Collections MAY include a `partOf` property if we decide to create a top-level collection of collections.
https://iiif.io/api/presentation/3.0/#partof

Examples of top-level collections.

- Bodleian
  https://iiif.bodleian.ox.ac.uk/iiif/collection/top
- National Library of Scotland
  https://view.nls.uk/collections/top.json

## Notes

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

## Omitted Properties

### Behavior

We do not include behavior until we have have method for determining this. Clients SHOULD interpret our omission of `behavior` on IIIF resources as `individuals`

https://iiif.io/api/presentation/3.0/#behavior

_Individuals_

> Valid on Collections, Manifests, and Ranges. For Collections that have this behavior, each of the included Manifests are distinct objects in the given order. For Manifests and Ranges, the included Canvases are distinct views, and should not be presented in a page-turning interface. **This is the default layout behavior if not specified.** Disjoint with unordered, continuous, and paged.
