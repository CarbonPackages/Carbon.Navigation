[![Latest Stable Version](https://poser.pugx.org/carbon/navigation/v/stable)](https://packagist.org/packages/carbon/navigation)
[![Total Downloads](https://poser.pugx.org/carbon/navigation/downloads)](https://packagist.org/packages/carbon/navigation)
[![License](https://poser.pugx.org/carbon/navigation/license)](LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/CarbonPackages/Carbon.Navigation.svg?style=social&label=Fork)](https://github.com/CarbonPackages/Carbon.Navigation/fork)
[![GitHub stars](https://img.shields.io/github/stars/CarbonPackages/Carbon.Navigation.svg?style=social&label=Stars)](https://github.com/CarbonPackages/Carbon.Navigation/stargazers)
[![GitHub watchers](https://img.shields.io/github/watchers/CarbonPackages/Carbon.Navigation.svg?style=social&label=Watch)](https://github.com/CarbonPackages/Carbon.Navigation/subscription)

# Carbon.Navigation Package for Neos CMS

This package provides various helps for implementing navigations in your Neos site.

# NodeTypes

All Node Types are marked as abstract. So you have to include them as supertypes if you want to use them. You can read more about Node Type definition [here](https://neos.readthedocs.io/en/stable/CreatingASite/NodeTypes/NodeTypeDefinition.html).

## `Carbon.Navigation:NotInMenu`

Hide the property `_hiddenInIndex`. Defined in [NodeTypes.NotInMenu.yaml](Configuration/NodeTypes.NotInMenu.yaml)

## `Carbon.Navigation:HideSeo`

Turn off all type of SEO properties. Defined in [NodeTypes.HideSeo.yaml](Configuration/NodeTypes.HideSeo.yaml)

## `Carbon.Navigation:RedirectToParentPage`

(Only in the live context) Redirect the user to the parent page. Defined in [NodeTypes.RedirectToParentPage.yaml](Configuration/NodeTypes.RedirectToParentPage.yaml) and [ToParentPage.fusion](Resources/Private/Fusion/Redirect/ToParentPage.fusion)

## `Carbon.Navigation:RedirectToFirstChildPage`

(Only in the live context) Redirect the user to the first child page, if available. If not, the user gets redirected to the parent page. Defined in [NodeTypes.RedirectToFirstChildPage.yaml](Configuration/NodeTypes.RedirectToFirstChildPage.yaml) and [ToFirstChildPage.fusion](Resources/Private/Fusion/Redirect/ToFirstChildPage.fusion)

## `Carbon.Navigation:References`

Insert a property called `navigationreferences`. It is handy if you want to create a navigation and wants to let the editor to choose which documents should be included. However, you can also pass a custom collection to the Fusion prototype. Defined in [NodeTypes.References.yaml](Configuration/NodeTypes.References.yaml) and [References.fusion](Resources/Private/Fusion/References/References.fusion)

# Menu Fusion prototypes

You can edit the default behavior of each fusion prototype in your [Settings.yaml](Configuration/Settings.yaml). You can set the configuration via Settings.yaml or directly in the corresponding Fusion prototype. The Setting is here to provide an easy way to change some basics without writing Fusion code. If you don't have any entries, no markup at all gets rendered. No more empty `<ul>` anymore!

## Properties for all menu prototypes

| Property      | Description                                                                                                                                                       |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `namespace`   | (string) You can easily change the namespace of the navigation. Useful if you have multiple navigations on your page. Defaults to the name of the prototype       |
| `wrapText`    | (boolean \|\| string) If `true`, the text inside the `a` gets wrapped with a `span`. If it is a string, this string will become the tag name. Defaults to `false` |
| `listTag`     | The tag of the full navigation gets wrapped. If it set to `false`, the navigation gets no surrounding tag. Defaults to `'ul'`                                     |
| `elementTag`  | The tag a navigation entry gets wrapped. If it set to `false`, the entry gets no surrounding tag. Defaults to `'li'`                                              |
| `renderClass` | (array) The array which defines the css classes for the menu. Read more about this [here](#therenderclass)                                                        |

### The renderClass

The `renderClass` entry in the setting for each menu type defines the CSS classes for this particular menu. It has three subkeys: `list`, `element` and `link`. Everyone of this key as further entries. If the keys are set to `false`, this type of class gets not rendered.

| Key          | Description                                                                                                                                                                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `entryLevel` | (boolean) Render a class with the entry level                                                                                                                                                                                                                |
| `menuLevel`  | (boolean) Render a class with the menu level                                                                                                                                                                                                                 |
| `subpages`   | (boolean) Render a class who indicate if the node has subpages (shown in the menu) or not                                                                                                                                                                    |
| `isFirst`    | (boolean) Render a class who indicate the first item in the list                                                                                                                                                                                             |
| `isLast`     | (boolean) Render a class who indicate the last item in the list                                                                                                                                                                                              |
| `type`       | (boolean) Render a class who indicate which type of link is rendered                                                                                                                                                                                         |
| `state`      | (array) Render classes who indicates which state (`normal`, `active`, `current` or `absent`) the node has. The values of the states can be `false`, a string or an array. If it is set to an array, the entry get multiple classes for this particular state |
| `dimension`  | (array) Used only in the dimension menu. You can set if the dimension entry gets also a class with the dimension name (`key`) and/or the name with the uriPathSegment (`value`). Very useful if you want to use flags or icons in your dimension menu        |

Look at [Settings.yaml](Configuration/Settings.yaml) for the default values for the different menu types

## `Carbon.Navigation:Mixin`

Basic Mixin for Menus. Based on [Neos.Neos:MenuItems](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-menuitems).

Defined in [Mixin.fusion](Resources/Private/Fusion/Menu/Mixin.fusion)

## `Carbon.Navigation:Menu`

Render a menu with items for nodes. Based on `Neos.Neos:MenuItems`. Besides the [default properties](#propertiesforallmenuprototypes) following properties are available:

| Property              | Description                                                                                                     |
| --------------------- | --------------------------------------------------------------------------------------------------------------- |
| `maximumLevels`       | (integer) Restrict the maximum depth of items in the menu (relative to `entryLevel`) . Defaults to `2`          |
| `filter`              | (string) Filter items by node type, defaults to `'Neos.Neos:Document,!Carbon.Navigation:NotInMenu'`             |
| `showHome`            | (boolean) If set to `true`, the homepage link gets rendererd in the menu. Defaults to `false`                   |
| `homeLabel`           | (string) Replace the label from `site`. If set to `false`, the label from the site itself get used.             |
| `entryLevel`          | (integer) Start the menu at the given depth. If no `startingPoint` is set, it is defaults to `1`, otherwise `0` |
| `startingPoint`       | (Node) The parent node of the first menu level                                                                  |
| `lastLevel`           | (integer) Restrict the menu depth by node depth (relative to site node)                                         |
| `renderHiddenInIndex` | (boolean) Whether nodes with `hiddenInIndex` should be rendered, defaults to `false`                            |
| `itemCollection`      | (array) Explicitly set the Node items for the menu (alternative to `startingPoints` and levels)                 |

Defined in [Menu.fusion](Resources/Private/Fusion/Menu/Menu.fusion)

## `Carbon.Navigation:References`

Provides a list of links, based on nodes which are set in the inspector. Based on `Carbon.Navigation:Mixin`. `itemCollection` is set to the closest instance of `Carbon.Navigation:References` who has the property `navigationreferences` set. `maximumLevels` defaults to `1` and `renderHiddenInIndex` defaults to `true`.

Defined in [References.fusion](Resources/Private/Fusion/Menu/References.fusion)

## `Carbon.Navigation:Breadcrumb`

Provides a breadcrumb navigation based on the current node. Based on `Carbon.Navigation:Mixin`. `listTag` defaults to `'ol'`.

| Property    | Description                                                                                         |
| ----------- | --------------------------------------------------------------------------------------------------- |
| `showHome`  | (boolean) If set to `true`, the homepage link gets rendererd in the menu. Defaults to `false`       |
| `homeLabel` | (string) Replace the label from `site`. If set to `false`, the label from the site itself get used. |

Defined in [Breadcrumb.fusion](Resources/Private/Fusion/Menu/Breadcrumb.fusion)

## `Carbon.Navigation:Dimensions`

Create links to other node variants (e.g., variants of the current node in other dimensions) by using this Fusion object. Extends [Neos.Neos:DimensionsMenu](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-dimensionsmenu). If no specific `dimension` is set, the `Neos.Neos:DimensionsMenu` prototype output the label from the node, and not the dimensions label. This prototype also fixes this wrong behavior.

| Property                    | Description                                                                                         |
| --------------------------- | --------------------------------------------------------------------------------------------------- |
| `renderCurrent`             | (boolean) If set to `false` the current dimension didn't get rendered. Defaults to `true`           |
| `dimension`                 | (optional, string) name of the dimension which this menu should be based on. Example: `'language'`. |
| `presets`                   | (optional, array): If set, the presets rendered will be taken from this list of preset identifiers  |
| `includeAllPresets`         | (boolean) If set to `true`, include all presets, not only allowed combinations. Defaults to `false` |
| `renderHiddenInIndex`       | (boolean) Whether nodes with hiddenInIndex should be rendered, defaults to `true`                   |
| `useUriSegmentAsLabel`      | (boolean) If set to true, the uri segment will get used as label, defaults to `false`               |
| `mulitipleDimensionDivider` | (string) String to divide multiple dimensions (if no specific `dimension` is set), defaults to `-`  |

Defined in [Dimensions.fusion](Resources/Private/Fusion/Menu/Dimensions.fusion)

## `Carbon.Navigation:Label`

A small helper to get the label for an menu entry. Per default, it reads the `item.label` property. If you want to output just the title you can edit the prototye e. g. like this;

```elm
prototype(Carbon.Navigation:Label) {
    renderer = ${q(props.item.node).property('title')}
}
```

Defined in [Label.fusion](Resources/Private/Fusion/Menu/Label.fusion)

## License

Licensed under MIT, see [LICENSE](LICENSE)
