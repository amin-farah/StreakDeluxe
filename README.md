# Streak Extension

## How to Download and Install

### Step-by-Step Installation
1. Download and extract the zip file `streakdeluxe`.
2. Go to your Chrome extensions and click **Manage Extensions**.
3. Turn on **Developer Mode**.
4. Click **Load Unpacked** and load the unzipped folder.

## Inspiration
Studying happens on the internet a lot of the time nowadays. But even when you're on webpages related to the topic you want to study, work, or just focus on—it’s still quite easy to get distracted.  
That's why we wanted to make productivity more interesting and make it feel more rewarding.

## What it Does
**Streak** is a Chrome extension that aids in student productivity by displaying a combo meter that gradually increases as long as the student remains on a Chrome tab relevant to their desired study subject.  
When they get side-tracked, they lose their combo rapidly.

The combo meter incentivizes productivity in the following ways:
- Illustrates if a tab is relevant.
- Gamification, referencing many games.
- Psychological: The more points you have, the faster they can be lost. Since gaining points is harder than losing them, it helps users stay focused on tabs related to their topic.

## How it was Built
- **Layout:** HTML and CSS.
- **Logic:** Vanilla JavaScript.
- **Integration:** Chrome API and Cohere AI API, requiring additional JavaScript and JSON.

### Features and How They Work:
- **Subject lock-in:**  
  Chrome extensions reset every page refresh. We save the topic chosen by the user by using an event handler in JavaScript and saving it into the user's local session via the Chrome API.

- **Retrieving current tab information:**  
  Chrome API is used to retrieve the title of the tab by adding `currentTab` to JSON permissions.

- **Determine relevance:**  
  Relevance is determined using the Cohere AI API. The current tab title and locked-in subject are sent through a trimmed AI prompt to return a simple "Yes" or "No" regarding relevance, with high accuracy (above 95%).

- **Hide and show GIF:**  
  Based on relevance, an angry or happy GIF is toggled using a "hide" CSS class.

- **Combo:**  
  - Increases by multiplying by ~1.2 and applying a power function every 2 seconds if relevant.
  - Decreases by dividing by 1.5 every 2 seconds if irrelevant.

- **Save combo:**  
  Saved similarly to the subject lock-in process.

- **Productivity bar:**  
  - Two CSS bars: a green one grows within a maximum value of 300px.
  - Gradual increase in width when being productive.
  - Upon reaching 100%, a combo boost is triggered.
  - Progress resets if you switch tabs.

## Challenges
- APIs were recently updated, requiring manual documentation checks.
- Could not complete the original idea of injecting HTML directly into current webpages within one day.
- Had to use Chrome session storage because local variables wouldn’t persist properly.
- Trial and error to find reasonable combo increase/decrease formulas.
- Formatting the extension to be appropriately sized.
- Fixing the bar width so it doesn't change the entire extension size.
- Optimizing the AI prompt for speed.

## Examples

**Example 1:**  
Being on a pasta recipes page while the input topic is "Gluten Free Recipes":  
> As we can see, the LLM's response indicates that gluten-free recipes and pasta recipes are not correlated (since pasta is not gluten-free), and the combo meter goes down.

**Example 2:**  
Inputting the topic "Proof by Induction" and searching for an introductory calculus YouTube video:  
> Since proof by induction is not a calculus topic, the LLM indicates no correlation, and the combo meter goes down.

**Example 3:**  
Keeping the topic "Proof by Induction" but switching to an introductory discrete mathematics YouTube video:  
> The LLM indicates correlation since proof by induction is part of discrete mathematics, so the combo meter stays up.

## What's Next for Streak
- Inject the extension into every website that is opened (local injection).
- Make it faster so that it doesn't require reloading and reopening after every new page or refresh.

These improvements are crucial to making Streak as practical and seamless as originally envisioned. Hopefully, they will be accomplished soon!
