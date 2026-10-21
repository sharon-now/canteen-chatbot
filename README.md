# Canteen Chatbot

A rule-based chatbot for a school canteen, written in Python. It shows the menu, gives prices, takes orders with a confirmation step, gives opening hours, checks order status, and hands over to a person when it keeps missing.

Notebook: `week_7_canteen_chatbot.ipynb`

## How it works

- **Text normalizer**: lowercases, removes punctuation and extra spaces, so "Hello!!" and "hello" match the same way.
- **Rule table + router**: a list of (intent, pattern, handler) tried in order. The first match runs its handler function.
- **Intents (6)**: greeting, menu, price, order, opening hours, order status / human help.
- **Input variations**: patterns catch capitals, punctuation, plurals ("chapatis"), several phrasings, and local words (muraho, ndashaka, umuceri).
- **Fallback**: says what the bot can do, logs the unmatched message with a time, and offers a person after 2 misses in a row.
- **Closure**: "bye", "goodbye", "quit", "exit" work at any point. Orders need a yes/no confirmation before they are saved.

## Test plan, round 1 (written before running)

| # | You type | Expected reply |
|---|----------|----------------|
| 1 | Hello!! | Greeting message |
| 2 | muraho | Greeting message (local greeting) |
| 3 | what do you sell? | Menu list with prices |
| 4 | how much is chapati | Chapati costs 300 RWF |
| 5 | I want 2 chapatis and 1 juice | Order summary, total 1100 RWF, asks to confirm |
| 6 | (after test 5) yes | Order confirmed |
| 7 | when do you open? | Opening hours |
| 8 | where is my order | Says order is being prepared |
| 9 | asdfgh | Fallback message (not understood) |
| 10 | bye | Goodbye message |

Round 1 results: (FILL IN after you check your output: write "all 10 passed" or list any that failed)

## Test plan, round 2 (written before running)

| # | You type | Expected reply |
|---|----------|----------------|
| 11 | hi, how much is rice | Rice costs 1000 RWF. |
| 12 | Hello, I want 2 beans | Order summary: 2 x beans, total 1000 RWF, asks to confirm |
| 13 | what time do you stop selling? | Opening hours |
| 14 | can you help me order chips | Order summary: 1 x chips, total 800 RWF, asks to confirm |
| 15 | muraho, ndashaka umuceri | Understands the local phrasing |

## Bug log

### Bug 1: greeting hid the real question (tests 11 and 12)
- **What happened**: "hi, how much is rice" and "Hello, I want 2 beans" both got only the greeting.
- **Cause**: the greeting rule was first in the rule table, so any message containing "hi" or "hello" matched it before the price or order rule.
- **Fix**: moved the greeting rule to the end of the rule table.

### Bug 2: "stop selling" ended the chat (test 13)
- **What happened**: "what time do you stop selling?" got "Goodbye!" instead of opening hours.
- **Cause**: "stop" was in the exit pattern, so it matched inside a normal question.
- **Fix**: "stop" now exits only when it is the whole message. Added "time" to the opening hours pattern.

### Bug 3: local words not understood (test 15)
- **What happened**: "muraho, ndashaka umuceri" did not become an order.
- **Cause**: the bot did not know "ndashaka" (I want) or "umuceri" (rice).
- **Fix**: added "ndashaka" to the order pattern and a LOCAL_WORDS dictionary that maps local item names to menu items.

### Note on test 15 (test script flaw)
The first run of test 15 answered "Please answer yes or no" because the order from test 14 was still waiting for confirmation. The bot was correct. The test script did not reset the bot between tests. The re-run script now resets it before each test.

## Evidence of test-driven fix

| Test | Before the fix | After the fix |
|------|----------------|---------------|
| 11 | Greeting only | Rice costs 1000 RWF. |
| 12 | Greeting only | Order: 2 x beans, total 1000 RWF, confirm? |
| 13 | "Goodbye!" | The canteen is open Monday to Friday, 7:00 to 16:00. |
| 14 | Correct | Correct |
| 15 | "Please answer yes or no" | Order: 1 x rice, total 1000 RWF, confirm? |

After the fixes, round 1 was run again to check nothing broke: (FILL IN: "all 10 still passed" or list any that failed).

## How to run

Open the notebook in Google Colab and run all cells. Type `chat()` in a new cell to talk to the bot.
