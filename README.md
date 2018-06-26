[![Latest Stable Version](https://poser.pugx.org/carbon/navigation/v/stable)](https://packagist.org/packages/carbon/navigation)
[![Total Downloads](https://poser.pugx.org/carbon/navigation/downloads)](https://packagist.org/packages/carbon/navigation)
[![License](https://poser.pugx.org/carbon/navigation/license)](LICENSE)
[![GitHub forks](https://img.shields.io/github/forks/CarbonPackages/Carbon.Navigation.svg?style=social&label=Fork)](https://github.com/CarbonPackages/Carbon.Navigation/fork)
[![GitHub stars](https://img.shields.io/github/stars/CarbonPackages/Carbon.Navigation.svg?style=social&label=Stars)](https://github.com/CarbonPackages/Carbon.Navigation/stargazers)
[![GitHub watchers](https://img.shields.io/github/watchers/CarbonPackages/Carbon.Navigation.svg?style=social&label=Watch)](https://github.com/CarbonPackages/Carbon.Navigation/subscription)

# Carbon.Navigation Package for Neos CMS

## NodeTypes

All Node Types are marked as abstract. So you have to include them as supertypes if you want to use them. You can read more about Node Type definition [here](https://neos.readthedocs.io/en/stable/CreatingASite/NodeTypes/NodeTypeDefinition.html).

### `Carbon.Navigation:NotInMenu`

Hide the property `_hiddenInIndex`. Defined in [NodeTypes.Mixin.yaml](Configuration/NodeTypes.Mixin.yaml)

### `Carbon.Navigation:HideSeo`

Turn off all type of SEO properties. Defined in [NodeTypes.Mixin.yaml](Configuration/NodeTypes.Mixin.yaml)

### `Carbon.Navigation:Redirect.ToParentPage`

(Only in the live context) Redirect the user to the parent page. Defined in [NodeTypes.Redirect.yaml](Configuration/NodeTypes.Redirect.yaml) and [ToParentPage.fusion](Resources/Private/Fusion/Redirect/ToParentPage.fusion)

### `Carbon.Navigation:Redirect.ToFirstChildPage`

(Only in the live context) Redirect the user to the first child page, if available. If not, the user gets redirected to the parent page. Defined in [NodeTypes.Redirect.yaml](Configuration/NodeTypes.Redirect.yaml) and [ToFirstChildPage.fusion](Resources/Private/Fusion/Redirect/ToFirstChildPage.fusion)

### `Carbon.Navigation:References`

Insert a property called `navigationreferences`. This is very useful if you want to create a navigation and want the editor to choose which documents should be included. However, you can also pass a custom collection to the Fusion prototype. Defined in [NodeTypes.References.yaml](Configuration/NodeTypes.References.yaml) and [References.fusion](Resources/Private/Fusion/References/References.fusion)

## Menu Fusion prototypes

### `Carbon.Navigation:Dimensions`

Extendend variant from [Neos.Neos:DimensionsMenu](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-dimensionsmenu). If you set `renderCurrent` to `false`, the current dimension didn't get rendered. You got also some useful css classes (Defined in `Carbon.Navigation:Dimensions.Class`) to create the needed styling. Defined in [Dimensions.fusion](Resources/Private/Fusion/Menu/Dimensions.fusion)

### `Carbon.Navigation:LogoTag`

Create a Tag with a link to the homepage. Defined in [LogoTag.fusion](Resources/Private/Fusion/Menu/LogoTag.fusion)

### `Carbon.Navigation:Menu`

Extend variant from [Neos.Neos:Menu](https://neos.readthedocs.io/en/stable/References/NeosFusionReference.html#neos-neos-menu). If you set `wrapAnchor` to `true`, the text inside the anchor gets wrapped with a `span` tag, if the value is set to an string, this string will be used as tag name. The main difference to the default menu is that if you have no item to render, no markup at all gets rendered. You can also inject custom code with the properties `beforeFirst`, `afterLast`, `beforeItem` and `afterItem`. If you want to use css class names in [BEM](http://getbem.com/) styles, you have to set `useBEM` to true. Defined in [Menu.fusion](Resources/Private/Fusion/Menu/Menu.fusion)

## License

Licensed under MIT, see [LICENSE](LICENSE)
