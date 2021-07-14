---
title: DraggableCore
description: 'Revue Draggable'
category: Guide
position: 3
---

For users that require absolute control, a `<DraggableCore>` element is available. 
This is useful as an abstraction over touch and mouse events, but with full control.
`<DraggableCore>` has no internal state.

`<DraggableCore>` is a useful building block for other libraries that simply want to abstract browser-specific quirks and receive callbacks when a user attempts to move an element. 
It does not set styles or transforms on itself and thus must have callbacks attached to be useful.

## API

### Types
```ts
type DraggableEventHandler = (e: MouseEvent, data: DraggableData) => void | false;

type DraggableData = {
    node: HTMLElement;
    x: number;
    y: number;
    deltaX: number;
    deltaY: number;
    lastX: number;
    lastY: number;
};

interface DraggableCoreProps {
    allowAnyClick: boolean;
    cancel: string;
    disabled: boolean;
    enableUserSelectHack: boolean;
    offsetParent: HTMLElement;
    grid: [number, number];
    handle: string;
    onStart: DraggableEventHandler;
    onDrag: DraggableEventHandler;
    onStop: DraggableEventHandler;
    onMouseDown: (e: MouseEvent) => void;
    scale: number;
}
```

### Props
```ts
export default {
    scale: {
        type: Number as PropType<DraggableCoreProps['scale']>,
        default: 1
    },
    allowAnyClick: {
        type: Boolean as PropType<DraggableCoreProps['allowAnyClick']>,
        default: true
    },
    disabled: {
        type: Boolean as PropType<DraggableCoreProps['disabled']>,
        default: false
    },
    enableUserSelectHack: {
        type: Boolean as PropType<DraggableCoreProps['enableUserSelectHack']>,
        default: true
    },
    onStart: {
        type: Function as PropType<DraggableCoreProps['onStart']>,
        default: () => {}
    },
    onDrag: {
        type: Function as PropType<DraggableCoreProps['onDrag']>,
        default: () => {}
    },
    onStop: {
        type: Function as PropType<DraggableCoreProps['onStop']>,
        default: () => {}
    },
    onMouseDown: {
        type: Function as PropType<DraggableCoreProps['onMouseDown']>,
        default: () => {}
    },
    cancel: {
        type: String as PropType<DraggableCoreProps['cancel']>,
        default: undefined
    },
    offsetParent: {
        type: Object as PropType<DraggableCoreProps['offsetParent']>,
        default: undefined
    },
    grid: {
        type: Array as unknown as PropType<DraggableCoreProps['grid']>,
        default: undefined
    },
    handle: {
        type: String as PropType<DraggableCoreProps['handle']>,
        default: undefined
    }
}
```
<alert>

Note that there is no start position.
`<DraggableCore>` simply calls drag handlers with the below parameters,
indicating its position (as inferred from the underlying MouseEvent) and deltas.
It is up to the parent to set actual positions on `<DraggableCore>`.

</alert>

Drag callbacks (onStart, onDrag, onStop) are called with the [same arguments as `<Draggable>`](/draggable).