# Web-Crawling-Project-

# README

This project is a Python-based application for crawling, storing, scheduling, and exposing book-related data via APIs. The source data comes from the website [Books to Scrape](https://books.toscrape.com/). The application includes the following functionalities:

1. *Data Crawling*: A Python crawler to scrape book information from the website.
2. *Database Integration*: Storing the scraped data in a MongoDB database.
3. *Scheduler*: A periodic scheduler to update the database with new or updated book information.
4. *APIs*: RESTful APIs for accessing the book data with features like filtering, sorting, and API key-based authentication.

---

## Prerequisites

1. *Python*: Ensure Python 3.8 or higher is installed.
2. *MongoDB*: Set up a MongoDB instance (local or cloud).
3. *Required Libraries*:
   - pymongo: For MongoDB interactions
   - requests: For HTTP requests
   - beautifulsoup4: For web scraping
   - fastapi: For creating APIs
   - uvicorn: For running the FastAPI application
   - apscheduler: For scheduling tasks
   - python-dotenv: For managing environment variables (optional but recommended)

Install the required libraries using pip:
bash
pip install pymongo requests beautifulsoup4 fastapi uvicorn apscheduler python-dotenv


---

## Directory Structure


book_crawler_project/
  |-- book_crawler.ipynb  # Main Jupyter Notebook file containing all the code
  |-- .env                # Optional file for storing environment variables (e.g., MongoDB URI, API Key)


---

## How to Run the Program

### Step 1: Set Up MongoDB

1. Configure your MongoDB database.
2. Note down the connection string (e.g., mongodb+srv://<username>:<password>@cluster_url).
3. If using an .env file, add the following:
   
   MONGO_URI=mongodb+srv://<username>:<password>@cluster_url
   

### Step 2: Run the Jupyter Notebook

1. Open the book_crawler.ipynb file in Jupyter Notebook or Jupyter Lab.
2. Execute the cells in sequence:
   - *Crawler*: Scrape all book information and store it in the MongoDB database.
   - *Scheduler*: Start the periodic task to update the database daily.
   - *APIs*: Define and start the FastAPI server for exposing APIs.

### Step 3: Start the API Server

1. Ensure the FastAPI server runs as part of the notebook.
2. Alternatively, convert the API-related cells into a standalone script and run it:
   bash
   uvicorn api:app --reload
   

### Step 4: Interact with the APIs

Use tools like curl, Postman, or a web browser to test the APIs.

#### API Endpoints

- *Book List API*:
  
  GET /books
  
  Query Parameters:
  - category: Filter by book category
  - min_price: Minimum price filter
  - max_price: Maximum price filter
  - sort_by: Sort by price, rating, etc.

  Example:
  bash
  curl -X GET "http://127.0.0.1:8000/books?category=Fiction&min_price=10&sort_by=rating" -H "X-API-KEY: your_api_key"
  

- *Book Details API*:
  
  GET /books/{book_name}
  
  Example:
  bash
  curl -X GET "http://127.0.0.1:8000/books/The-Great-Gatsby" -H "X-API-KEY: your_api_key"
  

---

## Scheduler Functionality

- The scheduler runs daily and:
  1. Checks if a new book is added to the website.
  2. Updates the database if any book details have changed.

---

## Notes

- Replace <username>, <password>, and cluster_url in the MongoDB URI with your credentials.
- Replace your_api_key with the actual API key defined in your code.
- Ensure the FastAPI server is running before making API requests.

---

## Troubleshooting

1. *MongoDB Connection Issues*:
   - Verify the connection string.
   - Ensure MongoDB is running.
2. *API Authentication Errors*:
   - Ensure the correct API key is passed in the X-API-KEY header.
3. *Scheduler Not Running*:
   - Check if the APScheduler service is initialized correctly.

---

## Future Enhancements

- Add more advanced filters and sorting options in the APIs.
- Implement pagination for the book list API.
- Enhance error handling and logging.
- Deploy the FastAPI application to a cloud platform (e.g., AWS, Heroku, or Azure).

---

## Credits

- Website: [Books to Scrape](https://books.toscrape.com/)
- Libraries: FastAPI, APScheduler, BeautifulSoup, pymongo, and others.
