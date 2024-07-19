<h1 align="center">
  Todo App
</h1>

<p>
  I learnt how to handle form inputs, manage local storage, perform CRUD (Create, Read, Update, Delete) operations on tasks, implement event listeners, and toggle UI elements.
</p>

## Preview
https://github.com/user-attachments/assets/539a5ffb-bfe3-40fc-8aad-5eafbf392a12

## Steps
**S1**<br>
In this project, you will learn how `localStorage` works in JavaScript by building a Todo app. LocalStorage is a web storage feature of JavaScript that lets you persist data by storing the data as a <b>key:value</b> pair.<br>

The HTML and CSS for this project have been provided for you. Take a look at the files to get yourself familiarized with them.<br>

Begin by accessing the `task-form`, `confirm-close-dialog`, and `open-task-form-btn` elements with the `getElementById()` method. Save them in the variables `taskForm`, `confirmCloseDialog`, and `openTaskFormBtn`.

```js
const taskForm = document.getElementById("task-form");
const confirmCloseDialog = document.getElementById("confirm-close-dialog");
const openTaskFormBtn = document.getElementById("open-task-form-btn");
```

**S2**<br>
You need to access more elements with the `getElementById()` method. This time you need the `close-task-form-btn`, `add-or-update-task-btn`, and `cancel-btn` elements. Save them in the variables `closeTaskFormBtn`, `addOrUpdateTaskBtn`, and `cancelBtn`.

```js
const closeTaskFormBtn = document.getElementById("close-task-form-btn");
const addOrUpdateTaskBtn = document.getElementById("add-or-update-task-btn");
const cancelBtn = document.getElementById("cancel-btn");
```

**S3**<br>
Next, access the `discard-btn`, `tasks-container`, and `title-input` elements using the `getElementById()` method. Save them in variables named `discardBtn`, `tasksContainer`, and `titleInput`, respectively.

```js
const discardBtn = document.getElementById("discard-btn");
const tasksContainer = document.getElementById("tasks-container");
const titleInput = document.getElementById("title-input");
```

**S4**<br>
The last set of elements you need to get from the HTML file are the `date-input` and `description-input` elements. Save them in the variables `dateInput` and `descriptionInput` respectively.

```js
const dateInput  = document.getElementById("date-input");
const descriptionInput   = document.getElementById("description-input");
```

**S5**<br>
Create a `taskData` constant and set it to an empty array. This array will store all the tasks along with their associated data, including title, due date, and description. This storage will enable you to keep track of tasks, display them on the page, and save them to `localStorage`.<br>

Use `let` to create a `currentTask` variable and set it to an empty object. This variable will be used to track the state when editing and discarding tasks.

```js
const taskData = [];
let currentTask = {};
```

**S6**<br>
Now, you will work on opening and closing the form modal. In earlier projects, you learned how to add and remove classes from an element with `el.classList.add()` and `el.classList.remove()`. Another method to use with the `classList` property is the `toggle` method.<br>

The `toggle` method will add the class if it is not present on the element, and remove the class if it is present on the element.<br>
`Example Code`<br>
`element.classList.toggle("class-to-toggle");`<br>

Add an event listener to the `openTaskFormBtn` element and pass in a `click` event for the first argument and an empty callback function for the second argument. For the callback function, use the `classList.toggle()` method to toggle the `hidden` class on the taskForm element. Now you can `click` on the "Add new Task" button and see the form modal.

```js
openTaskFormBtn.addEventListener("click", () => {
  taskForm.classList.toggle("hidden")
});
```

**S7**<br>
The HTML `dialog` element has a `showModal()` method that can be used to display a modal dialog box on a web page.<br>

`Example Code`<br>
`dialogElement.showModal();`<br>

Add an event listener to the `closeTaskFormBtn` variable and pass in a `click` event for the first argument and a callback function for the second argument. For the callback function, call the `showModal()` method on the `confirmCloseDialog` element. This will display a modal with the `Discard` and `Cancel` buttons.

