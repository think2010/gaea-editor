# GaeaEditor

A scalable web page editor.

- **Adaptation**: Support all react components. Add a few lines of configuration, you can let your components in the edit menu display, and can be dragged into the view area, and edit its properties.
- **Scalable**: Support plug-ins to expand the editor for any function. Plug-ins can be inserted into any part of the editor, plug-ins can also provide slots for other plug-ins, plug-ins can create and share data flow editor, call the editor arbitrary function.

# Usage

## Installation

```bash
npm i gaea-editor --save
```

## A simple example

Write a custom component `custom-component.tsx`.

```typescript
import * as React from 'react'
export default class CustomComponent extends React.Component<any, any>{
    // You need at least two properties in defaultProps to fit into the editor
    static defaultProps = {
        // Edit the name of the menu display
        gaeaName: 'my-textarea', 
        // Ensure that the other components and the overall does not repeat
        // Do not worry, `gaea-web-components` All this field starts with `gaea-`
        gaeaUniqueKey: 'textarea' 
    }

    render() { return <textarea /> }
}
```

Next, display the editor:

```typescript
import * as React from 'react'
import GaeaEditor from 'gaea-editor'
import CustomComponent from './custom-component'

// Put the custom components in the array, they will be displayed in the right menu
const customComponentArray: Array<FitGaea.Component> = [CustomComponent]

export default class Home extends React.Component<any, any>{
    render() {
        // Menu components are divided into common and custom, if you like, you can remove the common components
        // However, if there is no gaeaUniqueKey called gaea-layout, or a new outer container is defined by `rootLayoutComponentUniqueKey`, view area rendering will block
        return (
            <GaeaEditor componentClasses={[CustomComponent]} />
        )
    }
}
```

## External configuration

If you do not want to put the configuration on defaultProps, or need to migrate many components, you can [achieve through external configuration.](<docs/custom-options.md>)

## Configure rules

In addition to the necessary `gaeaName` and `gaeaUniqueKey`, you can set the [gaeaEdit](<docs/gaea-edit.md>) custom edit settings, set the [gaeaEvent](<docs/gaea-event.md>) custom component event settings.

# Deploy

```bash
npm i gaea-render --save
```

Pass the string passed by the editor `onSave` callback to the `value` attribute of `gaea-render`.

Do not forget to give all the components of the editor to `gaea-render`.

```typescript
import * as React from 'react'
import GaeaRender from 'gaea-render'

// From the gaea-editor onSave callback
const saveInfo = `{...}`

export default class Production extends React.Component <any, any> {
    render() {
        return (
            <GaeaPreview value={saveInfo}/>
        )
    }
}
```

# Development

If you want to extend the plug-in, look at the [developer documentation](<docs/develop.md>).