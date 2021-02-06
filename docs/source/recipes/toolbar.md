# Toolbar enhancements

You can configure the actions and buttons of the toolbar from the `toolbar`
configuration object. The toolbar is split into two areas:

- the `top` part, where the regular actions sit, like the "Edit" button, the
  Save/Cancel pair or, in some cases, the "Back" navigation button for pages to
  return to the regular section of the site.
- the `bottom` part, where the personal actions are placed.

The toolbar can be configured per "activity", which is a prop passed to the
`<Toolbar>` component when it's created. Available activities are: view, add,
edit, contents, contact-form, search, history, sharing, manage-translations,
diff, control-panel.

## Customization

To add a new button to the toolbar, insert it in your configuration scripts:


import {ButtonA, ButtonB} from './components';

const applyConfig = (config) => {
  config.toolbar.activities.view.top.push(ButtonA)
  config.toolbar.activities.view.bottom.push(ButtonB)
  return config;
};

export default applyConfig;

To insert new actions to the More component menu, use the `defaultMoreActions`
key:

```jsx
import {MyAction}  from './components';

export default function (config) {
  config.toolbar.defaultMoreActions.push(MyAction);

  return config;
}
```

It's also possible to configure the "default view actions", which are, by
default, defined as:

```
const defaultViewActions = [
  EditButton,
  ContentsButton,
  AddButton,
  moreMenu(defaultMoreActions),
];
```

This is exposed as `config.toolbar.defaultViewActions`.

### Dropdown menus

Because it's not straight-forward to reuse the More component to create new
dropdown menus, use the `DropdownWithButton` component for that:

```jsx
import { DropdownWithButton } from '@plone/volto/components/manage/Toolbar/Dropdown';

const applyConfig = (config) => {
  config.toolbar.activities.someActivity.top.push((props) => (
    <DropdownWithButton
      {...props}
      name="add-something"
      title="Add something"
      icon={<Icon name={addSVG} size="30px" />}
      headerActions={
        <button aria-label={'Add'} onClick={() => {}} tabIndex={0}>
          <Icon name={addSVG} size="30px" />
        </button>
      }
    >
      <div>Hello!</div>
    </DropdownWithButton>
  ));
  return config;
}

export default applyConfig;