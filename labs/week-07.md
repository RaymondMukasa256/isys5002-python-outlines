# ISYS5002 - Week 7

## Key Concepts

- **Dictionaries:** A data structure that stores key-value pairs, allowing for efficient data retrieval and manipulation.
- **Dictionary Operations:** Common operations like adding, modifying, and accessing elements in a dictionary.
- **Dictionary Methods:** Useful built-in methods for working with dictionaries, such as `get()`, `keys()`, `values()`, and `items()`.
- **Data Representation:** Choosing appropriate data structures (like dictionaries) to effectively model and represent business data.
- **Data Analysis:** Techniques for extracting insights, identifying patterns, and drawing conclusions from business data stored in dictionaries.

## Activity: Conceptual Application & Analysis

Here's an example of a **dictionary** in Python:

```python
{"name": "Widget A", "price": 9.99, "qty_sold": 120}
```

It's like a list, but:

- The syntax (of course)
- Each "item" is labelled (key &rarr; value)
- It's quite normal for items to be of different data types

You've been tasked with analysing sales data for a small retail business. The data is stored in a dictionary, where the keys represent product IDs and the values are dictionaries containing information about each product, such as its name, price, and quantity sold.

```python
sales_data = {
    "P001": {"name": "Widget A", "price": 9.99, "qty_sold": 120},
    "P002": {"name": "Widget B", "price": 14.50, "qty_sold": 85},
    "P003": {"name": "Widget C", "price": 7.25, "qty_sold": 200},
    "P004": {"name": "Widget D", "price": 12.75, "qty_sold": 75}
}
```

## Two challenges

1. Explain how you would use dictionary operations and methods to **programmatically** calculate the total revenue generated from the sales data. Describe the step-by-step process, including any potential challenges or considerations.

2. The business owner wants to identify the best-selling product. Describe how you would use dictionary operations and methods to **programatically** determine the product with the highest quantity sold, and explain your reasoning.
