# Assignment 8 – Build Your Intent Dataset
**The first stage of Portfolio Project 2, Part 1.**

## The labels

| **Label** | **What it means** | **Messages** |
|---|---|---:|
| menu | The student asks what food or drinks the canteen sells or has available. | 34 |
| price | The student asks what an item costs. | 34 |
| order | The student wants to buy or order an item. | 35 |
| hours | The student asks when the canteen opens, closes or works. | 33 |
| status | The student asks if an order already placed is ready, or where it is. | 33 |
| human | The student asks for a person, staff or general help. | 30 |
| out_of_scope | Everything this chatbot does not answer: complaints, payment, delivery, small talk, greetings or goodbyes alone, and unrelated topics. | 33 |

## The labelling guideline

1. One message, one label. A greeting plus a request is labelled by the request ('hi, how much is rice' is price).
2. Label the goal, not just the words: 'how much for 2 chapati' is price, not order, because the student wants a cost.
3. Asking what food or drinks exist or are available is menu; asking what an item costs is price.
4. Wanting or buying an item, with or without a quantity, is order.
5. Asking about an order that was already placed (is it ready, where is it) is status, not order.
6. Asking for a person, staff, the manager or a human is human; a general request for help is also human.
7. Complaints, payment methods, small talk, greetings or goodbyes alone, and unrelated topics are out_of_scope.
8. Keep the student's words: typos, SMS, Kinyarwanda and mixed language, exactly as typed.
9. Delivery questions are out_of_scope because the canteen bot does not handle delivery.

## Where the messages come from

| **Source** | **Rows** |
|---|---:|
| rules | 22 |
| local | 39 |
| written | 150 |
| unmatched | 2 |
| people | 19 |

## Quality check

The dataset contains 232 messages across seven intent categories.

- Labels not in INTENTS: None reported.
- Duplicates: Not reported.
- Conflicting labels: Not reported.
- The dataset includes English, Kinyarwanda, mixed language and informal messages.

## Split and baseline

189 training messages and 43 test messages.

The rule-based baseline was evaluated using the test messages. The notebook's baseline results should be used to report the exact number of correctly classified messages and accuracy.

## Entities

**ITEM:** Food and drink names such as rice, beans, chapati, chips, juice and yoghurt.

**DAY:** Days of the week and today.

These entities help identify important information in students' messages.

## What is still weak

- Some intent categories may need more real-life examples from students.
- The dataset includes different ways of writing, but more Kinyarwanda and mixed-language examples would improve language coverage.
- Some messages may be difficult to classify because they contain more than one possible meaning.
- The baseline is rule-based, so it may fail to understand messages that use words or expressions that are not included in its rules.
