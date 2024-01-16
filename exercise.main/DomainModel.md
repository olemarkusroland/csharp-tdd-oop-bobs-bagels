# Core
1. I'd like to add a specific type of bagel to my basket.
2. I'd like to remove a bagel from my basket.
3. I'd like to know when my basket is full when I try adding an item beyond my basket capacity.
4. I�d like to change the capacity of baskets.
5. I'd like to know if I try to remove an item that doesn't exist in my basket.
6. I'd like to know the total cost of items in my basket.
7. I'd like to know the cost of a bagel before I add it to my basket.
8. I'd like to be able to choose fillings for my bagel.
9. I'd like to know the cost of each filling before I add it to my bagel order.
10. I want customers to only be able to order things that we stock in our inventory.
 
## Core Class
| Class | properties |
|---|---|
| BagelVariant | `string Name`, `double Price` |
| BagelFilling | `string Name`, `double Price` |
| CoffeeVariant | `string Name`, `double Price` |
| Bagel | `BagelVariant Variant`, ` List<BagelFilling> Fillings` |
| Coffee | `CoffeeVariant Variant` |
| Basket | `List<Bagel> Bagels`, `List<Coffee> Coffees`, `int Capacity` |


| User story | Class| Method | Scenario | Output |
|---|---|---|---|---|
| 1 | Basket | `Add(Bagel bagel)`, `Add(Coffee coffee)` | `Basket` is not full | Adds product to `Basket.Bagels`|
| 3 | Basket |                    | `Basket` is full    | Displays `"Basket is full"`|
| 2 | Basket | `Remove(Bagel bagel)`, `Remove(Coffee coffee)` | Product exists in `Basket`       | Removes|
| 5 | Basket |                      | Product does not exist in `Basket` | Displays `$"{product} was not found in basket"`|
| 4 | Basket | `ChangeCapacity(int capacity)` |  | Sets `Basket.Capacity` to `capacity`|
| 6 | Basket | `double Cost()` |  | Returns total cost of products in `Basket` |
| 7 | Bagel | `double Cost()` |  | Returns total `Price` of `Variant` + all `BagelFilling`s |
| 8 | Bagel | `AddFilling(BagelFilling filling)` |  | Adds `filling` to `Fillings`|
| 9 | BagelFilling | `IEnumerable<BagelFilling> GetAll()` |  | Returns all the `Filling`s |


## Bob's Inventory
| SKU  | Price | Name   | Variant       |
|------|-------|--------|---------------|
| BGLO | 0.49  | Bagel  | Onion         |
| BGLP | 0.39  | Bagel  | Plain         |
| BGLE | 0.49  | Bagel  | Everything    |
| BGLS | 0.49  | Bagel  | Sesame        |
| COFB | 0.99  | Coffee | Black         |
| COFW | 1.19  | Coffee | White         |
| COFC | 1.29  | Coffee | Cappuccino    |
| COFL | 1.29  | Coffee | Latte         |
| FILB | 0.12  | Filling| Bacon         |
| FILE | 0.12  | Filling| Egg           |
| FILC | 0.12  | Filling| Cheese        |
| FILX | 0.12  | Filling| Cream Cheese  |
| FILS | 0.12  | Filling| Smoked Salmon |
| FILH | 0.12  | Filling| Ham           |

# Extension 1
1. Products are identified using Stock Keeping Units, or SKUs.

To acheive this I will create a new class `BobsBagels` that will abstract the current class `Core`. 

2. Some items are multi-priced.

| SKU  | Name    | Variant     | Price | Special Offers    |
|------|---------|-------------|-------|-------------------|
| BGLO | Bagel   | Onion       | 0.49  | 6 for 2.49        |
| BGLP | Bagel   | Plain       | 0.39  | 12 for 3.99       |
| BGLE | Bagel   | Everything  | 0.49  | 6 for 2.49        |
| COFB | Coffee  | Black       | 0.99  | Coffee & Bagel for 1.25 |


## BobsBagels class
| User story | Method | Scenario | Output |
|---|---|---|---|
| 1 | `Add(string sku)` | `Basket` is not full | Adds product to `Basket.Bagels`|
| 3 |                   | `Basket` is full     | Displays `"Basket is full"`|
| 2 | `Remove(string sku)` | product exists in `Basket`         | Removes product from `Basket.Product`|
| 5 |                      | product does not exist in `Basket` | Displays `$"{product} was not found in basket"`|
| 4 | `ChangeCapacity(int capacity)` |  | Sets `Basket.Capacity` to `capacity`|
| 6 | `double Cost()` |  | Returns total cost of products in basket |
| 7 | `double Cost()` |  | Returns total `Price` of `Variant` + all `BagelFilling`s |
| 8 | `AddFilling(BagelFilling filling)` |  | Adds `filling` to `Fillings`|
| 9 | `IEnumerable<BagelFilling> GetAll()` |  | Returns all the `Filling`s |