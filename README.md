import React, { useState, useEffect, forwardRef, useImperativeHandle } from 'react';
import { AgGridReact } from 'ag-grid-react';

const CustomCellRenderer = forwardRef((props, ref) => {
  const [value, setValue] = useState(props.value);

  useEffect(() => {
    setValue(props.value);
  }, [props.value]);

  useImperativeHandle(ref, () => ({
    refresh: (params) => {
      setValue(params.value);
      return true;
    }
  }));

  return <span>{value}</span>;
});

const MyGridComponent = () => {
  const [rowData, setRowData] = useState([
    { make: 'Toyota', model: 'Celica', price: 35000 },
    { make: 'Ford', model: 'Mondeo', price: 32000 },
    { make: 'Porsche', model: 'Boxter', price: 72000 }
  ]);

  const columnDefs = [
    { headerName: 'Make', field: 'make' },
    { headerName: 'Model', field: 'model' },
    {
      headerName: 'Price',
      field: 'price',
      cellRenderer: 'customCellRenderer'
    }
  ];

  const frameworkComponents = {
    customCellRenderer: CustomCellRenderer
  };

  const onButtonClick = () => {
    rowData[0].price = 40000;
    setRowData([...rowData]);
  };

  return (
    <div
      className="ag-theme-alpine"
      style={{
        height: '500px',
        width: '600px'
      }}
    >
      <button onClick={onButtonClick}>Update Data</button>
      <AgGridReact
        columnDefs={columnDefs}
        rowData={rowData}
        frameworkComponents={frameworkComponents}
      ></AgGridReact>
    </div>
  );
};
