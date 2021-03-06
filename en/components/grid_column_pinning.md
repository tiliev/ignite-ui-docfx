---
title: Grid column pinning
_description: The Ignite UI for Angular Data Grid control features the fastest, touch-responsive data-rich grid with popular features, including hierarchical and list views.
_keywords: Ignite UI for Angular, UI controls, Angular widgets, web widgets, UI widgets, Angular, Native Angular Components Suite, Native Angular Controls, Native Angular Components Library, Angular Data Grid component, Angular Data Grid control, Angular Grid component, Angular Grid control, Angular High Performance Grid, column pinning, pinning, pin
---

### Grid Column Pinning

**Column Pinning** is available through the **igx-grid** API. Each column can be pinned as long as the pinned area does not become wider than the grid itself. Column pinning is controlled through the `pinned` input of the `igx-column`. Pinned columns are always rendered on the left side of the grid and stay fixed through horizontal scrolling of the unpinned columns in the grid body.

```html
<igx-grid #grid1 [data]="data | async" [width]="700px" [autoGenerate]="false" [paging]="true" [perPage]="6" (onColumnInit)="initColumns($event)"
    (onSelection)="selectCell($event)">
    <igx-column [field]="Name" [pinned]="true"></igx-column>
    <igx-column [field]="AthleteNumber"></igx-column>
    <igx-column [field]="TrackProgress"></igx-column>
</igx-grid>
```

You may also use the grid's `pinColumn` or `unpinColumn` methods of the `IgxGridComponent` to pin or unpin columns by their field name:

```typescript
this.grid.pinColumn("AthleteNumber");
this.grid.unpinColumn("Name");
```

Both methods return a boolean value indicating whether their respective operation is successful or not. Usually the reason they fail is that the column is already in the desired state. `pinColumn` also fails when the result would mean that the pinned area becomes larger than or the same size as the grid itself. Consider the following example:

```html
<igx-grid #grid1 [data]="data | async" [width]="300px" [autoGenerate]="false">
    <igx-column [field]="Name" [width]="200px" [pinned]="true"></igx-column>
    <igx-column [field]="AthleteNumber" [width]="200px"></igx-column>
</igx-grid>
```

```typescript
var succeed = this.grid.pinColumn("AthleteNumber"); // pinning fails and succeed will be false
```

If pinning the `AthleteNumber` column is allowed the pinned area would exceed the grid's width.

A column is pinned to the right of the rightmost pinned column. Changing the order of the pinned columns can be done by subscribing to the `onColumnPinning` event and changing the `insertAtIndex` property of the event arguments to the desired position index.

```html
<igx-grid #grid1 [data]="data | async" [autoGenerate]="true" (onColumnPinning)="columnPinning($event)"></igx-grid>
```

```typescript
public columnPinning(event) {
    if (event.column.field === "Name") {
        event.insertAtIndex = 0;
    }
}
```

<div class="divider--half"></div>

### Additional Resources
<div class="divider--half"></div>

* [Grid overview](grid.html)
* [Virtualization and Performance](grid_virtualization.html)
* [Paging](grid_paging.html)
* [Filtering](grid_filtering.html)
* [Sorting](grid_sorting.html)
* [Summaries](grid_summaries.html)
* [Column Resizing](grid_column_resizing.html)

<div class="divider--half"></div>
Our community is active and always welcoming to new ideas.

* [Ignite UI for Angular **Forums**](https://www.infragistics.com/community/forums/f/ignite-ui-for-angular)
* [Ignite UI for Angular **GitHub**](https://github.com/IgniteUI/igniteui-angular)
