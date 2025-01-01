---
icon: file-code
---

# HTMX



## HTMX Tutorial for Beginners

HTMX is a lightweight JavaScript library that allows you to create dynamic, interactive web applications without writing much JavaScript. With HTMX, you can add interactivity to your HTML by utilizing attributes that leverage AJAX, WebSockets, and more. This tutorial will guide you through the basics of HTMX with examples to get you started.

***

## 1. Setting Up HTMX

To use HTMX, include the library in your HTML file by adding the following script tag:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTMX Tutorial</title>
    <script src="https://unpkg.com/htmx.org"></script>
</head>
<body>
    <!-- Your content here -->
</body>
</html>
```

That's it! HTMX is now ready to use.

***

## 2. Basic HTMX Attributes

HTMX uses specific attributes to define interactions. Here are the most common ones:

* `hx-get`: Sends a GET request to a specified URL.
* `hx-post`: Sends a POST request to a specified URL.
* `hx-trigger`: Defines the event that triggers the request (e.g., `click`, `load`).
* `hx-target`: Specifies the element where the server's response will be injected.
* `hx-swap`: Controls how the response is swapped into the target element.
* `hx-indicator`: Specifies an element to show while a request is in progress.

***

## 3. Example 1: Fetching Content

Here’s how to use HTMX to fetch and display content dynamically:

### HTML:

```html
<div id="content">
    <button hx-get="/get-message" hx-target="#content" hx-swap="innerHTML">Get Message</button>
</div>
```

### Server Response (at `/get-message`):

```html
<p>Hello, HTMX!</p>
```

When the button is clicked, HTMX sends a GET request to `/get-message` and replaces the content of the `#content` div with the server's response.

***

## 4. Example 2: Form Submission

You can use HTMX to submit forms without a full page reload.

### HTML:

```html
<div id="result"></div>
<form hx-post="/submit-form" hx-target="#result" hx-swap="innerHTML">
    <input type="text" name="username" placeholder="Enter your name">
    <button type="submit">Submit</button>
</form>
```

### Server Response (at `/submit-form`):

```html
<p>Thank you, John!</p>
```

When the form is submitted, HTMX sends the form data to `/submit-form`, and the server's response is injected into the `#result` div.

***

## 5. Example 3: Infinite Scrolling

HTMX makes implementing infinite scrolling straightforward:

### HTML:

```html
<div id="items">
    <!-- Initial items here -->
</div>
<button hx-get="/load-more-items" hx-target="#items" hx-swap="beforeend">Load More</button>
```

### Server Response (at `/load-more-items`):

```html
<div class="item">New Item 1</div>
<div class="item">New Item 2</div>
```

Clicking the "Load More" button appends new items to the `#items` div without reloading the page.

***

## 6. Example 4: Loading Indicator

The `hx-indicator` attribute allows you to show an element while a request is in progress.

### HTML:

```html
<div id="loading-indicator" style="display: none;">Loading...</div>
<div id="content">
    <button hx-get="/get-data" hx-target="#content" hx-swap="innerHTML" hx-indicator="#loading-indicator">Fetch Data</button>
</div>
```

In this example, the `#loading-indicator` div will be shown while the request is being processed and hidden when it completes.

### Server Response (at `/get-data`):

```html
<p>Data loaded successfully!</p>
```

***

## 7. Example 5: Live Updates with WebSockets

HTMX can also handle real-time updates using WebSockets.

### HTML:

```html
<div id="updates" hx-swap-oob="true">
    <!-- Updates will appear here -->
</div>

<script>
    const socket = new WebSocket('ws://example.com/live-updates');
    socket.onmessage = function(event) {
        const update = event.data;
        document.getElementById('updates').innerHTML += update;
    };
</script>
```

The `hx-swap-oob` attribute ensures the content is swapped out of band, even if it's not within a specified target.

***

## 8. Advanced Features

* **`hx-boost`**: Enhance regular links and forms to use AJAX automatically.
* **`hx-push-url`**: Update the browser’s URL when performing actions, enabling better navigation.
* **`hx-headers`**: Add custom headers to requests.

### Example:

```html
<button hx-get="/data" hx-headers='{"Authorization": "Bearer TOKEN"}'>Fetch Data</button>
```

***

## 9. Debugging HTMX

To debug HTMX requests, add the following to your page:

```html
<script>
    htmx.logAll();
</script>
```

This will log all HTMX events to the console, making it easier to debug.

***

## 10. Wrapping Up

HTMX is a powerful tool for building interactive web applications with minimal JavaScript. By focusing on HTML and server responses, you can create dynamic experiences that are simple to maintain. Try incorporating HTMX into your projects and see how it streamlines your development process!
