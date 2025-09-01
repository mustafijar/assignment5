1)What is the difference between getElementById, getElementsByClassName, and querySelector / querySelectorAll?
1.1 document.getElementById("btn")
Finds one element with the specified id.
Returns a single element object or null if it is not found.
ID is unique, so only one element is expected.
1.2 document.getElementsByClassName("classCard")
Finds all elements with that class.
Returns an HTMLCollection that updates automatically if the DOM changes.
Access elements by index: [0], [1], etc.
It is not a real array and needs conversion with Array.from().
1.3 document.querySelector(".card")
Finds the first element that matches a CSS selector (#id, .class, div > p, etc.).
Returns a single element object or null.
1.4 document.querySelectorAll(".card")
Finds all elements that match a CSS selector.
Returns a NodeList that does not update automatically.
NodeList supports iteration with forEach; it looks like an array but is not a real array.

2)How do you create and insert a new element into the DOM?
Steps:

Create element: const div = document.createElement("div");
Set content and attributes:
div.textContent = "Hello!";
div.className = "myClass";
div.setAttribute("id", "uniqueId");
Insert into DOM:
parent.appendChild(div); adds at the end
parent.prepend(div); adds at the beginning
sibling.before(div); or sibling.after(div);
oldElement.replaceWith(div);
3)What is Event Bubbling and how does it work?
When an event happens on an element, it first triggers on that element (target). Then it bubbles up to the parent, grandparent, and all the way to the document.
Example:
button.addEventListener("click", () => console.log("button clicked")); div.addEventListener("click", () => console.log("div clicked")); document.body.addEventListener("click", () => console.log("body clicked")); Clicking a button logs:
button clicked, div clicked, body clicked.

4)What is Event Delegation in JavaScript? Why is it useful?
Definition: Event Delegation is a technique where you attach a single event listener to a parent element instead of adding multiple listeners to child elements. Because of event bubbling, the parent can notice events that occur on its children and manage them appropriately. How it works:
a. Events bubble up from the target element to its ancestors. b. The parent element’s event listener can check event.target to determine which child was clicked or triggered. Example:
// Instead of adding click listener to each

document.querySelector("ul").addEventListener("click", function(e) { if (e.target.tagName === "LI") { console.log("Clicked:", e.target.textContent); } }); Why it is useful:
Efficiency: Fewer event listeners mean less memory use and improved performance. Dynamic elements: Newly added child elements work automatically without needing new listeners. Simpler code maintenance: There is only one listener instead of many.
5)What is the difference between preventDefault() and stopPropagation() methods?
event.preventDefault() Stops the default action/behavior of an element. Example: Prevent a form from submitting. Stop a link () from opening a new page. document.querySelector("a").addEventListener("click", function(e) { e.preventDefault(); // link will not open console.log("Link click prevented!"); });

event.stopPropagation() Stops the event from bubbling (or capturing) to parent elements. Example: document.querySelector(".child").addEventListener("click", function(e) { e.stopPropagation(); // event will not reach parent console.log("Child clicked, but parent won't know."); });

document.querySelector(".parent").addEventListener("click", function() { console.log("Parent clicked"); });
