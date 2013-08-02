---
date: '2011-05-13 02:42:24'
layout: post
slug: using-a-google-spreadsheet-as-a-grade-book
status: publish
title: Using a Google Spreadsheet as a gradebook
wordpress_id: '778'
categories:
- tech
tags:
- google
- javascript
---

Over the past couple years I've been a Teaching/Graduate Assistant for several courses, and being the lazy nerd that I am, I've streamlined my boring tasks in these areas. One task of particular importance is storing student grades and sending out student grade reports. There are several tools that teachers generally use to handle these tasks; however, TAs/GAs don't usually have access to this administrative software. This being the case, I created my own solution with Google Docs.

It's no mystery that spreadsheets are an excellent way to store tabular data such as student grade reports, but generally this is done with Excel on a personal machine. Excel is great and has many features that Google Docs does not; however, the door swings both ways. Google Docs allows for great accessibility since it is stored on the Google cloud. You can access and edit the document via any computer or phone (with authentication, of course). This is great for TAs. Students generally want information about their grades when you don't have your materials with you, but with Google Docs the materials are always there.

### Calculating Grades

One of the obvious disadvantages of the pen and paper approach is that the grades must be calculated each time you want to know an average or potentential grade. What if a new quiz grade comes in? You have to calculate again. And every time you manually enter numbers into the calculator it increases your chances for human error. With a spreadsheet these calculations are done automatically in real time. You can easily gain analysis of how an individual is doing or data on the class as a whole. The functions aren't all that difficult once you understand how to use them.

Each square in a spreadsheet is called a cell. Horizontal lines of cells are called rows and vertical lines of cells are called columns. To create a calculation within a cell simply click on it and press the = sign. Then you can type out a calculation. For example, if I have a row of different grades in cells A1-M1 and I want to average them all together I can go to the cell to the right of the last grade(N1) and then type `=AVERAGE(A1:M1)` and hit enter. This will fill the current cell (N1) with the average of all those grades.

One of the nice things about spreadsheets is that you can use autocompletion to fill in these rows or columns. For example, if you start with a blank spreadsheet and start in the very top upper left, enter the number 1, go down one cell and enter the number 2, you can then select those two cells, click on the bottom right corner of the number 2 cell and drag downwards as many cells as you like. This will number the cells linearly (1,2,3,4,5...). This autocompletion can also be used to repeat a function. So if I had several rows of student grades and want to provide averages for all of them I could simply click on the bottom right of the function I made in N1 and drag it down. It will automatically provide averages for each row.

Now this can get as complicated as you'd like it to. For instance, in some of the classes I've taught we've used a point system where quizzes are worth 20 points and exams are worth 100 points. Averaging those grades together is useless! Instead, I can get the sum of the grades, multiply it by 100 and divide it by the sum of the possible points. If the maximum points possible was 400, this calculation would look like `=SUM(A1:M1) * 100 / 400` If I want to drop the lowest quiz grade, I can use the min function like so: `=(SUM(A1:M1) - MIN(A1:M1)) * 100 / 380` If I put all the potential points for assignments in a row above the students grades then I can automatically calculate the 400 and 380 as well instead of manually entering them. These can likewise be used to generate assignment averages and potential grades.

### Emailing Grades

What I've said already should be enough reason to move to Google Docs instead of pen and paper or a local Excel file, but if you're looking to go above and beyond I will show you how can e-mail individual grade reports to students with a Google spreadsheet. First, you'll need a spreadsheet with grades in it. Each row should have a cell with the student's name and a cell with the student's e-mail. Then go to Tools→Script editor and open a new script window. Here's the code I use:


```
function sendGrades() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var startRow = 2;    // First row of data to process
  var numRows = 13;    // Number of rows to process
  var startColumn = 1; // First column of data to process
  var numColumn = 14;  // Number of columns to process
  // Fetch the range of cells
  var dataRange = sheet.getRange(startRow, startColumn, 
                     numRows, numColumn);
  // Fetch values for each row in the Range.
  var data = dataRange.getValues();
  for (i in data) {
    var row = data[i];
    var first_name = row[0];
    var last_name = row[1];
    var emailAddress = row[2];
    var quiz1 = row[3];
    var quiz2 = row[4];
    var quiz3 = row[5];
    var quiz4 = row[6];
    var practical1 = row[7];
    var quiz5 = row[8];
    var quiz6 = row[9];
    var quiz7 = row[10];
    var practical2 = row[11];
    var finalnum = row[12];
    var finallet = row[13];
    var subject = "Grade Report";
    var message = ""+
      "Hey guys,\n"+
      "\n"+
      "Here is your grade report for the semester.\n"+
      "Regards,\n"+
      "Conner\n"+
      "\n"+
      last_name+", "+first_name+" - Grades:\n"+
      " - Quiz 1: "+quiz1+"/10\n"+
      " - Quiz 2: "+quiz2+"/10\n"+
      " - Quiz 3: "+quiz3+"/10\n"+
      " - Quiz 4: "+quiz4+"/10\n"+
      " - Practical 1: "+practical1+"/50\n"+
      " - Quiz 5: "+quiz5+"/10\n"+
      " - Quiz 6: "+quiz6+"/10\n"+
      " - Quiz 7: "+quiz7+"/10\n"+
      " - Practical 2: "+practical2+"/50\n"+
      " - Final Average: "+finalnum+"\n"+
      " - Final Grade: "+finallet;
    MailApp.sendEmail(emailAddress, subject, message);
  }
}
```


The start row is 2 since I reserve the first row of my spreadsheet for headings where I can specify the assignment name. Since I had 13 students in this lab, the number of rows is set to 13. The start column is 1 since the students' first names are in the first column and the number of columns is 14 since there were 9 assignments, a column for a final average, a column for a final letter grade and 3 columns for first name, last name, and e-mail address. You can set the e-mails subject in the subject field and specify a message with the message field. It might help to know a little bit about coding at this point, but if you're uncomfortable then just edit the names of things and leave the stuff you don't understand the same. The last line of the script sends the e-mail. Each student will receive a grade report. If you want to test it first you can change the MailApp.sendEmail() line to `Logger.log(message);` and add a new line after the next curly brace with `MailApp.sendEmail('your@email.com', 'Hi', Logger.getLog());`For instance...

```
...
    //MailApp.sendEmail(emailAddress, subject, message);
    Logger.log(message);
  }
  MailApp.sendEmail('your@email.com', 'Hi', Logger.getLog());
}
```


Just click the Play icon at the top of the script to run it, or alternatively click on Run and then the function name. This can easily be modified to fit any course, so you don't have to rewrite all of this all over again.
