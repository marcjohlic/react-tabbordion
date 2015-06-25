# react-tabbordion

Provides base for handling state and styles for technically similar components such as tabs, accordions, option lists,
multiselect lists and so on.

Solves most CSS issues in elegant BEM'ish conventions. You have total control over style: only one globally required
rule!

```css
[data-state="tabbordion"] {
    clip: rect(0 0 0 0);
    height: 1px;
    position: absolute;
    position: fixed;
    width: 1px;
    z-index: -1;
}
```

This hides native HTML input elements so that they remain accessible. While we are at accessibility the component also
includes ARIA attributes. You can also add CSS-only (= JS disabled) support by using `:checked` in your stylesheets.

## Installation

```
npm install --save react-tabbordion
```

## An example

```js
var classNames = {
  content: 'tabs-content',
  panel: 'tabs-panel',
  title: 'tabs-title'
}

<Tabbordion className="tabs" classNames={classNames} initialIndex={0} name="tabs">
  <Panel title={<span>My title</span>}>
    <h2>Sample</h2>
    <p>Content</p>
  </Panel>
  <Panel title={<span>Another title</span>}>
    <h2>Another Sample</h2>
    <p>Some other kind of content</p>
  </Panel>
</Tabbordion>
```

**Output:**

```html
<ul role="tablist" class="tabs tabs--active-count-1 tabs--count-2">
  <li aria-expanded="true" aria-selected="true" class="tabs-panel tabs-panel--checked tabs-panel--content tabs-panel--first">
    <input aria-controls="panel-tabs-0" checked data-state="tabbordion" id="tabs-0" name="tabs" role="tab" value="0" type="radio" />
    <label class="tabs-title tabs-title--checked tabs-title--content tabs-title--first" id="label-tabs-0" for="tabs-0">
      <span>My title</span>
    </label>
    <div aria-labelledby="tabs-0" class="tabs-content tabs-content--checked tabs-content--first" id="panel-tabs-0" role="tabpanel">
      <h2>Sample</h2>
      <p>Content</p>
    </div>
  </li>
  <li aria-expanded="false" aria-selected="false" class="tabs-panel tabs-panel--unchecked tabs-panel--content tabs-panel--last">
    <input aria-controls="panel-tabs-1" data-state="tabbordion" id="tabs-1" name="tabs" role="tab" value="1" type="radio" />
    <label class="tabs-title tabs-title--unchecked tabs-title--content tabs-title--last" id="label-tabs-1" for="tabs-1">
      <span>Another title</span>
    </label>
    <div aria-labelledby="tabs-1" class="tabs-content tabs-content--unchecked tabs-content--last" id="panel-tabs-1" role="tabpanel">
      <h2>Another Sample</h2>
      <p>Some other kind of content</p>
    </div>
  </li>
</ul>
```

## Tabbordion
This is the main controller component. It handles state and passes properties to all children.

### Props

The following special props are accepted:
- `classModifiers`
- `classNames`
- `classSeparator`
- `initialIndex`
- `mode`
- `name`
- `onChange`
- `onAfterChange`
- `onBeforeChange`
- `contentTag`
- `panelTag`
- `tag`

#### `initialIndex`

Defaults to `null`. You most likely want to give it 0. Otherwise none of the panels is active until opened.

### Classes

Tabbordion uses minimal BEM style in it's classes. This means if you name panel element as `derp`, you will get
`className="derp derp--checked"` when the panel is active.

Output can be fully customized using `classModifiers`, `classNames` and `classSeparator`.

`classSeparator` defaults to `--` and it is added between the block element and modifier parts of the class.

`classNames` is an object with four customizable panel elements with following defaults:

1. `panel` = 'panel' > `.panel` (container element)
2. `state` = 'panel__state' > `.panel__state` (input element)
3. `title` = 'panel__title' > `.panel__title` (label element)
4. `content` = 'panel__content' > `.panel__content` (content container element)

`classModifiers` are the M in BEM and are added after the separator when a specific modifier state is met.

1. `checked` = 'checked' > `.panel .panel--checked`
2. `content` = 'content' > `.panel .panel--content`
3. `disabled` = 'disabled' > `.panel .panel--disabled`

Modifiers are applied to all elements defined in `classNames`.

#### `mode` (string)

1. `single` (default)

    A single panel is always open. Just like normal tabs component (or a normal radio list).

2. `toggle`

    A single panel may be open; active can be closed by toggling it. Just like your usual accordion component.

3. `multiple`

    Multiple panels may be open. Just like any checkbox list. Panels are grouped together, but each has it's own state.

#### `name` (string)

This string is passed to input elements name attribute as-is to allow for native browser grouping behavior.

This value is also used for generating input, label and content container id attributes.

#### `tag`, `panelTag` and `contentTag` (string)

Element to generate the semantic structure. Defaults to `ul`, `li` and `div` respectively.



*TODO: documentation for Panel and Animated components, demos for all mentioned five use cases*
