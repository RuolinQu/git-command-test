import React from "react";
import "./Calendar.css"; // You can define your CSS styles for the calendar here

const daysOfWeek = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"];

const Calendar = ({ currentDate }) => {
  const renderDaysOfWeek = () => {
    return daysOfWeek.map((day) => (
      <div className="day-of-week" key={day}>
        {day}
      </div>
    ));
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

    for (let i = 0; i < blanksBeforeFirstDay; i++) {
      days.push(
        <div className="empty-day" key={`empty-${i}`}>
          {/* Render empty placeholders for days before the first day of the month */}
        </div>
      );
    }

    for (let day = 1; day <= daysInMonth; day++) {
      days.push(
        <div className="calendar-day" key={day}>
          {day}
        </div>
      );
    }

    return days;
  };

  console.log(currentDate);
  return (
    <div className="calendar-container">
      <div className="month-header">
        {currentDate.toLocaleString("default", {
          month: "long",
          year: "numeric",
        })}
      </div>
      <div className="days-of-week">{renderDaysOfWeek()}</div>
      <div className="calendar-days">{renderCalendarDays()}</div>
    </div>
  );
};

export default Calendar;


.calendar-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 300px; /* Adjust width as needed */
    font-family: Arial, sans-serif;
  }
  
  .month-header {
    font-size: 1.2em;
    margin-bottom: 10px;
  }
  
  .days-of-week {
    display: flex;
    justify-content: space-around;
    width: 100%;
    margin-bottom: 10px;
  }
  
  .day-of-week {
    width: calc(100% / 7); /* Equal width for each day of the week */
    text-align: center;
  }
  
  .calendar-days {
    display: flex;
    flex-wrap: wrap;
    width: 100%;
  }
  
  .calendar-day {
    width: calc(100% / 7); /* Equal width for each day cell */
    text-align: center;
    margin-bottom: 5px;
  }
  
  .empty-day {
    width: calc(100% / 7); /* Equal width for empty day cell */
  }
  
