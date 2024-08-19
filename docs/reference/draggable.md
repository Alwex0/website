---
sidebar_label: draggable
title: draggable
---

## Draggable Objects

```python
class Draggable(Control)
```

A control that can be dragged from to a `DragTarget`.

When a draggable control recognizes the start of a drag gesture, it displays a `content_feedback` control that tracks the user&#x27;s finger across the screen. If the user lifts their finger while on top of a `DragTarget`, that target is given the opportunity to complete drag-and-drop flow.

**Example**:

```
import flet
from flet import (
    Column,
    Container,
    Draggable,
    DragTarget,
    DragTargetAcceptEvent,
    Page,
    Row,
    border,
    colors,
)


def main(page: Page):
    page.title = "Drag and Drop example"

    def drag_will_accept(e):
        e.control.content.border = border.all(
            2, colors.BLACK45 if e.data == "true" else colors.RED
        )
        e.control.update()

    def drag_accept(e: DragTargetAcceptEvent):
        src = page.get_control(e.src_id)
        e.control.content.bgcolor = src.content.bgcolor
        e.control.content.border = None
        e.control.update()

    def drag_leave(e):
        e.control.content.border = None
        e.control.update()

    page.add(
        Row(
            [
                Column(
                    [
                        Draggable(
                            group="color",
                            content=Container(
                                width=50,
                                height=50,
                                bgcolor=colors.CYAN,
                                border_radius=5,
                            ),
                            content_feedback=Container(
                                width=20,
                                height=20,
                                bgcolor=colors.CYAN,
                                border_radius=3,
                            ),
                        ),
                        Draggable(
                            group="color",
                            content=Container(
                                width=50,
                                height=50,
                                bgcolor=colors.YELLOW,
                                border_radius=5,
                            ),
                        ),
                        Draggable(
                            group="color1",
                            content=Container(
                                width=50,
                                height=50,
                                bgcolor=colors.GREEN,
                                border_radius=5,
                            ),
                        ),
                    ]
                ),
                Container(width=100),
                DragTarget(
                    group="color",
                    content=Container(
                        width=50,
                        height=50,
                        bgcolor=colors.BLUE_GREY_100,
                        border_radius=5,
                    ),
                    on_will_accept=drag_will_accept,
                    on_accept=drag_accept,
                    on_leave=drag_leave,
                ),
            ]
        )
    )


flet.app(target=main)
```
  
  -----
  
  Online docs: https://flet.dev/docs/controls/draggable

