# Task Manager

## DOM Task Manager

<div align="center">
  <img src="./asset/light.png" width="49%" alt="Task Manager Light Mode">
  <img src="./asset/dark.png" width="49%" alt="Task Manager Dark Mode">
</div>

## Live Demo

Add your live project link here:

`YOUR_LIVE_DEMO_LINK`

## GitHub Repository

Add your repository link here:

`https://github.com/masumprajapati5/Task-Manager`

---

## 1. Attributes vs Properties

There is a difference between:

```js
input.value
```

and

```js
input.getAttribute("value")
```

`input.value` is a DOM property. It gives us the current value of the input.

For example, if the user types something inside the input:

```js
console.log(input.value);
```

it returns what the user has currently entered.

On the other hand:

```js
console.log(input.getAttribute("value"));
```

reads the `value` attribute that was originally written in the HTML.

Example:

```html
<input type="text" value="Task 1">
```

If the user changes `Task 1` to `Task 2`:

```js
input.value
```

will return:

```text
Task 2
```

while:

```js
input.getAttribute("value")
```

can still return:

```text
Task 1
```

So basically:

```text
input.value                  -> current DOM value
input.getAttribute("value")  -> HTML attribute value
```

---

## 2. Event Propagation

Event propagation describes how an event travels through the DOM.

For example:

```html
<div id="grandparent">
    <div id="parent">
        <button id="child">Click Me</button>
    </div>
</div>
```

### Event Bubbling

In bubbling, the event starts from the target and then moves towards its parent elements.

```text
Child
  ↓
Parent
  ↓
Grandparent
```

Example:

```js
child.addEventListener("click", () => {
    console.log("Child");
});

parent.addEventListener("click", () => {
    console.log("Parent");
});

grandparent.addEventListener("click", () => {
    console.log("Grandparent");
});
```

When the child is clicked, the console output will be:

```text
Child
Parent
Grandparent
```

This project also uses bubbling for **event delegation**.

Instead of putting separate event listeners on every Edit, Delete and Complete button, one event listener is added to the task container.

```js
allTasks.addEventListener("click", (e) => {
    const card = e.target.closest(".task");

    if (!card) return;

    // Edit, Delete and Complete actions
});
```

This is useful because task cards are created dynamically.

### Event Capturing

Capturing works in the opposite direction.

The event travels from the outer element towards the target.

```text
Grandparent
    ↓
Parent
    ↓
Child
```

Capturing can be enabled by passing `true`:

```js
grandparent.addEventListener("click", () => {
    console.log("Grandparent");
}, true);

parent.addEventListener("click", () => {
    console.log("Parent");
}, true);

child.addEventListener("click", () => {
    console.log("Child");
}, true);
```

Output:

```text
Grandparent
Parent
Child
```

So:

```text
Capturing -> Parent to Target
Bubbling  -> Target to Parent
```

---

## 3. Browser Rendering Pipeline

The browser cannot directly display HTML and CSS as we write them.

It processes the files through multiple steps before showing the final webpage.

### HTML Process

First the browser receives the HTML.

```text
HTML
 ↓
Tokenization
 ↓
Parsing
 ↓
DOM Tree
```

### Tokenization

The HTML code is broken into smaller tokens.

For example:

```html
<h1>Task Manager</h1>
```

contains information such as:

```text
Opening h1 tag
Text
Closing h1 tag
```

### Parsing

The browser processes these tokens and understands the relationship between the elements.

It then creates the DOM.

### DOM Tree

DOM stands for **Document Object Model**.

HTML is represented as a tree of objects.

Example:

```text
Document
   ↓
HTML
 ├── Head
 └── Body
      ├── Nav
      ├── Section
      └── Main
```

JavaScript can then access and manipulate these DOM elements.

For example:

```js
document.querySelector("#allTasks");
```

---

## 4. CSSOM Tree

CSS also goes through processing.

```text
CSS
 ↓
Tokenization
 ↓
Parsing
 ↓
CSSOM Tree
```

CSSOM stands for **CSS Object Model**.

It contains the styling information required by the browser.

After the DOM and CSSOM are ready, the browser combines them.

```text
DOM Tree + CSSOM Tree
          ↓
      Render Tree
```

---

## 5. Render Tree

The Render Tree contains the elements that need to be displayed along with their calculated styles.

After creating the Render Tree, the browser continues with:

```text
DOM + CSSOM
     ↓
Render Tree
     ↓
Layout
     ↓
Paint
     ↓
Composite
```

### Layout

The browser calculates the size and position of elements.

For example:

- width
- height
- position
- spacing

### Paint

After layout, the browser draws the visual parts of the webpage such as:

- text
- backgrounds
- borders
- buttons
- shadows

### Composite

Some elements can be placed on separate layers, especially when properties such as `transform` and `opacity` are involved.

The browser then combines these layers to produce the final image displayed on the screen.

---

## 6. DOM Manipulation

Tasks in this project are generated dynamically using JavaScript.

For example:

```js
const card = document.createElement("div");

card.classList.add("task");

allTasks.append(card);
```

Each task also stores information using custom data attributes:

```js
card.dataset.id = x.id;
card.dataset.category = x.category;
card.dataset.status = x.status;
```

This results in something similar to:

```html
<div
    class="task"
    data-id="1"
    data-category="Work"
    data-status="Pending">
</div>
```

---

## 7. Features

The Task Manager currently includes:

- Add Task
- Edit Task
- Delete Task
- Complete / Undo Task
- Search Tasks
- Category Filter
- Completed Tasks Filter
- Pending Tasks Filter
- Total Task Counter
- Completed Task Counter
- Pending Task Counter
- Dark / Light Mode
- Local Storage
- Responsive Design
- Event Delegation

---

## Tech Stack

```text
HTML
CSS
Vanilla JavaScript
Local Storage
```

No JavaScript framework is used.