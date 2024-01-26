// DateCalendar.test.js
import React from 'react';
import { mount } from 'enzyme';
import DateCalendar from './DateCalendar';

describe('DateCalendar Component', () => {
  const currentDate = new Date(2022, 0, 15); // January 15, 2022

  it('renders without crashing', () => {
    const wrapper = mount(<DateCalendar currentDate={currentDate} onDateClick={() => {}} selectedDates={[]} />);
    expect(wrapper.exists()).toBe(true);
  });

  it('calls onDateClick when a date is clicked', () => {
    const onDateClickMock = jest.fn();
    const wrapper = mount(<DateCalendar currentDate={currentDate} onDateClick={onDateClickMock} selectedDates={[]} />);

    // Simulate a click on a date cell
    wrapper.find('td').at(5).simulate('click'); // Click on the 6th day (index 5)

    // Check if onDateClick is called with the correct date
    expect(onDateClickMock).toHaveBeenCalledWith(new Date(2022, 0, 6));
  });

  it('applies selected style to clicked date cell', () => {
    const selectedDates = [new Date(2022, 0, 6)];
    const wrapper = mount(<DateCalendar currentDate={currentDate} onDateClick={() => {}} selectedDates={selectedDates} />);

    // Check if the clicked date cell has the 'selected' class
    expect(wrapper.find('td.selected').exists()).toBe(true);
  });

  it('does not apply selected style to non-clicked date cells', () => {
    const selectedDates = [new Date(2022, 0, 6)];
    const wrapper = mount(<DateCalendar currentDate={currentDate} onDateClick={() => {}} selectedDates={selectedDates} />);

    // Check if other date cells do not have the 'selected' class
    expect(wrapper.find('td:not(.selected)').exists()).toBe(true);
  });
});
