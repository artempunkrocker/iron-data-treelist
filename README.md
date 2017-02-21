# \<iron-data-treelist\>

`iron-data-treelist` builds treelist from your data

## Features v.0.1

* Building treelist via data
* Custom node content templates
* Expanding & collapsing nodes
* Non-modified user data 

## Using

### Template model
Node templates should bind to template models of the following structure:
```js
{
  expanded: false,  // true if node have been expanded for the current item
  level: 0,         // level of the node for the current item
  item: {}          // user data corresponding to items,
}
```

For example, given the following `data` array:
##### data.json
```js
[
  {
    "name: "Root Object",
    "items": [
      {
        "name" : "Child 1"
      },
      {
        "name": "Child 2",
        "items": [
          {
            "name": "Child 2.1",
            "items": [
              {
                "name": "Child 2.1.1"
              },
              {
                "name": "Child 2.1.2"
              },
              {
                "name": "Child 2.1.3"
              },
              {
                "name": "Child 2.1.4"
              }
            ]
          }
        ]
      }
    ]
  }
]
```

This sample demonstrates using of treelist:
```html
<template is="dom-bind">
  <iron-ajax url="data.json" last-response="{{data}}" auto></iron-ajax>
  <iron-data-treelist items="[[data]]">
    <template>
      [[item.name]]
    </template>
  </iron-data-treelist>
</template>
```

### Styling
There are several custom properties and mixins you can use to style the component:

Custom property | Description
----------------|--------------
`--node-indent` | Width of the node indent | `24px`
`--iron-data-treelist-node` | Mixin applied to the node
`--iron-data-treelist-node-hover` | Mixin applied to the node when its hovered
`--iron-data-treelist-expander` | Mixin applied to default expander icon
`--iron-data-treelist-expander-opened` | Mixin applied to opened default expander icon

## Roadmap

There are several planned features:

* Custom expander template
* Nodes focusing & selecting 
* Two-way data binding
* Data binding enhancement