```js
closeTaskFormBtn.addEventListener("click", () => {
  confirmCloseDialog.showModal();
})
```

**S8**<br>
If the user clicks the `Cancel` button, you want to cancel the process and close the modal so the user can continue editing. The HTML `dialog` element has a `close()` method that can be used to close a modal dialog box on a web page.<br>

`Example Code`<br>
`dialogElement.close();`<br>

Add an event listener to the `cancelBtn` element and pass in a `click` event for the first argument and a callback function for the second argument. For the callback function, call the `close()` method on the `confirmCloseDialog` element.

```js
cancelBtn.addEventListener("click", () => {
  confirmCloseDialog.close();
})
```

**S9**<br>
If the user clicks the `Discard` button, you want to close the modal showing the `Cancel` and `Discard` buttons, then hide the form modal. <br>

Add a click event listener to `discardBtn`, then use the `close()` method on the `confirmCloseDialog` variable. Also, use `classList` to toggle the class `hidden` on `taskForm` so the form modal will close too.

```js
discardBtn.addEventListener("click", () => {
  confirmCloseDialog.close();
  taskForm.classList.toggle("hidden");
})
```

**S10**<br>
Now that you've worked on opening and closing the modal, it's time to get the values from the input fields, save them into the `taskData` array, and display them on the page.<br>

To start, add a `submit` event listener to your `taskForm` element and pass in `e` as the parameter of your arrow function. Inside the curly braces, use the `preventDefault()` method to stop the browser from refreshing the page after submitting the form.

```js
taskForm.addEventListener("submit", (e) => {
  e.preventDefault();
})
```

**S11**<br>
You will need to determine whether the task being added to the `taskData` array already exists or not. If the task does not exist, you will add it to the array. If it does exist, you will update it. To accomplish this, you can use the <i>findIndex()</i> method.<br>

The `findIndex()` array method finds and returns the index of the first element in an array that meets the criteria specified by a provided testing function. If no such element is found, the method returns `-1`. Here's an example:<br>

`Example Code`<br>
`const numbers = [3, 1, 5, 6];`<br>
`const firstNumLargerThanThree = numbers.findIndex((num) => num > 3);`<br>
`console.log(firstNumLargerThanThree); // prints index 2`<br>

Use `const` to declare a variable called `dataArrIndex` and assign it the value of `taskData.findIndex()`. For the `findIndex()` method, pass in an arrow function with `item` as the parameter. Within the arrow function, check if the id property of item is strictly equal to the id property of currentTask.

```js
const dataArrIndex  = taskData.findIndex((item) => item.id === currentTask.id)
```

**S12**<br>
When a user creates a task, it should be saved in an object.<br>

Create a `const` variable called `taskObj` and assign it the value of an empty object. Then below that, add a console statement that logs the value of `taskObj` to the console.<br>

Open up the console to see the empty object.

```js
const taskObj = {};
console.log(taskObj);
```

**S13**<br>
Inside your taskObj, add an id property name. For the value use the value of the titleInput.

To see the new result, click on the "Add New Task" button. Then add a title and click on the "Add Task" button. Open up the console to see the result.
```js
const taskObj = {
   id: titleInput.value
};
```

**S14**<br>
The user should be able to input a title with upper and lowercase letters. But for the `id`, the value should be all lowercase.<br>

Update your `titleInput.value` to be all lowercase. You can use the `toLowerCase()` method to do this.<br>
`Example Code`<br>
`str.toLowerCase();`<br>

To see the new result, click on the `"Add New Task"` button. Then add a title of `WALK DOG` and click on the `"Add Task"` button. Open up the console to see the result of `"walk dog"`.

```js
id: titleInput.value.toLowerCase()
```

**S15**<br>
Right now, your `id` value is a lowercase string. But the final result should be a hyphenated string.<br>

Start by chaining the `split` method to the `titleInput.value` to split the string into an array of words. For the separator, use a space character(`" "`).<br>

To see the new result, click on the `"Add New Task"` button. Then add a title of `WALK DOG` and click on the `"Add Task"` button. Open up the console to see the result of `['walk', 'dog']`.

