# news-fetcher

# Overview
This Python script uses the NewsAPI to fetch and display recent news articles based on a search query. It retrieves a list of articles, each with a title and a URL, and prints them to the console.

# Prerequisites
Python 3.x installed.
News API key: Sign up at NewsAPI to obtain a free API key.
newsapi-python Library: Install it with the following command:

pip install newsapi-python

# How It Works
Initialize the News API Client: The NewsApiClient is initialized with your API key.
Fetch News Articles: The fetch_news function queries NewsAPI for articles related to a specified keyword.
Display Results: The titles and URLs of articles are printed, making it easy to explore the latest articles on the topic.

#Code Structure
fetch_news Function
This function retrieves news articles based on a query, language, and number of results per page.

Parameters:
1. query (str): The search term or keyword (e.g., "technology").
2. language (str): Language code for the news articles, default is 'en' for English.
3. page_size (int): The number of articles to retrieve, default is 5.

Returns: A list of formatted strings containing each article's title and URL, or an error message if no articles are found or an error occurs.

# Example Code
from newsapi import NewsApiClient

# Initialize the News API client with your API key
newsapi = NewsApiClient(api_key='YOUR_API_KEY')

def fetch_news(query, language='en', page_size=5):
    try:
        # Fetch news articles
        response = newsapi.get_everything(q=query, language=language, page_size=page_size)

        # Check if articles are found
        if response['status'] == 'ok' and response['totalResults'] > 0:
            articles = response['articles']
            news_list = []

            # Process and print each article's title and link
            for article in articles:
                title = article['title']
                url = article['url']
                news_list.append(f"{title}\n{url}\n")

            return news_list
        else:
            return "No news articles found."

    except Exception as e:
        return f"An error occurred: {str(e)}"

# Fetch news based on a query
query = "technology"
news = fetch_news(query)
for item in news:
    print(item)
    
# Usage Instructions

1. Replace YOUR_API_KEY: Insert your NewsAPI key in the code where it says 'YOUR_API_KEY'.
2. Run the Script: Execute the script to fetch and display news articles on a specified topic.

#Sample Output

Enter a query: technology
Latest Technology News:
- AI Breakthrough in Medical Imaging
  https://example.com/article1

- Advances in Renewable Energy
  https://example.com/article2
  
# Notes
1. API Key Limits: The free API key has request limits. Avoid excessive requests to prevent reaching the rate limit.
2. Language and Query Customization: Customize query and language to retrieve different articles.
   
This script provides an efficient way to stay updated on current news in any field using Python.
