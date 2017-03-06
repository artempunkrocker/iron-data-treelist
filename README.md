# \<iron-data-treelist\>

`iron-data-treelist` builds treelist from your data.
Data must be an array of `Object` and each `Object` must contain
a `items` property for showing or hiding expander. 

## Features v.0.2

* Building treelist via data
* Custom node content templates
* Custom node expander templates
* Selecting nodes
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
    "name": "Root Object",
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

### Custom expander

Node's expanders are customizable.
Insert `template` tag into markup and add `is=expander` attribute to him to use your own templates.

Next sample demonstrates how to use custom expanders

```html
<template>
  <dom-module id="x-custom-expander">
    <template>
      <iron-ajax url="data.json" last-response="{{data}}" auto></iron-ajax>
      <iron-data-treelist items="[[data]]">
        <template>
          [[item.Title]]
        </template>
        <template is="expander">
          <iron-icon icon="[[iconForNode(expanded)]]"></iron-icon>
        </template>
      </iron-data-treelist>
    </template>
    <script>
      HTMLImports.whenReady(function() {
        Polymer({
          is: 'x-custom-expander',
          iconForNode: function(expanded) {
            return !expanded ? 'icons:add' : 'icons:remove';
          }
        })
      });
    </script>
  </dom-module>
</template>

<x-custom-expander></x-custom-expander>
```

### Styling
There are several custom properties and mixins you can use to style the component:

Custom property | Description
----------------|--------------
`--node-indent` | Width of the node indent | `24px`
`--iron-data-treelist-node` | Mixin applied to the node | `{}`
`--iron-data-treelist-node-selected` | Mixin applied to selected node | `{}`
`--iron-data-treelist-node-hover` | Mixin applied to the node when its hovered | `{}`
`--iron-data-treelist-expander` | Mixin applied to default expander icon | `{}`
`--iron-data-treelist-expander-opened` | Mixin applied to opened default expander icon | `{}`

## Roadmap

There are several planned features:

* Nodes focusing
* Two-way data binding
* Data binding enhancement