```js
id: titleInput.value.toLowerCase().split(" ")
```

**S16**<br>
Now that your `id` is an array of words, you can use the `join` method to turn the result back into a string. For the separator, use a hyphen(`-`).<br>

To see the new result, click on the `"Add New Task"` button. Then add a title of `WALK DOG` and click on the `"Add Task"` button. Open up the console to see the result of `"walk-dog"`.

```js
id: titleInput.value.toLowerCase().split(" ").join("-")
```

**S17**<br>
There is one last thing you will need to do to make this `id` unique. But first, place the entire value below inside an embedded expression ${}.<br>

`Example Code`<br>
`titleInput.value.toLowerCase().split(" ").join("-")`<br>

Then wrap that value in template strings. In the next step, you will add a unique number to the end of the `id` value to make it truly unique.

```js
id: `${titleInput.value.toLowerCase().split(" ").join("-")}`
```

**S18**<br>
To make the `id` more unique, add another hyphen and use <i>Date.now()</i>. `Date.now()` returns the number of milliseconds elapsed since `January 1, 1970 00:00:00 UTC`.

`Example Code`<br>
`console.log(Date.now()); // 1628586800000`<br>

To see the new result, click on the `"Add New Task"` button. Then add a title of `WALK DOG` and click on the `"Add Task"` button. Open up the console to see the result.

```js
id: `${titleInput.value.toLowerCase().split(' ').join('-')}-${Date.now()}`
```

**S19**<br>
Now it is time to add the remaining properties to the `taskObj` object.<br>

Retrieve the values from the `titleInput`, `dateInput`, and `descriptionInput` fields, and then save them in the properties `title`, `date`, and `description` of the `taskObj` object.<br>

Add a new task and open up the console to see the taskObj object with the new properties.

```js
title: titleInput.value(),
date: dateInput.value(),
description: descriptionInput.value(),
```

**S20**<br>
Now that have finished testing your `taskObj`, you can remove the `console.log(taskObj)` statement.

```js

```

**S21**<br>
Now that you have obtained the values from the input fields and generated an `id`, you want to add them to your `taskData` array to keep track of each task. However, you should only do this if the task is new. If the task already exists, you will set it up for editing. This is why you have the `dataArrIndex` variable, which provides the index of each task. <br>

Create an `if` statement with the condition `dataArrIndex === -1`. Within the `if` statement, use the `unshift()` method to add the `taskObj` object to the beginning of the `taskData` array.<br>

`unshift()` is an array method that is used to add one or more elements to the beginning of an array.
`Example Code`<br>
`const arr = [1, 2, 3];`<br>
`arr.unshift(0);`<br>
`// [0, 1, 2, 3]`<br>
`console.log(arr);` 

```js
if (dataArrIndex === -1) {
  taskData.unshift(taskObj);
}
```

**S22**<br>
Now that you have saved the task in the `taskData` array, you should display the task on the page by looping through it. <br>

Use `forEach()` on `taskData`, then destructure `id`, `title`, `date`, `description` as the parameters. Don't return anything yet.

```js
taskData.forEach(({id, title, date, description}));
```

**S23**<br>
Using arrow syntax complete the `forEach` callback function. Inside the callback function body use an addition assignment to set the `innerHTML` of `tasksContainer` to empty backticks.

```js
taskData.forEach(({id, title, date, description}) => {
    tasksContainer.innerHTML += ``
  });
```

**S24**<br>
Create a `div` element with the class of `task`. Utilize template strings to set the `id` attribute of the `div` to the `id` you destructured from the task data.

```js
<div class="task" id="${id}"></div>
```

**S25**<br>
Create a `p` element and use template strings to set its content to the `title` you destructured. Right before the content of the `p` element, create a `strong` element with the text `Title:`.

```js
<p><strong>Title:</strong> ${title}</p>
```

**S26**<br>
Similarly to the previous step, create another `p` element, and interpolate the `date` you destructured as the text content. Inside this paragraph, create a `strong` element with the text `Date:`.

