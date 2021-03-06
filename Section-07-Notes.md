# JavaScript - The Complete Guide 2020 (Beginner + Advanced)

## Section 07: Working with the DOM

## 145 Module Introduction

- HTML, DOM & JavaScript
- Nodes & Elements
- Querying DOM Nodes & Traversing the DOM
- Evaluation & Manipulating DOM Nodes
- Creating & Removing DOM Nodes

## 146 What's the DOM?

- HTML Parsed & Rendered by Browser
- JavaScript is a "Hosted Language"
- Browser Exposes Web API to allow JavaScript to work with the parsed document
- DOM = Object Representation of Loaded and Rendered HTML Code

```javascript
const titleEl = document.querySelector("h1"); // select the first h1 HTML Element node
```

- DOM is not strictly tied to Browsers! There are other tools that can parse HTML!
- "document" is the Root DOM Node
- Provides access to element querying, DOM content, etc
- "document" is a property of the "window" object

- "window" reflects the active Browser Window/Tab
- Acts as global storage for script, also provides access to window-specific properties and methods

## 147 Document and Window Object

```javascript
console.log(document); // prints html elements
console.dir(document); // prints DOM Object Property tree

document.element; // HTML element tree

console.log(window); // All the core APIs that the Browser wants to expose to me
console.dir(window); // Both log and dir print the same thing, the Object Property tree
```

## 148 Understanding the DOM and how it's created

- The Document Object Model (DOM)

```html
<html>
	<head>
		<title>The DOM</title>
	</head>
	<body>
		<header>
			<h1>Dive Into the DOM</h1>
		</header>
		<main>
			<p>There's a lot to it!</p>
		</main>
	</body>
</html>
```

- The browser renders the pixels AND
- Stores these tags as an Object in memory
- html element NODES
- A Tree of Nodes, parents and children
- Text Nodes, including whitespace and line breaks
- Element Nodes are different than text nodes
- Chrome tools Elements Tab
- == \$0
- console.dir(\$0); // You get the properties for the specific element
  - Even for an h1 tag, there are MANY properties

## 149 Nodes & Elements - Querying the DOM Overview

- querySelector() // gets single elements
- getElementById() // gets single elements
- Different ways of querying elements(by CSS selector, by ID)

- querySelectorAll() // gets collections elements (NodeList)
  - a "non-live" NodeList, that is, a "snapshot" of the currently rendered DOM
- getElementsByTagName()

