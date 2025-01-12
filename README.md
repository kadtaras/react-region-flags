# react-region-flags

A React component to display country flags using Flag icons in Material React Table.

Features
Easy-to-use React component.
Supports custom flag sizes.
Uses standard classes from the [flag-icons library](https://github.com/lipis/flag-icons).

Installation:

Install the required dependency using npm or yarn:

```bash
npm install flag-icons material-react-table
# or
yarn add flag-icons material-react-table
```

Don't forget to import the CSS file for flag-icons in your project:
```import "flag-icons/css/flag-icons.min.css";```

Usage with Material React Table
The Flags component can be seamlessly integrated with Material React Table to display country flags alongside other data. Below is an example:

```tsx
import React, { useMemo } from "react";
import { MaterialReactTable, MRT_ColumnDef } from "material-react-table";
import { Flags } from "react-region-flags";

const locations = [
    { localCode: "ABC123", name: "Kyiv", countryName: "Ukraine", address: "Street 1", time: "2025-01-01T12:00:00Z" },
    { localCode: "XYZ789", name: "New York", countryName: "United States of America", address: "Street 2", time: "2025-01-02T15:00:00Z" },
];

const CheckNewLocationsTable = () => {
    const columns = useMemo<MRT_ColumnDef<any>[]>(
        () => [
            {
                accessorKey: 'localCode',
                header: 'Local Code',
            },
            {
                accessorKey: 'countryName',
                header: 'Name',
                Cell: ({ cell }) => {
                    return (
                        <div>
                            <Flags regionName={cell.getValue<string>()} flagSize={10} />
                            {cell.getValue<string>()}
                        </div>
                    );
                },
            },
            {
                accessorKey: 'address',
                header: 'Address',
            },
            {
                accessorKey: 'time',
                header: 'Time',
                Cell: ({ cell }) => {
                    const date = new Date(cell.getValue<string>());
                    return date.toLocaleString();
                },
            },
        ],
        [],
    );

    return (
        <MaterialReactTable
            columns={columns}
            data={locations}
            enableStickyHeader
        />
    );
};

export default CheckNewLocationsTable;
```
## Props

| Prop        | Type                | Description                                                        | Default Value |
|-------------|---------------------|--------------------------------------------------------------------|---------------|
| regionName  | `string`            | The name of the country/region. Only predefined names in `flagMap` are supported. | **Required**  |
| flagSize    | `number` (optional) | The size of the flag in pixels (applied via `fontSize`).           | `12`          |

Key Points:
Dynamic Flags:

The Flags component dynamically renders flags based on the countryName.
Styling:

Flags are styled with a flex container to align them with the corresponding text.
Reusable Helper Functions:

timestampRenderer is used for formatting timestamps, showcasing extensibility.
This example demonstrates how to enhance your table UI with visual indicators like flags. Feel free to adapt it to your specific needs.

