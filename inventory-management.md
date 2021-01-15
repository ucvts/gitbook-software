# Inventory Management

## Summary

Now that we've gotten our feet wet with web applications and database, it's time to branch out on your own a bit. Imagine you're a freelance developer who has been tasked with crafting an inventory management for a business of your choosing. Your job is to plan, design, build, and test the application for commercial use!

## Requirements

Your application will need to behave similarly to the [UCVTS Library](ucvts-library.md), so dive back into that code if you need help getting started or run into issues. At a minimum, it needs to handle the following business use cases.

* Employees should be able to view all products available in the store. This may differ based on the type of business you've chosen, but should at least include a unique product ID, name, description, unit price \(i.e., the cost of a single unit\), and quantity.
* Employees should be able to add, remove, and modify products. In general, all product fields should be editable, with the exception of the product ID. Your business might have others that aren't intended to be modified, but you should be prepared to defend your choices here.
* Employees should be able to search for a product by ID, name, and unit price \(exact matches is the minimum requirement, meaning you won't be penalized if your search feature doesn't detect partial matches\). Employees should select the field on which they're searching, rather than searching across all possible fields. Capitalization shouldn't matter.

## Nice-to-Haves

In software, a nice-to-have is something that isn't requirement to go to market, but would be...nice to have! Consider these extra credit for the assignment, but only if done well. Poorly implemented nice-to-haves can negatively impact an application \(and your grade!\).

* Partial search functionality by ID, name, and description. For example, if I select `Name` type `red`, then I should get all products with those characters in the name \(e.g., `Red Shoes`, `Credit Card Processing Machine`, etc.\).
* Filter functionality by unit price and quantity. For example, if I select `Quantity`, choose `Less Than`, and type `10`, I should get back all products whose quantities are currently less than 10.

## Deliverables

1. Submit your repository URL.
2. Submit a video demo for the application + optional extra credit \(between 3 and 5 minutes\).

## Deadline

All submissions are due on Canvas by 11:59pm on Sunday, January 31, 2021.

