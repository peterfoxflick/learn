---
layout: post
title: GAS Exceeds Timeout
subtitle: A simple approach for when your google app scripts times outs.
tags: [google-app-scripts]
---

How to work around a Google App Script timeout.


First and foremost you should look at your script and try to make it more efficient. Not only will this avoid timeouts it can make your script run better. The simplest approach is to minimize calls to different Apps (SpreadsheetApp, DocumentApp, DriveApp). These two tips help me the most:
- Gather data from a sheet in bulk, not one cell at a time
- Write to a spreadsheet with [setValues vs setValue](https://developers.google.com/apps-script/reference/spreadsheet/range#setValues(Object))

But when that doesn't work then use this little trick of code. It will complete a loop, but times out before the script will. That way the script finishes successfully and if you set the script to run every 5 minutes then it will continue to run.


```javascript
var YOUR_MAX = //Max iterations for the loop

function keepGoing() {

  var start = new Date();
  var diff = 0;

  var start = Number(PropertiesService.getScriptProperties().getProperty("START"));
  Logger.log(start);

  for(var i = start; i < YOUR_MAX && diff < 280; i++){

    //MAKE CHANGES HERE **************************************************************************


    //END CHANGE AREA ****************************************************************************
    //Change time and counter for next run (incase it times out before finishing)
    PropertiesService.getScriptProperties().setProperty("START", i);

    var now = new Date();
    var difdate = (now.getTime() - startd.getTime()) * 0.001;
    diff = difdate;
    Logger.log("DIFF: " + diff);

  }

}

```
