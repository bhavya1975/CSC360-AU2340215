# Reflection

## Date: 8 September 2026

## Project Discussion

### Why do we need a `try-catch` block?

When we are using an external API, it could fail at any time. We can't simply show the error message in the console. We should rather log it in a proper format.

So we use:

```java
try {
    // logic
} catch (Exception error) {
    // show error message
}
```

---

### What are Generics in Java?

Generics allow us to dynamically specify a data type using the `<>` diamond brackets, which can be replaced with different data types.

---

### What is a View in Java?

It is a read-only subset of pre-written queries or data, or something similar.

---

### Collections in Java

* LinkedList
* Queue
* List
* Set
* HashMap

### How is event related to GUI

An event is a signal sent to the application indicating that a user action (like a mouse click, keypress, or window resize) or system trigger has occurred. The GUI manages these through an Event Dispatch Thread (EDT) running an continuous event loop (or main loop), 
which listens for incoming events and notifies the appropriate listeners to update the UI. 

### event hierarchy

When an event triggers, it traverses through a strict chain of responsibility:OS / Virtual Machine $\rightarrow$ Browser / Window Manager $\rightarrow$ Event Handler (Target Component)Events can propagate using two main approaches:
* Top-down (Event Capturing/Bubbling-down): The event starts at the top window level and trickles down to the specific component that was interacted with.
* Bottom-up (Event Bubbling): The target component handles the event first, then passes it up through parent containers to the top level.

### why use sliders 

because when the data is conitnuous in nature and needs testing to know waht fits the best
so you use it you slide you observe and choose so best

### dilogue box

forcing attention and don't wat the user to loose context and go away

why we use it ??
to get some input from the user in a specific format  in short modal pop-ups
like user name , password , etc

* Structured Input: Collect short, specific input (e.g., username, password, confirmation prompts) without altering the main interface layout.
* Modal Pop-ups: Block interaction with the rest of the app until closed, keeping the user focused on a critical task.

### scrollbar

Scrollbars allow users to navigate through content that exceeds the screen dimensions 
without cluttering the visible page. However, poorly styled or aggressively shifting scrollbars 
can act as a distraction, drawing focus away from the main interaction flow.

