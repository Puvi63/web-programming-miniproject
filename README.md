# Page & Paper: E-Book Sales and Preview Page

A responsive, multi-page online bookstore built for a Web Programming college project. Visitors can browse e-books, search and filter the collection, read a free sample chapter, and manage a shopping cart that remembers its contents between pages. "Page & Paper" is a fictional brand and all books, authors and excerpts are original.

## Objectives

- Build a complete, multi-page website using only HTML, CSS, Bootstrap 5 and vanilla JavaScript.
- Practise responsive layout with the Bootstrap grid, navbar, cards, forms and utilities.
- Practise DOM manipulation, event handling and form validation in JavaScript.
- Use `localStorage` to keep data between page loads without a backend.
- Present a clean, professional design with accessible markup.

## Technologies used

- HTML5 (semantic elements)
- CSS3 (custom properties, flexbox, grid helpers)
- Bootstrap 5.3 (loaded from the jsDelivr CDN)
- Vanilla JavaScript (ES6+)
- Google Fonts: Playfair Display, Inter and Lora (loaded from the CDN, with system-font fallbacks)

No frameworks, build tools, server code or database are used.

## Features

- Home page with hero, featured book, best sellers, popular categories and a promotional section
- Explore page with live search by title or author and category filter buttons
- Book details page that shows the correct book from a `?id=` query parameter
- Free-sample preview page with a distinct excerpt for every book, a comfortable reading column and text size controls
- Shopping cart with quantity controls, remove buttons, subtotal and total, and an empty-cart message
- Cart saved in `localStorage` and a live item count in the navigation bar
- Contact form with built-in validation and a demonstration success message
- Toast notifications for add-to-cart and remove actions
- Responsive layout with a mobile menu, a skip link, labelled controls, alt text and visible keyboard focus

## Folder structure

```
ebook-store/
├── index.html          Home
├── books.html          Explore Books
├── book-details.html   Book Details
├── preview.html        Free Sample Preview
├── cart.html           Shopping Cart
├── contact.html        About and Contact
├── css/
│   └── style.css       All custom styles
├── js/
│   └── script.js       All JavaScript (data, cart, pages)
├── images/
│   ├── README.md       Notes about the cover images
│   └── cover-1.svg ... cover-8.svg
└── README.md
```

## How to run

1. Download or copy the whole `ebook-store` folder, keeping the folder structure intact.
2. Open `index.html` in a modern web browser (double-click it, or right-click and choose Open With).
3. Use the navigation bar to move between pages.

No installation or server is needed. An internet connection is required once so the browser can load Bootstrap and the fonts from their CDNs; if the fonts cannot load, the site falls back to standard system fonts.

## How the main interactions work

**Shared layout.** `script.js` builds the navbar and footer in one place and inserts them into `<div id="site-header">` and `<div id="site-footer">` on every page, so the navigation is identical everywhere. Each page's `<body>` has a `data-page` attribute (for example `data-page="cart"`) that tells the script which page-specific function to run.

**Book data.** All books are stored in a single `BOOKS` array at the top of `script.js`. Every page reads from it, so adding a new book there makes it appear in the grid, the details page and the preview page.

**Search and filtering.** On the Explore page, typing in the search box or clicking a category button calls `applyFilters()`. It keeps only the books whose title or author contains the search text and whose category matches the active button, then redraws the grid. The home page category tiles link to `books.html?category=...`, which pre-selects a filter.

**Details and preview.** Book cards link to `book-details.html?id=3` (the number is the book's id). The page reads the id with `URLSearchParams`, finds the matching book and fills in the page. The preview page works the same way using `preview.html?id=3`.

**Cart.** The cart is an array of `{ id, quantity }` objects saved in `localStorage` under the key `pagePaperCart`. Adding a book either creates an entry or increases its quantity (up to 10). The cart page redraws its rows and totals from the saved data after every change, and prices are looked up from `BOOKS` so the totals are always calculated, never stored. The navbar badge is updated whenever the cart is saved.

**Contact form.** The form uses HTML validation attributes (`required`, `type="email"`, `minlength`). On submit, JavaScript checks `form.checkValidity()`. Invalid forms show Bootstrap's error messages; a valid form shows a success message and resets. Nothing is sent anywhere.

## Limitations

- This is a front-end demonstration: there is no backend, user accounts or real payment. The checkout button only shows a demonstration message.
- The cart is stored in the browser's `localStorage`, so it is specific to one browser on one device and is cleared if the user clears site data.
- Only sample excerpts are provided; there is no real e-book download or reader.
- Book data is hard-coded in `script.js` rather than loaded from a database.
- Bootstrap and the web fonts come from CDNs, so a first load needs an internet connection.
- The shared header and footer are inserted by JavaScript, so they will not appear if JavaScript is disabled.