```js
<p><strong>Date:</strong> ${date}</p>
```

**S27**<br>
Create one more `p` element and interpolate the `description` you destructured as the text. Also, create a `strong` element inside the paragraph with the text `Description:`.

```js
<p><strong>Description:</strong> ${description}</p>
```

**S28**<br>
To allow for task management, you need to include both a delete and an edit button for each task.<br>

Create two `button` elements with the `type` attribute set to `button` and the `class` attribute set to `btn`. Set the text of the first button to `Edit` and the text of the second button to `Delete`.

```js
<button type="button" class="btn">Edit</button>
<button type="button" class="btn">Delete</button>
```

**S29**<br>
After adding the task to the page, you should close the form modal to view the task. To do this, utilize `classList` to toggle the `hidden` class on the `taskForm` element.

```js
taskForm.classList.toggle("hidden");
```

**S30**<br>
If you attempt to add another task now, you'll notice that the input fields retain the values you entered for the previous task. To resolve this, you need to clear the input fields after adding a task.<br>

Instead of clearing the input fields one by one, it's a good practice to create a function that handles clearing those fields. You can then call this function whenever you need to clear the input fields again.<bbr>

Use arrow syntax to create a `reset` function and set it to a pair of curly braces.<br>

```js
const reset = () => {};
```

**S31**<br>
Inside the `reset` function, set each value of `titleInput`, `dateInput`, `descriptionInput` to an empty string.<br>

Also, use `classList` to toggle the class `hidden` on the `taskForm` and set `currentTask` to an empty object. That's because at this point, `currentTask` will be filled with the task the user might have added.

```js
const reset = () => {
  titleInput.value = ""
  dateInput.value = ""
  descriptionInput.value = "" 
  taskForm.classList.toggle("hidden");
  currentTask = {}
}
```

**S32**<br>
Remove the existing code toggling the class of `hidden` on `taskForm` and call the `reset` function instead. This would clear the input fields and also hide the form modal for the user to see the added task.

```js
reset();
```

**S33**<br>
Also, remove the existing code toggling the class `hidden` on `taskForm` inside the `discardBtn` event listener and call the `reset` function instead. That's because when you click the `Discard` button, everything in the input fields should go away.

```js
reset();
```

**S34**<br>
You should display the `Cancel` and `Discard` buttons to the user only if there is some text present in the input fields. <br>

To begin, within the `closeTaskFormBtn` event listener, create a `formInputsContainValues` variable to check if there is a value in the `titleInput` field or the `dateInput` field or the `descriptionInput` field.

```js
const formInputsContainValues = titleInput.value || dateInput.value || descriptionInput.value;
```

**S35**<br>
Create an `if` statement to check if `formInputsContainValues` is true. If `formInputsContainValues` is true, indicating that there are changes, use the `showModal()` method on `confirmCloseDialog`. Otherwise, if there are no changes, call the `reset()` function to clear the input fields and hide the form modal.

```js
if (formInputsContainValues){
  confirmCloseDialog.showModal();
} else {
  reset();
};
```

**S36**<br>
You can enhance code readability and maintainability by refactoring the `submit` event listener into two separate functions. The first function can be used to add the input values to `taskData`, while the second function can be responsible for adding the tasks to the DOM. <br>

Use arrow syntax to create an `addOrUpdateTask` function. Then move the `dataArrIndex` variable, the `taskObj` object, and the `if` statement into the `addOrUpdateTask` function.

```js
const addOrUpdateTask = () => {
  const dataArrIndex = taskData.findIndex((item) => item.id === currentTask.id);
  const taskObj = {
    id: `${titleInput.value.toLowerCase().split(" ").join("-")}-${Date.now()}`,
    title: titleInput.value,
    date: dateInput.value,
    description: descriptionInput.value,
  };

  if (dataArrIndex === -1) {
    taskData.unshift(taskObj);
  };
};
```

**S37**<br>
Use arrow syntax to create an updateTaskContainer function. Then move the taskData.forEach() and its content into it.

