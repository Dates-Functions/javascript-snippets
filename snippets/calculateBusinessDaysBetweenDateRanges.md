---
title: Number of Business Days between date ranges
tags: date
author: srivatsa-cfg
createdOn: 2023-01-25T12:48:49+03:00
lastUpdated: 2023-01-25T12:48:49+03:00
---

Calculates the number of business days between two date ranges using moment.


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

const calculateBizdays = (start, end) => {
    if ( start === "" || start === null || typeof start == 'undefined') return "";
    if ( end === "" || end === null || typeof end == 'undefined') return "";
    
    let startDateString = moment(start).format("MM-DD-YYYY"); // Convert start timestamp to date
    let endDateString = moment(end).format("MM-DD-YYYY"); // Convert end timestamp to date
    let diff = moment(endDateString).businessDiff(moment(startDateString)); // Calculate the difference including holidays
    return diff;
```
