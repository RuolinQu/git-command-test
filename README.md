import React, { useState } from "react";
import { DateTime } from "luxon";

const DatePicker = () => {
  const [selectedDate, setSelectedDate] = useState(DateTime.local());

  const handleDateChange = (date) => {
    setSelectedDate(date);
  };

  const handlePreviousMonth = () => {
    handleDateChange(selectedDate.minus({ months: 1 }));
  };

  const handleNextMonth = () => {
    handleDateChange(selectedDate.plus({ months: 1 }));
  };

  const daysInMonth = selectedDate.daysInMonth;
  const firstDayOfMonth = selectedDate.startOf("month");

  const daysArray = Array.from({ length: daysInMonth }, (_, i) =>
    firstDayOfMonth.plus({ days: i })
  );

  return (
    <div>
      <div>
        <button onClick={handlePreviousMonth}>Previous Month</button>
        <button onClick={handleNextMonth}>Next Month</button>
      </div>
      <div>
        <h3>{selectedDate.toFormat("MMMM yyyy")}</h3>
        <table>
          <thead>
            <tr>
              <th>Sun</th>
              <th>Mon</th>
              <th>Tue</th>
              <th>Wed</th>
              <th>Thu</th>
              <th>Fri</th>
              <th>Sat</th>
            </tr>
          </thead>
          <tbody>
            {daysArray.map((day) => (
              <tr key={day.toISODate()}>
                <td>{day.toFormat("d")}</td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
};

export default DatePicker;