```js
const updateTaskContainer = () => {
  taskData.forEach(
    ({ id, title, date, description }) => {
    (tasksContainer.innerHTML += `
    <div class="task" id="${id}">
      <p><strong>Title:</strong> ${title}</p>
      <p><strong>Date:</strong> ${date}</p>
      <p><strong>Description:</strong> ${description}</p>
      <button type="button" class="btn">Edit</button>
      <button type="button" class="btn">Delete</button>
    </div>
    `)
    }
  );
};
```

**S38**<br>
Inside the `addOrUpdateTask` function, call the `updateTaskContainer` and `reset` functions.

```js
updateTaskContainer();
reset();
```

**S39**<br>
Now remove the `reset()` call inside the `taskForm` submit event listener and call the `addOrUpdateTask` function instead.

```js
addOrUpdateTask();
```

**S40**<br>
There's a problem. If you add a task, and then add another, the previous task gets duplicated. This means you need to clear out the existing contents of `tasksContainer` before adding a new task.<br>

Set the `innerHTML` of `tasksContainer` back to an empty string.

```js
tasksContainer.innerHTML = "";
```

**S41**<br>
To enable editing and deleting for each task, add an `onclick` attribute to both buttons. Set the value of the `onclick` attribute to `editTask(this)` for the `Edit` button and `deleteTask(this)` for the `Delete` button. The `editTask(this)` function will handle editing, while the `deleteTask(this)` function will handle deletion.<br>

`this` is a keyword that refers to the current context. In this case, `this` points to the element that triggers the event – the buttons.

```js
<button type="button" class="btn" onclick="editTask(this)">Edit</button>
<button type="button" class="btn" onclick="deleteTask(this)">Delete</button> 
```

**S42**<br>
Create a `deleteTask` function using arrow syntax. Pass `buttonEl` as the parameter and define an empty set of curly braces for the function body.

```js
const deleteTask = (buttonEl) => {}
```

**S43**<br>
You need to find the index of the task you want to delete first.<br>

Create a `dataArrIndex` variable and set its value using the `findIndex()` method on the `taskData` array. Pass `item` as the parameter for the arrow callback function, and within the callback, check if the `id` of `item` is equal to the `id` of the `parentElement` of `buttonEl`.

```js
const deleteTask = (buttonEl) => {
  const dataArrIndex = taskData.findIndex((item) => item.id === buttonEl.parentElement.id)
}
```

**S44**<br>
You need to remove the task from the DOM using `remove()` and from the `taskData` array using `splice()`.<br>

`splice()` is an array method that modifies arrays by removing, replacing, or adding elements at a specified index, while also returning the removed elements. It can take up to three arguments: the first one is the mandatory index at which to start, the second is the number of items to remove, and the third is an optional replacement element.<br>

Here's an example:<br>
<b>`Example Code`</b><br>
`const fruits = ["mango", "date", "cherry", "banana", "apple"];`<br>
`// Remove date and cherry from the array starting at index 1`<br>
`const removedFruits = fruits.splice(1, 2);`<br>
`console.log(fruits); // [ 'mango', 'banana', 'apple' ]`<br>
`console.log(removedFruits); // [ 'date', 'cherry' ]`<br>

Use the `remove()` method to remove the `parentElement` of the `buttonEl` from the DOM. Then use `splice()` to remove the task from the `taskData` array. Pass in `dataArrIndex` and `1` as the arguments of your splice(). `dataArrIndex` is the index to start and `1` is the number of items to remove.

```js
const deleteTask = (buttonEl) => {
  const dataArrIndex = taskData.findIndex(
    (item) => item.id === buttonEl.parentElement.id
  );
  buttonEl.parentElement.remove();
  taskData.splice(dataArrIndex, 1);
}
```

**S45**<br>
Use arrow syntax to create an `editTask` function. Pass in `buttonEl` as the parameter and add empty curly braces for the body.

```js
const editTask = (buttonEl) => {}
```

**S46**<br>
As you did in the `deleteTask` function, you need to find the index of the task to be edited.<br>

