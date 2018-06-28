[![Latest Stable Version](https://poser.pugx.org/carbon/navigation/v/stable)](https://packagist.org/packages/carbon/navigation)
[![Total Downloads](https://poser.pugx.org/carbon/navigation/downloads)](https://packagist.org/packages/carbon/navigation)
[![License](https://poser.pugx.org/carbon/navigation/license)](LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/CarbonPackages/Carbon.Navigation.svg?style=social&label=Fork)](https://github.com/CarbonPackages/Carbon.Navigation/fork)
[![GitHub stars](https://img.shields.io/github/stars/CarbonPackages/Carbon.Navigation.svg?style=social&label=Stars)](https://github.com/CarbonPackages/Carbon.Navigation/stargazers)
[![GitHub watchers](https://img.shields.io/github/watchers/CarbonPackages/Carbon.Navigation.svg?style=social&label=Watch)](https://github.com/CarbonPackages/Carbon.Navigation/subscription)

# Carbon.Navigation Package for Neos CMS

This package provides various helps for implementing navigations in your Neos site.

## NodeTypes

All Node Types are marked as abstract. So you have to include them as supertypes if you want to use them. You can read more about Node Type definition [here](https://neos.readthedocs.io/en/stable/CreatingASite/NodeTypes/NodeTypeDefinition.html).

### `Carbon.Navigation:NotInMenu`

Hide the property `_hiddenInIndex`. Defined in [NodeTypes.NotInMenu.yaml](Configuration/NodeTypes.NotInMenu.yaml)

### `Carbon.Navigation:HideSeo`

Turn off all type of SEO properties. Defined in [NodeTypes.HideSeo.yaml](Configuration/NodeTypes.HideSeo.yaml)

### `Carbon.Navigation:RedirectToParentPage`

(Only in the live context) Redirect the user to the parent page. Defined in [NodeTypes.RedirectToParentPage.yaml](Configuration/NodeTypes.RedirectToParentPage.yaml) and [ToParentPage.fusion](Resources/Private/Fusion/Redirect/ToParentPage.fusion)

### `Carbon.Navigation:RedirectToFirstChildPage`

(Only in the live context) Redirect the user to the first child page, if available. If not, the user gets redirected to the parent page. Defined in [NodeTypes.RedirectToFirstChildPage.yaml](Configuration/NodeTypes.RedirectToFirstChildPage.yaml) and [ToFirstChildPage.fusion](Resources/Private/Fusion/Redirect/ToFirstChildPage.fusion)

### `Carbon.Navigation:References`

Insert a property called `navigationreferences`. This is very useful if you want to create a navigation and want the editor to choose which documents should be included. However, you can also pass a custom collection to the Fusion prototype. Defined in [NodeTypes.References.yaml](Configuration/NodeTypes.References.yaml) and [References.fusion](Resources/Private/Fusion/References/References.fusion)

## Menu Fusion prototypes

You can edit the default behavior of each fusion prototype in your [Settings.yaml](Configuration/Settings.yaml). The configuration which can be set via Settings.yaml can also be set directly in the corresponding Fusion prototype. The Setting is here to provide an easy way to change some basics without writing Fusion code. The main difference to the default menus is that if you have no item to render, no markup at all gets rendered.

### Properties for all menu prototypes

| Property     | Description                                                                                                                                                       |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `useBEM`     | (boolean) If set to `true`, the CSS classes get written in [BEM-Style](http://getbem.com). Defaults to `false`                                                    |
| `namespace`  | (string) You can easily change the namespace of the navigation. Useful if you have multiple navigations on your page. Defaults to the name of the prototype       |
| `wrapText`   | (boolean \|\| string) If `true`, the text inside the `a` gets wrapped with a `span`. If it is a string, this string will become the tag name. Defaults to `false` |
| `listTag`    | The tag of the full navigation gets wrapped. If it set to `false`, the navigation gets no surrounding tag. Defaults to `'ul'`                                     |
| `elementTag` | The tag a navigation entry gets wrapped. If it set to `false`, the entry gets no surrounding tag. Defaults to `'li'`                                              |

### `Carbon.Navigation:Menu`

Render a menu with items for nodes. Extends [Neos.Neos:Menu](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-menu). Besides the [default properties](#propertiesforallmenuprototypes) following properties are available:

| Property              | Description                                                                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| `maximumLevels`       | (integer) Restrict the maximum depth of items in the menu (relative to `entryLevel`) . Defaults to `2`                                              |
| `filter`              | (string) Filter items by node type, defaults to `'Neos.Neos:Document,!Carbon.Navigation:NotInMenu'`                                                 |
| `showHome`            | (boolean) If set to `true`, the homepage link gets rendererd in the menu. Done with `beforeFirst`. Defaults to `false`                              |
| `entryLevel`          | (integer) Start the menu at the given depth. If no `startingPoint` is set, it is defaults to `1`, otherwise `0`                                     |
| `startingPoint`       | (Node) The parent node of the first menu level                                                                                                      |
| `lastLevel`           | (integer) Restrict the menu depth by node depth (relative to site node)                                                                             |
| `renderHiddenInIndex` | (boolean) Whether nodes with `hiddenInIndex` should be rendered, defaults to `false`                                                                |
| `itemCollection`      | (array) Explicitly set the Node items for the menu (alternative to `startingPoints` and levels)                                                     |
| `beforeFirst`         | (boolean \|\| string) If set, the string gets injected **before the first item**. The variables `item`, `iteration` and `entryLevel` are available. |
| `afterLast`           | (boolean \|\| string) If set, the string gets injected **after the last item**. The variables `item`, `iteration` and `entryLevel` are available.   |
| `beforeItem`          | (boolean \|\| string) If set, the string gets injected **before every item**. The variables `item`, `iteration` and `entryLevel` are available.     |
| `afterItem`           | (boolean \|\| string) If set, the string gets injected **after every item**. The variables `item`, `iteration` and `entryLevel` are available.      |

In the variable `item` are following properties available:

| Property            | Description                                                                                                          |
| ------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `item.node`         | (Node) A node instance (with resolved shortcuts) that should be used to link to the item                             |
| `item.originalNode` | (Node) Original node for the item                                                                                    |
| `item.state`        | (string) Menu state of the item: `'normal'`, `'current'` (the current node) or `'active'` (ancestor of current node) |
| `item.label`        | (string) Full label of the node                                                                                      |
| `item.menuLevel`    | (integer) Menu level the item is rendered on                                                                         |
| `item.subItems`     | (array) The sub nodes from the current `item.node`. Useful to check if a page has subpages                           |

Defined in [Menu.fusion](Resources/Private/Fusion/Menu/Menu.fusion)

### `Carbon.Navigation:References`

Provides a list of links, based on nodes set in the inspector. Based on `Carbon.Navigation:Menu`. `itemCollection` is set to the closest instance of `Carbon.Navigation:References` who has the property `navigationreferences` set. `maximumLevels` defaults to `1` and `renderHiddenInIndex` defaults to `true`.

Defined in [References.fusion](Resources/Private/Fusion/Menu/References.fusion)

### `Carbon.Navigation:Breadcrumb`

Provides a breadcrumb navigation based on menu items. Based on `Carbon.Navigation:Menu`. `maximumLevels` is set to `1` and `listTag` defaults to `'ol'`.

| Property   | Description                                                                        |
| ---------- | ---------------------------------------------------------------------------------- |
| `sortDesc` | (boolean) If set to `true` the sort order is set to descending. Defaults to `true` |

Defined in [Breadcrumb.fusion](Resources/Private/Fusion/Menu/Breadcrumb.fusion)

### `Carbon.Navigation:Dimensions`

Create links to other node variants (e.g., variants of the current node in other dimensions) by using this Fusion object. Extends [Neos.Neos:DimensionsMenu](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-dimensionsmenu).

| Property              | Description                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------------------- |
| `renderCurrent`       | (boolean) If set to `false` the current dimension didn't get rendered. Defaults to `true`           |
| `dimension`           | (optional, string) name of the dimension which this menu should be based on. Example: `'language'`. |
| `presets`             | (optional, array): If set, the presets rendered will be taken from this list of preset identifiers  |
| `includeAllPresets`   | (boolean) If set to `true`, include all presets, not only allowed combinations. Defaults to `false` |
| `renderHiddenInIndex` | (boolean) Whether nodes with hiddenInIndex should be rendered, defaults to `true`                   |

Defined in [Dimensions.fusion](Resources/Private/Fusion/Menu/Dimensions.fusion)

## License

Licensed under MIT, see [LICENSE](LICENSE)
