// src/MonthCalendar.js
import React from 'react';
import './MonthCalendar.css'; // Optional: for styling

const MonthCalendar = () => {
  const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

  return (
    <table className="month-calendar">
      <tbody>
        {[0, 1, 2, 3].map((rowIndex) => (
          <tr key={rowIndex}>
            {months.slice(rowIndex * 3, rowIndex * 3 + 3).map((month, monthIndex) => (
              <td key={monthIndex} className="month-cell">
                {month}
              </td>
            ))}
          </tr>
        ))}
      </tbody>
    </table>
  );
};

export default MonthCalendar;
