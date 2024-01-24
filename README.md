// DateRangeController.js
import React, { useState } from 'react';
import DateCalendar from './DateCalendar';

const DateRangeController = () => {
  const [startDate, setStartDate] = useState(null);
  const [endDate, setEndDate] = useState(null);

  const handleDateClick = (clickedDate) => {
    if (!startDate) {
      // If no start date selected, set clickedDate as start date
      setStartDate(clickedDate);
      setEndDate(null);
    } else if (!endDate && clickedDate > startDate) {
      // If start date selected and no end date, and clickedDate is after start date, set as end date
      setEndDate(clickedDate);
    } else {
      // Reset selection if clicked on an invalid date
      setStartDate(null);
      setEndDate(null);
    }
  };

  return (
    <div>
      <h2>Date Range Controller</h2>
      <div>
        <strong>Selected Range: </strong>
        {startDate && endDate ? `${startDate.toLocaleDateString()} to ${endDate.toLocaleDateString()}` : 'None'}
      </div>
      <DateCalendar
        currentDate={new Date()}
        onDateClick={handleDateClick}
        selectedDates={[startDate, endDate]}
      />
    </div>
  );
};

export default DateRangeController;

// DatePickerController.js
import React, { useState } from 'react';
import DateCalendar from './DateCalendar';

const DatePickerController = () => {
  const [selectedDate, setSelectedDate] = useState(null);

  const handleDateClick = (clickedDate) => {
    setSelectedDate(clickedDate);
  };

  return (
    <div>
      <h2>Date Picker Controller</h2>
      <div>
        <strong>Selected Date: </strong>
        {selectedDate ? selectedDate.toLocaleDateString() : 'None'}
      </div>
      <DateCalendar
        currentDate={new Date()}
        onDateClick={handleDateClick}
        selectedDates={[selectedDate]}
      />
    </div>
  );
};

export default DatePickerController;
