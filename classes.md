# Classes

This page describes the functionality of classes used in the pywind library.

## Element

The base class of all elements. The end user should not use this class directly.

The Element class inherits from the `pygame.sprite.Sprite` class. It computes an image and a rect based on its style component and its prescribed position by its parent. It contains a group of child elements which it prescribes positions based on its style attributes and renders to its image surface.

## Style

The `Style` class contains layout and [styling options](styling.md) for an element. It sizes, colours, fonts etc.

It is given a style-string that is computed into various styling attributes.
