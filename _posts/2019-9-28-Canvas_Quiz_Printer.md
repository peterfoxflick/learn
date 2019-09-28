---
layout: post
title: Making Canvas Quiz Printer
subtitle: How I made the Canvas Quiz Printer chrome extension
tags: [canvas]
---

So it all began a long time ago. Well not really, it was last semester. I worked at a technology support center for teachers and I had some time to work on a project of my choosing. That being said I wanted to make something people would use. After researching it appeared that printing quizzes on canvas was one of the most highly requested features, and it had been turned down. This makes senses as Canvas is moving towards Quizes.next, so improving the existing quizzing feature is redundant, but for a quick and fun project to entertain a growing CS Student its a perfect fit.  

## The Plan

The game plan was simple.
1. Learn how to make chrome extensions
2. Get the quiz id, course id, and school id from the url
3. Use the above id's to get the questions from a quiz
4. Output each question as HTML

And thats how it worked folks. First I got the program to trigger when the extension icon was clicked. The current URL was analyzed for the id's and passed as parameters to a local HTML document that would run all the API requests.

The largest part of this project was going through and generating HTML for each question. I started with the easy ones, like multiple choice, or essay questions. Some questions like drop-downs, or matching were trickier to plan.

After a working HTML document was created I went back and added some Bootstrap styling and imported in the quiz title. This greatly increased the look and feel of the quiz.

## Almost there

After publishing the extension I reached out to my coworkers to test it out. One pointed out that the project failed to print more than 10 questions. It wasn't until now that I realized I had 11 questions in my test quiz. I always just assumed that the file upload question was simply not important enough to debug. A larger problem revealed. For some unknown reason, chrome was blocking the api response headers, which with canvas, included the link to the next url with more questions. This meant, from the original API call I had no idea how many pages of questions there would be.

Luckily, from getting the quiz title, and description, I already had easy access to that answers. Knowing the total number of questions meant I could go back and know how many requests were necessary to get all the questions from the quiz.

## Going further

I would love to go back and add some interactions to the printable quiz. Allow the user to change the font, add more lines to essay questions, things like that. For now I might tuck this project into the back drawer, but if you would like to take a stab at it just [fork it from GitHub](https://github.com/peterfoxflick/CanvasQuizPrinter).

PS. You can install the chrome extension from the [Chrome Web Store](https://chrome.google.com/webstore/detail/canvas-quiz-printer/aolnbenhahgdmbdgjdkphepifgdnphcl).  
