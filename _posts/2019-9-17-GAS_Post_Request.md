---
layout: post
title: GAS Post Request
subtitle: How to make a post request with Google App Scripts
tags: [google-app-scripts]
---

All we have to do to make a post requeset in GAS is use the [UrlFetchApp](https://developers.google.com/apps-script/reference/url-fetch/url-fetch-app#fetch(String,Object). The trick is to set the `options` key of `method` to `'POST'`.

This code below if from a personal project of mine where I create a Trello card every week. Instead of dealing with a plugin all I have to do is set a trigger to run this script every week.

```javascript
var KEY = "xxxx"; // API Key for trello
var TOKEN = "xxxxxx"; // API Token for Trello
var LIST_ID = "xxx"; // List ID for Trello
var LABEL_ID = "xxx"; // Optional for trello


//Curate the creation of a card.
function createCard(){
  var label = LABEL_ID;
  var list = LIST_ID;
  var des = "Write a blog post"; //Description of the trello card

  //Parameters that the API application accepts. In this case Trello.
   var params = {
     name: "Tech Post",
     desc: "Write a post about programing",
   //due: ,
     idList: list,
     idLabels: label,
     key: KEY,
     token: TOKEN
   }

   //Options for the URL Fetch APP. We want the method to be set to POST,
   // and to pass in our parameters into the payload.
   var options = {
     method : 'POST',
     contentType: 'application/json',
     payload : JSON.stringify(params)
   }

   //The base url to use
  var url = 'https://api.trello.com/1/cards';
  // Response saves the reply from the server. Use Logger.log(response) to take a look at what happened.
  var response = UrlFetchApp.fetch(url, options);
}

```
