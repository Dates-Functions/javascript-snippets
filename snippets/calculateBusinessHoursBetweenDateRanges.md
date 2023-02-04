---
title: Number of Business Hours between date ranges
tags: date
author: srivatsa-cfg
createdOn: 2023-02-01T12:48:49+03:00
lastUpdated: 2023-02-01T12:48:49+03:00
---

Calculates the number of business hours between two date ranges using moment.


```js
import moment, { duration } from 'moment';
import momentBusinessDays from 'moment-business-time';

let holidaysList= ['11-23-2023','11-24-2023','12-25-2023']

moment.updateLocale('us', {
    holidays: holidaysList,
    holidayFormat: 'MM-DD-YYYY',
    workinghours: {
        0: null,                       // Sun : CLOSED
        1: [ '00:00:00', '23:59:00' ], // Mon : 8am - 4pm  (local timezone)
        2: [ '00:00:00', '23:59:00' ], // Tue : 8am - 2pm  (local timezone)
        3: [ '00:00:00', '23:59:00' ], // Wed : 8am - 4pm  (local timezone)
        4: [ '00:00:00', '23:59:00' ], // Thu : 8am - 2pm  (local timezone)
        5: [ '00:00:00', '23:59:00' ], // Fri : 8am - 12pm (local timezone)
        6: null                        // Sat : CLOSED
    },
});

export const calculateBizHours = (start, end) => {
    if ( start === "" || start === null || typeof start == 'undefined') return "";
    if ( end === "" || end === null || typeof end == 'undefined') return "";
    let startTime = moment(start).format();
    let endTime = moment(end).format();
    let diff = moment(startTime).workingDiff(moment(endTime), 'hours'); // Calculate the difference including holidays &
    return diff;
};

```