Create a `dataArrIndex` variable. For its value, utilize the `findIndex()` method on `taskData`. Pass `item` as the parameter to its callback function and check if the `id` of `item` is equal to the `id` of the `parentElement` of `buttonEl`.

```js
const dataArrIndex = taskData.findIndex((item) => item.id === buttonEl.parentElement.id)
```

**S47**<br>
Use square bracket notation to retrieve the task to be edited from the `taskData` array using the `dataArrIndex`. Then, assign it to the `currentTask` object to keep track of it.

```js
currentTask = taskData[dataArrIndex];
```

**S48**<br>
The task to be edited is now in the `currentTask` object. Stage it for editing inside the input fields by setting the value of `titleInput` to `currentTask.title`, `dateInput` to `currentTask.date`, and `descriptionInput` to `currentTask.description`.

```js
titleInput.value = currentTask.title;
dateInput. value = currentTask.date;
descriptionInput.value = currentTask.description;
```

**S49**<br>
Set the `innerText` of the `addOrUpdateTaskBtn` button to `Update Task`.

```js
addOrUpdateTaskBtn.innerText = "Update Task";
```

**S50**<br>
Finally, display the `form` modal with the values of the input fields by using `classList` to toggle the `hidden` class on `taskForm`.

```js
taskForm.classList.toggle("hidden");
```

**S51**<br>
At this point, editing a task won't reflect when you submit the task. To make the editing functional, go back to the `if` statement inside the `addOrUpdateTask` function. Create an `else` block and set `taskData[dataArrIndex]` to `taskObj`.

```js
if (dataArrIndex === -1) {
  taskData.unshift(taskObj);
  } else {
    taskData[dataArrIndex] = taskObj;
}
```

**S52**<br>
If the user attempts to edit a task but decides not to make any changes before closing the form, there is no need to display the modal with the `Cancel` and `Discard` buttons.<br>

Inside the `closeTaskFormBtn` event listener, use `const` to create another variable named `formInputValuesUpdated`. Check if the user made changes while trying to edit a task by verifying that the `titleInput` value <b>is not equal to</b> `currentTask.title`, or the `dateInput` value <b>is not equal to</b> `currentTask.date`, or the `descriptionInput` value <b>is not equal to</b> `currentTask.description`.

```js
const formInputValuesUpdated = titleInput.value !== currentTask.title || dateInput.value !== currentTask.date || descriptionInput.value !== currentTask.description;
```

**S53**<br>
Now add `formInputValuesUpdated` as the second mandatory condition in the `if` statement using the `AND` operator.<br>

This way, the Cancel and Discard buttons in the modal won't be displayed to the user if they haven't made any changes to the input fields while attempting to edit a task.
```js
if (formInputsContainValues && formInputValuesUpdated) {
  confirmCloseDialog.showModal();
  } else {
    reset();
}
```

**S54**<br>
`localStorage` offers methods for saving, retrieving, and deleting items. The items you save can be of any JavaScript data type.For instance, the `setItem()` method is used to save an item, and the `getItem()` method retrieves the item. To delete a specific item, you can utilize the `removeItem()` method, or if you want to delete all items in the storage, you can use `clear()`.

Here's how you can save an item:<br>
`Example Code`<br>
`localStorage.setItem("key", value); // value could be string, number, or any other data type`<br>

A `myTaskArr` array has been provided for you. Use the `setItem()` method to save it with a key of `data`. After that, open your browser console and go to the Applications tab, select Local Storage, and the freeCodeCamp domain you see.

```js
localStorage.setItem("data", myTaskArr)
```

**S55**<br>
If you check the "Application" tab of your browser console, you'll notice a series of `[object Object]`. This is because everything you save in `localStorage` needs to be in string format.<br>

To resolve the issue, wrap the data you're saving in the `JSON.stringify()` method. Then, check local storage again to observe the results.

```js
localStorage.setItem("data", JSON.stringify(myTaskArr));
```

