<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [View][1]
    -   [sort][2]
    -   [columns][3]
    -   [computed-columns][4]
    -   [aggregates][5]
    -   [filters][6]
    -   [view][7]
    -   [view][8]
    -   [column-pivots][9]
    -   [row-pivots][10]
    -   [message][11]
    -   [worker][12]
    -   [load][13]
    -   [update][14]
    -   [notifyResize][15]
    -   [clone][16]
    -   [delete][17]
    -   [save][18]
    -   [restore][19]
    -   [reset][20]
    -   [copy][21]
    -   [download][22]
-   [View#perspective-view-update][23]
-   [View#perspective-config-update][24]

## View

**Extends ViewPrivate**

HTMLElement class for `<perspective-viewer` custom element.

### sort

Sets this `perspective.table.view`'s `sort` property, an array of column
names.

**Examples**

via Javascript DOM


```javascript
let elem = document.getElementById('my_viewer');
elem.setAttribute('sort', JSON.stringify([["x","desc"]));
```

via HTML


```javascript
<perspective-viewer sort='[["x","desc"]]'></perspective-viewer>
```

### columns

The set of visible columns.

**Parameters**

-   `columns` **[array][25]** An array of strings, the names of visible columns.

**Examples**

via Javascript DOM


```javascript
let elem = document.getElementById('my_viewer');
elem.setAttribute('columns', JSON.stringify(["x", "y'"]));
```

via HTML


```javascript
<perspective-viewer columns='["x", "y"]'></perspective-viewer>
```

### computed-columns

The set of visible columns.

**Parameters**

-   `computed-columns` **[array][25]** An array of computed column objects

**Examples**

via Javascript DOM


```javascript
let elem = document.getElementById('my_viewer');
elem.setAttribute('computed-columns', JSON.stringify([{name: "x+y", func: "add", inputs: ["x", "y"]}]));
```

via HTML


```javascript
<perspective-viewer computed-columns="[{name:'x+y',func:'add',inputs:['x','y']}]""></perspective-viewer>
```

### aggregates

The set of column aggregate configurations.

**Parameters**

-   `aggregates` **[object][26]** A dictionary whose keys are column names, and
    values are valid aggregations.  The `aggergates` attribute works as an
    override;  in lieu of a key for a column supplied by the developers, a
    default will be selected and reflected to the attribute based on the
    column's type.  See [perspective/src/js/defaults.js][27]

**Examples**

via Javascript DOM


```javascript
let elem = document.getElementById('my_viewer');
elem.setAttribute('aggregates', JSON.stringify({x: "distinct count"}));
```

via HTML


```javascript
<perspective-viewer aggregates='{"x": "distinct count"}'></perspective-viewer>
```

### filters

The set of column filter configurations.

**Examples**

via Javascript DOM


```javascript
let filters = [
    ["x", "<", 3],
    ["y", "contains", "abc"]
];
let elem = document.getElementById('my_viewer');
elem.setAttribute('filters', JSON.stringify(filters));
```

via HTML


```javascript
<perspective-viewer filters='[["x", "<", 3], ["y", "contains", "abc"]]'></perspective-viewer>
```

### view

Sets the currently selected plugin, via its `name` field.

**Parameters**

-   `v`  

### view

This element's `perspective.table.view` instance.  The instance itself
will change after every `View#perspective-config-update` event.

### column-pivots

Sets this `perspective.table.view`'s `column_pivots` property.

### row-pivots

Sets this `perspective.table.view`'s `row_pivots` property.

### message

When set, hide the data visualization and display the message.  Setting
`message` does not clear the internal `perspective.table`, but it does
render it hidden until the message is removed.

**Parameters**

-   `msg` **[string][28]** The message. This can be HTML - it is not sanitized.

**Examples**

```javascript
let elem = document.getElementById('my_viewer');
elem.setAttribute('message', '<h1>Loading</h1>');
```

### worker

This element's `perspective` worker instance.  This property is not
reflected as an HTML attribute, and is readonly;  it can be effectively
set however by calling the `load() method with a`perspective.table\`
instance from the preferred worker.

**Examples**

```javascript
let elem = document.getElementById('my_viewer');
let table = elem.worker.table([{x:1, y:2}]);
elem.load(table);
```

### load

Load data.  If `load` or `update` have already been called on this
element, its internal `perspective.table` will also be deleted.

**Parameters**

-   `data` **any** The data to load.  Works with the same input types
    supported by `perspective.table`.
-   `options`  

**Examples**

Load JSON


```javascript
const my_viewer = document.getElementById('#my_viewer');
my_viewer.load([
    {x: 1, y: 'a'},
    {x: 2, y: 'b'}
]);
```

Load CSV


```javascript
const my_viewer = document.getElementById('#my_viewer');
my_viewer.load("x,y\n1,a\n2,b");
```

Load perspective.table


```javascript
const my_viewer = document.getElementById('#my_viewer');
const tbl = perspective.table("x,y\n1,a\n2,b");
my_viewer.load(tbl);
```

Returns **[Promise][29]&lt;void>** A promise which resolves once the data is
loaded and a `perspective.view` has been created.

### update

Updates this element's `perspective.table` with new data.

**Parameters**

-   `data` **any** The data to load.  Works with the same input types
    supported by `perspective.table.update`.

**Examples**

```javascript
const my_viewer = document.getElementById('#my_viewer');
my_viewer.update([
    {x: 1, y: 'a'},
    {x: 2, y: 'b'}
]);
```

### notifyResize

Determine whether to reflow the viewer and redraw.

### clone

Duplicate an existing `<perspective-element>`, including data and view
settings.  The underlying `perspective.table` will be shared between both
elements

**Parameters**

-   `widget` **any** A `<perspective-viewer>` instance to clone.

### delete

Deletes this element's data and clears it's internal state (but not its
user state).  This (or the underlying `perspective.table`'s equivalent
method) must be called in order for its memory to be reclaimed.

Returns **[Promise][29]&lt;[boolean][30]>** Whether or not this call resulted in the
underlying `perspective.table` actually being deleted.

### save

Serialize this element's attribute/interaction state.

Returns **[object][26]** a serialized element.

### restore

Restore this element to a state as generated by a reciprocal call to
`save`.

**Parameters**

-   `x` **[object][26]** returned by `save`.

Returns **[Promise][29]&lt;void>** A promise which resolves when the changes have
been applied.

### reset

Reset's this element's view state and attributes to default.  Does not
delete this element's `perspective.table` or otherwise modify the data
state.

### copy

Copies this element's view data (as a CSV) to the clipboard.  This method
must be called from an event handler, subject to the browser's
restrictions on clipboard access.  See
[https://www.w3.org/TR/clipboard-apis/#allow-read-clipboard][31].

**Parameters**

-   `flat`   (optional, default `false`)

### download

Download this element's data as a CSV file.

**Parameters**

-   `flat` **[boolean][30]** Whether to use the element's current view
    config, or to use a default "flat" view. (optional, default `false`)

## View#perspective-view-update

`perspective-view-update` is fired whenever underlying `view`'s data has
updated, including every invocation of `load` and `update`.

## View#perspective-config-update

`perspective-config-update` is fired whenever an configuration attribute has
been modified, by the user or otherwise.

[1]: #view

[2]: #sort

[3]: #columns

[4]: #computed-columns

[5]: #aggregates

[6]: #filters

[7]: #view-1

[8]: #view-2

[9]: #column-pivots

[10]: #row-pivots

[11]: #message

[12]: #worker

[13]: #load

[14]: #update

[15]: #notifyresize

[16]: #clone

[17]: #delete

[18]: #save

[19]: #restore

[20]: #reset

[21]: #copy

[22]: #download

[23]: #viewperspective-view-update

[24]: #viewperspective-config-update

[25]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[27]: perspective/src/js/defaults.js

[28]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[29]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise

[30]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[31]: https://www.w3.org/TR/clipboard-apis/#allow-read-clipboard
