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

*Individuals*
> Valid on Collections, Manifests, and Ranges. For Collections that have this behavior, each of the included Manifests are distinct objects in the given order. For Manifests and Ranges, the included Canvases are distinct views, and should not be presented in a page-turning interface. **This is the default layout behavior if not specified.** Disjoint with unordered, continuous, and paged.

## Types

### Manifest

#### requiredStatement

All manifests SHOULD include a `requiredStatement` with a `label` of **Attribution** and a `value` of **Courtesy of Northwestern University Libraries**. If a work also has a distinct **Terms of Use** value, this SHOULD also be appended to the `value` array.

https://iiif.io/api/presentation/3.0/#requiredstatement

_Default_
```jsx
{
"requiredStatement": {
  "label": {
    "none": ["Attribution"]
  },
  "value": {
    "none": [
      "Courtesy of Northwestern University Libraries"
    ]
  }
}
```

_Terms of Use_
```jsx
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
```


#### partOf
All manifests SHOULD include a `partOf` property as all our published works are a part of a collection having a dereferencable IIIF Collection `id`.

https://iiif.io/api/presentation/3.0/#partof


### Collection

#### partOf

Collections MAY include a `partOf` property if we decide to create a top-level collection of collections.
https://iiif.io/api/presentation/3.0/#partof

Examples of top-level collections.
- Bodleian
https://iiif.bodleian.ox.ac.uk/iiif/collection/top
- National Library of Scotland
https://view.nls.uk/collections/top.json
