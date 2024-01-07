import React from "react";
import "./TableCalendar.css"; // You can define your CSS styles for the calendar here

const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

const Calendar = ({ currentDate }) => {
  const renderDaysOfWeek = () => {
    return daysOfWeek.map((day) => <th key={day}>{day}</th>);
  };

  const renderCalendarDays = () => {
    const firstDayOfMonth = new Date(
      currentDate.getFullYear(),
      currentDate.getMonth(),
      1
    );
    const lastDayOfMonth = new Date(
      currentDate.getFullYear(),
      currentDate.getMonth() + 1,
      0
    );
    const daysInMonth = lastDayOfMonth.getDate();
    const blanksBeforeFirstDay = firstDayOfMonth.getDay(); // Get the index of the first day (0-6)

    let days = [];
    let dayCounter = 1;

    for (let i = 0; i < 6; i++) {
      let weekDays = [];

      for (let j = 0; j < 7; j++) {
        if (i === 0 && j < blanksBeforeFirstDay) {
          // Render empty placeholders for days before the first day of the month
          weekDays.push(<td key={`empty-${j}`}></td>);
        } else if (dayCounter <= daysInMonth) {
          weekDays.push(<td key={dayCounter}>{dayCounter}</td>);
          dayCounter++;
        }
      }

      days.push(<tr key={i}>{weekDays}</tr>);
      if (dayCounter > daysInMonth) break;
    }

    return days;
  };

  return (
    <div className="calendar-container">
      <table className="calendar-table">
        <thead>
          <tr>{renderDaysOfWeek()}</tr>
        </thead>
        <tbody>{renderCalendarDays()}</tbody>
      </table>
    </div>
  );
};

export default Calendar;


.calendar-container {
    width: 300px; /* Adjust width as needed */
    font-family: Arial, sans-serif;
  }
  
  .calendar-table {
    width: 100%;
    border-collapse: collapse;
  }
  
  .calendar-table th,
  .calendar-table td {
    padding: 8px;
    text-align: center;
    border: 1px solid #ccc;
  }
  
  .calendar-table th {
    background-color: #f2f2f2;
  }
  
  .calendar-table td {
    cursor: pointer;
  }
  
  /* Add specific styles for days of the week (Mon to Sun) */
  .calendar-table th:nth-child(1),
  .calendar-table td:nth-child(1) {
    /* Style for Monday */
  }
  
  .calendar-table th:nth-child(2),
  .calendar-table td:nth-child(2) {
    /* Style for Tuesday */
  }
  
  /* Continue styling for each day of the week (Wednesday to Sunday) */
  /* .calendar-table th:nth-child(n),
     .calendar-table td:nth-child(n) {
       Style for respective days
     }
  */