- Nodes and Elements (There's a Difference)

  - Nodes

    - The objects that make up the DOM
    - HTML tags are "element nodes" (or just "elements")
    - Text creates "text nodes"
    - Attributes create "attribute nodes"

  - Elements

    - One type of node
    - Special properties and methods to interact with the elements
    - Available methods and properties depend on the kind of element
    - Can be selected in various different ways (via JavaScript)
    - Can be created and removed via JavaScript

## 150 Selecting Elements in the DOM

Chrome Browser Tools:

```javascript
document.getElementById("main-title"); // prints the selected element node

console.log(document.getElementById("main-title")); // shows the property list
```

```javascript
document.getElementsByClassName("list-item"); // returns HTMLCollection(number of elements in the collection)
// for-of loops work here

document.querySelector(".list-item"); // returns first matching item of NodeList
document.querySelectorAll(".list-item"); // returns entire NodeList(number of elements in the collection)

document.querySelector("ul li:first-of-type"); // returns first matching item of NodeList
document.querySelector("ul li:last-of-type"); // returns last matching item of NodeList
```

These selections can be made without a page reload.

## 151 Summary: Node Query Methods

## 152 Exploring and Changing DOM Properties

- Evaluating and Manipulating Elements

```javascript
<p id="welcome-text" class="text-default">
	Welcome!
</p>;

document.getElementById("welcome-text");

const p = document.getElementById("welcome-text");

p.textContent; // "Welcome!";
p.id; // "welcome-text";
p.className; // "text-default";

// Assign a new value to the className
p.className = "new-class"; // <p...class="new-class">
```

Back to the Browser Tools:

```javascript
const h1 = document.querySelector("h1");

// <header><h1 id="main-title">Dive Into the DOM!</h1></header>

h1.textContent; // "Dive Into the DOM!
h1.className; // "" No class is designated

// Assign some new text
h1.textContent = "Some new text!"; // "Some new text!"; appears as the new h1 text in the Browser

// Assign a new CSS class
h1.className = "title";

// Browser Tools > Elements
// <header><h1 id="main-title" class="title">Dive Into the DOM!</h1></header>

h1.style.color = "white";
h1.style.backgroundColor = "red"; // "background-color" probably doesn't work; check console.dir() & MDN
```

## 153 Attributes vs Properties

- Often, attributes are mapped to properties, but not always

```javascript
// <input id="input-1" class="input-default" value="Enter-text...">
// Attributes (placed in HTML code, on element tags)

const input
input.id // 1:1 mapping, yes (+live sync)
input.className // !1:1 mapping ("class" vs "className")(but live sync)
input.value // 1:1 mapping (1-way live sync, UI changes don't immediately change the property value)

input.setAttribute('value', 'some other default text'); // no UI change, but attribute change
input.value = input.getAttribute('value'); // makes the change
```

## 154 Selecting Multiple Elements & Summary

```javascript
const allLis = document.querySelectorAll("li"); // non-live list, snapshot

// If I wanted to work with a particular one, I'd have to access the index

const allLis = document.getElementsByTagName("li"); // live list
```

## 155 Traversing the DOM

- Children, Descendants, Parents, Ancestors

  - Child, DIRECT child node or element
  - Descendant, direct or indirect child node or element
  - Parent, direct relationship
  - Ancestor, direct or indirect relationship

```javascript
// document.body >> parentNode, parentElement, closest()

// previousSibling, previousElementSibling Current Node nextSibling, nextElementSibling
// <div>

// childNodes, children, querySelector()
// firstChild, firstElementChild, lastChild, lastElementChild
```

## 156 Traversing Child Nodes

```javascript
const ul = document.querySelector("ul");

ul.children[1]; // gets the 2nd child ELEMENT node, textNodes are excluded

ul.childNodes; // there are a bunch of textNodes in there
// "data" (property) on a textNode, sets the text of the textNode
```

## 157

```javascript
const liFirst = document.querySelector("li");

liFirst.parentElement; // Almost the same
liFirst.parentNode;

// Why do we have both?
document.documentElement.parentElement; // null
document.documentElement.parentNode; // #document

liFirst.closest("body"); // Closest ancestor
```

## 158

```javascript
const ul = li.parentElement;

ul.previousElementSibling; // previousSibling looks at ALL the nodes

ul.nextElementSibling;
```

## 159 DOM Traversal vs Query Methods

## 160

- Styles assigned to the style property override other styles (set by class, etc)
- Via style Property
- Via className
- Via classList
  - Object with built-in methods

```javascript
section.classList.toggle("visible");
section.classList.toggle("invisible");
```

## 161 Creating and Inserting Elements

- With innerHTML, the old html gets wiped
- I could append new data
- "Flashing changes" Re-rendered
- insertAdjacentHTML()
  - downside: No direct access to the newly-rendered content
  - eventListeners are not available
- document.createElement('li'); // tagName argument
- list.appendChild(newLi);

## 162 Adding Elements via HTML in Code

- list.append(newLi);
- list.append(newNode1, newNodeN...);

- list.prepend(newLi);
- list.prepend(newNode1, newNodeN...);

## 163 Adding Elements via createElement()

## 164 Inserting DOM Elements

- list.lastElementChild.before(newLi); // insert the element to a specific spot
- list.lastElementChild.after(newLi); // insert the element to a specific spot
- list.lastElementChild.replace(newLi); // replace the element

- list.insertAdjacentElement('afterend', newLi); // insert the element to a specific spot

## 165 Cloning DOM Nodes

- newLi.cloneNode(); // false > no children cloned, true > all children cloned

## 166 Live Node Lists vs Static Node Lists

- NodeList(s) // non-live
  - The reference values DO change dynamically, just not the collection
- HTMLCollection // live
  - Possible higher memory consumption

## 167 Removing Elements

```javascript
const list = document.querySelector("ul");
list.parentElement.removeChild(list);
```

## 168 Insertion & Removal Method Summary

## 169 Summary

## 170 Setting Up the Practice Project

## 171

## 172

## 173

## 174

## 175

## 176

## 177

## 178

## 179

## 180
