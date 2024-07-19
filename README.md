# JS Image Search Engine

This project is a simple image search engine built with JavaScript that interacts with the Unsplash API to fetch and display images based on user input. The app includes a search form and a "Show more" button to load additional images [TRY NOW!](https://qyuzet.github.io/js-search-engine).

![image](https://github.com/user-attachments/assets/edf99632-3c64-4939-92a4-a0ff9e238b00)


## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
  - [JavaScript](#javascript)
- [Contributing](#contributing)
- [License](#license)

## Features
- Search for images using keywords
- Display images in a grid layout
- Load more images with the "Show more" button

## Installation
1. Clone the repository:
    ```bash
    git clone https://github.com/Qyuzet/js-search-engine.git
    ```
2. Navigate to the project directory:
    ```bash
    cd js-search-engine
    ```
3. Open `index.html` in your browser.

## Usage
1. Enter a keyword in the search box and click "Search".
2. The results will be displayed in a grid.
3. Click "Show more" to load additional images.

## Code Explanation

### JavaScript
The JavaScript code handles fetching images from the Unsplash API and updating the DOM.
```javascript
// Store the Unsplash API access key
const accessKey = "u473YlVLlbY6x1lAeSphSzsBtbrw37fhrIDU3w6H2SI";

// Get references to HTML elements
const searchForm = document.getElementById("search-form");
const searchBox = document.getElementById("search-box");
const searchResult = document.getElementById("search-result");
const showMoreBtn = document.getElementById("show-more-btn");

let keyword = "";
let page = 1;

// Function to search images from Unsplash API
async function searchImages() {
  keyword = searchBox.value;
  const url = `https://api.unsplash.com/search/photos?page=${page}&query=${keyword}&client_id=${accessKey}&per_page=12`;

  const response = await fetch(url);
  const data = await response.json();

  if (page === 1) {
    searchResult.innerHTML = "";
  }

  const results = data.results;

  // Create and append image elements to the search result
  results.map((result) => {
    const image = document.createElement("img");
    image.src = result.urls.small;
    const imageLink = document.createElement("a");
    imageLink.href = result.links.html;
    imageLink.target = "_blank";

    imageLink.appendChild(image);
    searchResult.appendChild(imageLink);
  });
  showMoreBtn.style.display = "block";
}

// Event listener for search form submission
searchForm.addEventListener("submit", (e) => {
  e.preventDefault();
  page = 1;
  searchImages();
});

// Event listener for "Show more" button click
showMoreBtn.addEventListener("click", () => {
  page++;
  searchImages();
});
```



## Contributing
1. Fork the repository.
2. Create your feature branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a pull request.

## License
This project is licensed under the MIT License.
