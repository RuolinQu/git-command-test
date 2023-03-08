# git-command-test
# first


import React, { Component } from 'react';
import { AgGridReact } from 'ag-grid-react';

class CustomCellRenderer extends Component {
  refresh(params) {
    // update any state variables that affect the rendering of the cell
    // ...

    // tell the grid to re-render the cell
    return true;
  }

  render() {
    const { value } = this.props;
    return <span>{value}</span>;
  }
}

class MyGridComponent extends Component {
  constructor(props) {
    super(props);

    this.state = {
      rowData: [
        { make: 'Toyota', model: 'Celica', price: 35000 },
        { make: 'Ford', model: 'Mondeo', price: 32000 },
        { make: 'Porsche', model: 'Boxter', price: 72000 }
      ]
    };

    this.columnDefs = [
      { headerName: 'Make', field: 'make' },
      { headerName: 'Model', field: 'model' },
      {
        headerName: 'Price',
        field: 'price',
        cellRenderer: 'customCellRenderer'
      }
    ];

    this.frameworkComponents = {
      customCellRenderer: CustomCellRenderer
    };
  }

  render() {
    return (
      <div
        className="ag-theme-alpine"
        style={{
          height: '500px',
          width: '600px'
        }}
      >
        <AgGridReact
          columnDefs={this.columnDefs}
          rowData={this.state.rowData}
          frameworkComponents={this.frameworkComponents}
        ></AgGridReact>
      </div>
    );
  }
}
