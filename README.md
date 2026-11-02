# AI Shopping Assistant

A conversational shopping assistant prototype inspired by Amazon Rufus. Describe what you are looking for, and the assistant searches a local product catalog, checks customer ratings, and helps you compare products. You can also upload a product photo to find similar catalog items.

> **Prototype notice:** This project uses sample data and a simulated checkout. It does not process payments, reserve inventory, or arrange delivery.

## Features

- Search products with natural-language preferences such as product type, maximum price, and organic status.
- Retrieve average customer ratings and review counts from the local database.
- Upload a product image for AI-based attribute extraction and catalog search.
- Confirm a product choice to create a demo order record.
- Interact through a Streamlit chat interface.

## Tech stack

- Python and Streamlit
- LangChain agents and tools
- Groq-hosted language and vision models
- SQLite for products, reviews, and demo orders

## Requirements

- Python 3.10 or newer
- A Groq API key with access to the configured models
- Internet access for model requests

## Setup

1. Clone or download this project and open a terminal in its directory.
2. Create and activate a virtual environment:

   ```powershell
   python -m venv .venv
   .venv\Scripts\Activate.ps1
   ```

3. Install the dependencies:

   ```powershell
   python -m pip install streamlit langchain langchain-groq python-dotenv
   ```

4. Create a `.env` file in the project root and add your API key:

   ```text
   GROQ_API_KEY=your_groq_api_key
   ```

   Keep this key private and do not commit `.env` to source control.

5. Initialize or refresh the sample catalog and reviews:

   ```powershell
   python setup_db.py
   ```

6. Start the app:

   ```powershell
   streamlit run app.py
   ```

Streamlit will print a local URL (usually `http://localhost:8501`) to open in your browser.

## Example requests

- “Find organic honey under $20 with a rating of at least 4.5.”
- “Show me oats under $8.”
- Upload a product photo and choose **Find similar products**.
- After reviewing the results, explicitly confirm if you want to create a demo order.

## Project structure

| File or directory | Purpose |
| --- | --- |
| `app.py` | Streamlit chat interface and image-upload workflow |
| `shopping_agent.py` | Language and vision models, agent instructions, and shopping tools |
| `reviews_api.py` | Queries product rating and review-count aggregates |
| `setup_db.py` | Creates the SQLite tables and loads sample products and reviews |
| `store.db` | Local SQLite database used by the app |
| `resources/` | Sample product images |

The database contains a small, pre-populated catalog. Running `setup_db.py` inserts or updates the sample products and replaces the sample reviews; it does not connect to a live retailer.

## Limitations

- Orders are only written to the local `orders` table. There is no payment, inventory, fulfillment, or shipping integration.
- Product and review data are sample data.
- The app requires a working Groq API key and network access to the configured models.
- This is a demo, not a production-ready commerce application. Do not use it to handle real customer accounts, payments, or personal data without adding the necessary security, privacy, reliability, and operational controls.
