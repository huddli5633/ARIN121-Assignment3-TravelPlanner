# ARIN121-Assignment3-TravelPlanner

An AI travel planning assistant built entirely from a system prompt and tested in the Google AI Studio Playground. It helps travellers plan a trip day by day, decide between destinations when they are unsure where to go, and answer quick travel questions about a destination.

This repository was created for ARIN 121, Assignment 3 (Extending and Versioning Your Travel Planner). It builds on the planner I designed in Assignment 2.

## Files

| File | What it contains |
| --- | --- |
| `system-prompt.md` | The complete system instructions for the travel planner. |
| `README.md` | This guide: what the planner does, how to use it, and its limitations. |

The original Assignment 2 prompt is preserved in the commit history on `main` in the commit **"Preserve Assignment 2 starting prompt"**. The menu and new activity were developed on the `conversational-features` branch and merged into `main` through a pull request.

## How to use the prompt

1. Open [Google AI Studio](https://aistudio.google.com/) and start a new chat in the Playground.
2. Copy the full contents of `system-prompt.md` into **System instructions**.
3. Send a message. You can start with a general greeting to see the menu, or ask for what you want directly.

Saving or merging a file in GitHub does not update a Playground prompt, so always paste the latest version from `main`.

## The menu

When your first message does not make clear what you want (for example, "Hi, I'm thinking about taking a trip"), the planner shows this menu:

1. **Plan a trip.** Builds a day-by-day itinerary at your pace, recommends a place to stay, and adds a daily cost table if you share a budget.
2. **Choose a destination.** Compares the places you are considering against what matters most to you and recommends the best fit. *(New in Assignment 3)*
3. **Ask a travel question.** Answers a quick question about local customs, transit, weather, or entry requirements.

You can choose an activity in three ways:

- Type its number, such as `2`.
- Type its name, such as `Choose a destination`.
- Describe what you want in your own words, such as "I can't decide between Lisbon and Barcelona."

If your first message already makes your request clear (for example, "Plan a 4-day trip to Montreal"), the planner skips the menu and starts that activity right away. You can type `menu` at any time to see the options again, or `start over` to clear your details and begin again.

## New activity: Choose a destination

This is a multi-turn activity for travellers who have narrowed their trip down to a few places but cannot decide between them.

1. **You share your options and priorities.** Name two to four destinations and up to three things that matter most to you, in order (for example, food, then cost, then nightlife). Details you have already given, such as trip length, dates, or budget, are reused rather than asked for again.
2. **The planner compares them.** It shows a table with one column per destination and one row per priority, plus an estimated daily cost row if you gave a budget and a "Watch out for" row. It then gives a provisional recommendation based on your top priority.
3. **It asks about the biggest trade-off.** The planner asks one follow-up question at a time (for example, "Barcelona fits your nightlife priority better, but Lisbon is cheaper. Which matters more to you?") and waits for your answer.
4. **Your answer refines the recommendation.** It updates only the parts of the comparison your answer affects, removes any destination you rule out, and tells you whether its recommendation stayed the same or changed.
5. **It finishes with a final recommendation.** Once you choose a destination, accept the recommendation, or after three follow-up questions, it gives the recommended destination, two reasons linked to your priorities, and one trade-off. It then offers to plan your trip there using the details you have already given.

You can stop the comparison at any time by saying so (for example, "Let's leave it there"). The planner will summarize where things stand and stop asking questions.

## Switching between activities

You can switch activities at any point by saying so in your own words, such as "Actually, can you help me decide whether Quebec City would be better?" The planner switches right away, lists the details it is carrying forward (destination, trip length, dates, budget, interests, pace, and priorities), and asks only for what the new activity still needs. If you correct a detail, it uses the corrected value from then on.

A quick question in the middle of an activity, such as "What's the weather like in Lisbon in May?", is treated as a side question. The planner answers it briefly and then returns to where you left off.

## Features carried over from Assignment 2

- **Ambiguous destinations.** If a place name could mean more than one location (for example, Kingston), the planner asks which one you mean before planning.
- **Pace control and targeted edits.** You choose a relaxed (up to 2 activities per day), moderate (up to 3), or packed (up to 5) pace. When you ask to change one day, only that day changes.
- **Accommodation suitability check.** The planner recommends one place to stay and avoids options with restrictions that do not apply to you, such as women-only or adults-only.
- **Itemized daily cost breakdown.** With a budget, you get a cost table with one row per day in both the local currency and your currency, and the remaining budget is reported honestly rather than padded.
- **Application boundaries.** Requests unrelated to travel are declined, and the planner shows the menu instead.

## Limitations

- The planner relies only on what the AI model already knows. Costs, weather, and travel times are typical estimates, not live data, and it cannot check availability or make bookings.
- Choose a destination compares at most four destinations and asks at most three follow-up questions before giving a final recommendation.
- The planner does not yet ask how many people are travelling, so budgets and accommodation assume a single traveller unless you say otherwise.
- Because the behaviour comes from a system prompt, results can vary between models and settings. The tests for this version were run in the Google AI Studio Playground.
