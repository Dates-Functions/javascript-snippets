---
title: Number of Business Days between current date and given date
tags: date
author: srivatsa-cfg
createdOn: 2023-01-25T12:48:49+03:00
lastUpdated: 2023-01-25T12:48:49+03:00
---

Calculates the number of business days between current date and given date using moment.


```js
import moment, { duration } from 'moment';
import momentBusinessDays from 'moment-business-days';

/* Configure all the holiday days in set the valies in holidaysList.
   These are the few days for the year 2023, you can pass holidays across multiple years as well
*/
let holidaysList= ['01-02-2023','01-26-2023','07-04-2023', '11-23-2023','12-25-2023'] 


/* Working weekdays are set between Monday[1] to Friday[5].
   If you want to include Saturday as well, then workingWeekdays: [1, 2, 3, 4, 5, 6] will looks something like this.
*/
moment.updateLocale('us', {
    holidays: holidaysList,
    holidayFormat: 'MM-DD-YYYY',
    workingWeekdays: [1, 2, 3, 4, 5]
});

const calculateBizdays = (value) => {
    if ( value === "" || value === null || typeof value == 'undefined') return "";
    
    let currentDate = moment().toISOString(); // Current date
    let currentDateString = moment(currentDate).format("MM-DD-YYYY"); // Convert timestamp to date
    let dateString = moment(value).format("MM-DD-YYYY");
    let diff = moment(currentDateString).businessDiff(moment(dateString)); // Calculate the difference including holidays &
    return diff;
```
