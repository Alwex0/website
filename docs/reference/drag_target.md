---
sidebar_label: drag_target
title: drag_target
---

## DragTarget Objects

```python
class DragTarget(Control)
```

A control that completes drag operation when a `Draggable` widget is dropped.

When a draggable is dragged on top of a drag target, the drag target is asked whether it will accept the data the draggable is carrying. The drag target will accept incoming drag if it belongs to the same group as draggable. If the user does drop the draggable on top of the drag target (and the drag target has indicated that it will accept the draggable&#x27;s data), then the drag target is asked to accept the draggable&#x27;s data.

**Example**:

```
import flet as ft

def main(page: ft.Page):
    page.title = "Drag and Drop example"

    def drag_will_accept(e):
        e.control.content.border = ft.border.all(
            2, ft.colors.BLACK45 if e.data == "true" else ft.colors.RED
        )
        e.control.update()

    def drag_accept(e: ft.DragTargetEvent):
        src = page.get_control(e.src_id)
        e.control.content.bgcolor = src.content.bgcolor
        e.control.content.border = None
        e.control.update()

    def drag_leave(e):
        e.control.content.border = None
        e.control.update()

    page.add(
        ft.Row(
            [
                ft.Column(
                    [
                        ft.Draggable(
                            group="color",
                            content=ft.Container(
                                width=50,
                                height=50,
                                bgcolor=ft.colors.CYAN,
                                border_radius=5,
                            ),
                            content_feedback=ft.Container(
                                width=20,
                                height=20,
                                bgcolor=ft.colors.CYAN,
                                border_radius=3,
                            ),
                        ),
                        ft.Draggable(
                            group="color",
                            content=ft.Container(
                                width=50,
                                height=50,
                                bgcolor=ft.colors.YELLOW,
                                border_radius=5,
                            ),
                        ),
                        ft.Draggable(
                            group="color1",
                            content=ft.Container(
                                width=50,
                                height=50,
                                bgcolor=ft.colors.GREEN,
                                border_radius=5,
                            ),
                        ),
                    ]
                ),
                ft.Container(width=100),
                ft.DragTarget(
                    group="color",
                    content=ft.Container(
                        width=50,
                        height=50,
                        bgcolor=ft.colors.BLUE_GREY_100,
                        border_radius=5,
                    ),
                    on_will_accept=drag_will_accept,
                    on_accept=drag_accept,
                    on_leave=drag_leave,
                ),
            ]
        )
    )

ft.app(target=main)
```
  
  -----
  
  Online docs: https://flet.dev/docs/controls/dragtarget