**S56**<br>
Now that you have the `myTaskArr` array saved in `localStorage` correctly, you can retrieve it with `getItem()` by specifying the key you used to save the item.<br>

Use the `getItem()` method to retrieve the `myTaskArr` array and assign it to the variable `getTaskArr`. Then, log the `getTaskArr` variable to the console to see the result.

```js
const getTaskArr = localStorage.getItem("data");
console.log(getTaskArr);
```

**S57**<br>
The item you retrieve is a string, as you saved it with `JSON.stringify()`. To view it in its original form before saving, you need to use `JSON.parse()`.<br>

Use `getItem()` to retrieve the `myTaskArr` array again. This time, wrap it inside `JSON.parse()`, assign it to the variable `getTaskArrObj` and log the `getTaskArrObj` to the console.<br>

Check the console to see the difference between `getTaskArr` and `getTaskObj`.

```js
const getTaskArrObj = JSON.parse(localStorage.getItem("data"));
console.log(getTaskArrObj);
```

**S58**<br>
You can use `localStorage.removeItem()` to remove a specific item and `localStorage.clear()` to clear all items in the local storage.<br>

Remove the `data` item from local storage and open the console to observe the result. You should see `null`.

```js
localStorage.removeItem("data");
```

**S59**<br>
Using `localStorage.clear()` won't just delete a single item from local storage but will remove all items.<br>

Remove `localStorage.removeItem()` and use `localStorage.clear()` instead. You don't need to pass in anything. You should also see `null` in the console.

```js
localStorage.clear();
```

**S60**<br>
Remove the `myTaskArr` array and all of the code for `localStorage` because you don't need them anymore.

```js
```

**S61**<br>
Now you should save the task items to local storage when the user adds, updates, or removes a task.<br>

Inside the `addOrUpdateTask` function, use `setItem()` to save the tasks with a key of `data`, then pass the `taskData` array as its argument. Ensure that you stringify the `taskData`. This would persist data once the user adds or updates tasks.

```js
localStorage.setItem("data", JSON.stringify(taskData));
```

**S62**<br>
You also want a deleted task to be removed from local storage. For this, you don't need the `removeItem()` or `clear()` methods. Since you already use `splice()` to remove the deleted task from `taskData`, all you need to do now is save `taskData` to local storage again.<br>

Use `setItem()` to save the `taskData` array again. Pass in `data` as the key and ensure that `taskData` is stringified before saving.

```js
localStorage.setItem("data", JSON.stringify(taskData));
```

**S63**<br>
If you add, update, or remove a task, it should reflect in the UI. However, that's not happening now because you have yet to retrieve the tasks. To do this, you need to modify your initial `taskData` to be an empty array.<br>

Set `taskData` to the retrieval of `data` from local storage or an empty array. Make sure you parse the data coming with `JSON.parse()` because you saved it as a string.

```js
const taskData = JSON.parse(localStorage.getItem("data")) || [];
```

**S64**<br>
You've retrieved the task item(s) now, but they still don't reflect in the UI when the page loads. However, they appear when you add a new task. You can check if there's a task inside `taskData` using the length of the array. Because `0` is a falsy value all you need for the condition is the array length.<br>

Here is an example checking the length of an array:<br>
<b>`Example Code`</b><br>
`if (arr.length) {`<br>
  `// do something`<br>
`}`<br>

In that example, if `arr` has a length greater than `0`, the code inside the `if` statement block will run. If `arr` has a length of `0`, the code inside the `if` statement block will not run.<br>

Check if there's a task inside `taskData`, then call the `updateTaskContainer()` inside the `if` statement block.

```js
if (taskData.length) {
  updateTaskContainer();
}
```

**S65**<br>
If you try to add a new task, edit that task, and then click on the `Add New Task button, you will notice a bug.<br>

The form button will display the incorrect text of `"Update Task"` instead of `"Add Task"`. To fix this, you will need to assign the string `"Add Task"` to `addOrUpdateTaskBtn.innerText` inside your reset `function`. With that, you've completed this project.

```js
addOrUpdateTaskBtn.innerText = "Add Task";
```
