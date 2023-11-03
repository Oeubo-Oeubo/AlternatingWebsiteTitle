# How To Change Your Website Title With An Animated Array

Here is a simple vanilla JavaScript function that will change the original title of the website into different strings within an array. These strings will appear in order and only when you click off of the website.

## Step 1: Setup Your Boilerplate & Add Script Tag Within Head

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Alternating Title Project</title>
    <script>

    </script>
  </head>
  <body></body>
</html>
```

## Step 2: Create A Variable For Website Title and Create Your Array

We will need to create a constant called "title" to be able to read and write within the <title> DOM element.

```
const title = document.title;
```

Now create an array called "newTitle" that will consist of strings that you want the <title> to be.
(Keep in mind that long titles will be cut off.)

```
const newTitle = [
  // Keep in mind of character length because a long title will be cut off
  "Line One",
  "Line Two",
  "Line Three",
  "Line Four",
  "Line Five",
];
```

## Step 3: Window onBlur Function

We will need to create an event listener that detects when we are not actively on our website. This function will be activated when we are in a different tab or click on a different browser window.

```
window.addEventListener("blur", function () {

});
```

Within this function, we are going to set an interval that will change the title in order of the array every four seconds. First, we will need to create a variable for this interval called "intervalTime" and set it to null. Null will stop the interval from running. Second, create a "speed" variable that equals 4000 milliseconds (4 seconds). This variable will make it easier to adjust speed in the future.

```
var intervalTime = null;
var speed = 4000;
window.addEventListener("blur", function () {
  intervalTime = setInterval(function () {

  }, speed);
});
```

Inside the setInterval function, create an if statement with a variable named "i" and if i is less than newTitle array minus one, add one to i. If false, i equals 0. This if statement will reset to zero if the incremental increase exceeds the length of the array.

```
window.addEventListener("blur", function () {
  intervalTime = setInterval(function () {
    if (i < newTitle.length - 1) {
      i++;
    } else {
      i = 0;
    }
    document.title = newTitle[i]; // This replaces the title with which number of the array it is on
  }, speed);
});
```

## Step 4: Windows onFocus Function

We will want to reset the <title> element back to it's original value by creating an onFocus function that is activated when we are actively on the website.

```
window.addEventListener("focus", function () {

});
```

Inside the onFocus function, we need to clear the interval so it starts from the beginning the next time we click off and have the document.title equal title again.

```
window.addEventListener("focus", function () {
  // When the window is focused (you are actively on)
  clearInterval(intervalTime);
  document.title = title; // Changes back to original title
});
```

## Final Code

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Alternating Title Project</title>

    <script>
      const title = document.title;
      const newTitle = [
        // keep in mind of character length as a long title will be cut off
        "Line One",
        "Line Two",
        "Line Three",
        "Line Four",
        "Line Five",
      ];

      var intervalTime = null; // null will stop the interval
      var i = -1; // -1 will start at the first string of the array
      var speed = 4000; // 4 seconds

      window.addEventListener("blur", function () {
        // When the window is blurred (you are not actively on and have clicked off screen)
        intervalTime = setInterval(function () {
          if (i < newTitle.length - 1) {
            i++;
          } else {
            i = 0;
          }
          document.title = newTitle[i]; // This replace the title with which number of the array it is on
        }, speed);
      });

      window.addEventListener("focus", function () {
        // When the window is focused (you are actively on)
        clearInterval(intervalTime);
        document.title = title; // Changes back to original title
      });
    </script>
  </head>
  <body></body>
</html>
```
