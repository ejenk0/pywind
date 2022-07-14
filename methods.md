# Methods

This page describes the methods used in the pywind library.

## `pywind.tick`

`pywind.tick` is used to update the state of the pywind library. **It must be called once per frame before the pygame event queue is cleared**.

Running `pywind.tick` once per frame saves unessary calls to the pygame event queue and input system.

It currently updates the following:

Name | Description
--- | ---
`pywind.events` | Gets the latest pygame events without clearing the event queue. This is used for interactive pywind elements to detect events such as mouse clicks, keyboard inputs and screen resizing.
`pywind.mouse` | Gets the latest mouse position if the mouse has moved.
`pywind.keyboard` | Gets the latest keyboard state if it has changed.
`pywind.screen` | Gets the current pygame display surface if it has changed for [`pywind.Container`](classes.md#pywindcontainer) size calculations.
