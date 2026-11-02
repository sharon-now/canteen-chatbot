# Intent dataset: School Canteen Bot

Assignment 8, the first stage of Portfolio Project 2, Part 1.

## The labels

| Label | What it means | Messages |
|---|---|---|
| menu | The student asks what food or drinks the canteen sells or has available. | 33 |
| price | The student asks what an item costs. | 33 |
| order | The student wants to buy or order an item. | 34 |
| hours | The student asks when the canteen opens, closes or works. | 32 |
| status | The student asks if an order already placed is ready, or where it is. | 32 |
| human | The student asks for a person, staff or general help. | 30 |
| out_of_scope | Everything this chatbot does not answer: complaints, payment, delivery, small talk, greetings or goodbyes alone, gibberish. | 33 |

## The labelling guideline

1. One message, one label. A greeting plus a request is labelled by the request ('hi, how much is rice' is price).
2. Label the goal, not the words: 'how much for 2 chapati' is price, not order, because the student wants a cost.
3. Asking what food or drinks exist or are available is menu; asking what an item costs is price, even for 'price list'.
4. Wanting or buying an item, with or without a quantity, is order, even when 'help' or 'please' appears in the message.
5. Asking about an order that was already placed (is it ready, where is it) is status, not order.
6. Asking for a person, staff, the manager or a human is human; a general 'i need help' is also human.
7. Complaints, payment methods, small talk, a greeting or goodbye alone, other topics and gibberish are out_of_scope.
8. Keep the student's words: typos, SMS, Kinyarwanda and mixed language, exactly as typed.
9. Delivery questions (do you deliver, delivery fee) are out_of_scope: the canteen bot does not handle delivery.

## Where the messages come from

| Source | Rows |
|---|---|
| rules | 22 |
| unmatched | 2 |
| local | 39 |
| people | 15 |
| written | 149 |

## Quality check

```
Per source: {'rules': 22, 'local': 39, 'written': 149, 'unmatched': 2, 'people': 15}
people: 15 of at least 20
Labels not in INTENTS: []
Duplicates: []
Conflicting labels: []
Balance, largest / smallest: 1.13
```

## Split and baseline

185 training, 42 test. My Portfolio Project 1 rules get **24 of 42** test messages right. The messages they get wrong, for example:

- `mufunga saa ngahe?` (hours): the rules have no Kinyarwanda words for opening or closing, so the message falls to out_of_scope.
- `hi, is my food ready` (status): the rules say menu, because the word "food" is matched by the menu rule before the message can reach status.
- `is my rice ready` (status): none of the status words (where is my order, order status, is it ready) match, so it falls to out_of_scope.

## Entities

ITEM: rice, beans, chapati, chapatis, chips, juice, juices, umuceri, ibishyimbo, yoghurt. Found in 80 messages of the dataset.
DAY: monday, tuesday, wednesday, thursday, friday, saturday, sunday, today. Found in 13 messages of the dataset.

## What is still weak

- Only 15 messages come from real people, not the 20 required. The dataset leans on my own written phrasing.
- None of the real-people messages is for the human label, and none is in Kinyarwanda. Those labels rely on my own written and local phrasing.
- Some messages could be argued either way, such as 'help me pls' (human) and 'price list please' (price).
- Kinyarwanda coverage is small and was not reviewed line by line by a native speaker.
