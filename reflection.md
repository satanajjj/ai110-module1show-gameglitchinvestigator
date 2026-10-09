# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").
  There were multiple things that were broken when I first ran the game.
One bug was that, when looking at the hints, the hints were reversed. In other words, if the guess was too low, the hint would say to go lower, and if the guess was too high, the hint would say to go higher. This is opposite from the expected behavior of the hint, as the player would only make guesses further away from the answer.
Another bug that was present is that the New Game button does not reset the game if the game is already finished. When the game finishes, it does not allow any new guesses to be checked. When pressing the "New Game" button, the user would expect to be able to input new attempts, but the program does not accept any new inputs as guesses towards the secret.
A final bug that was noticed is that the difficulty selector names are not representative of the actual difficulty, as the user would expect Hard to have a larger number range than Normal, which is not the case as Hard has a range of 1 to 20 and Normal has a range of 1 to 100.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
ChatGPT and Claude
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
One AI suggestion that was correct was helping me move check_guess from app.py into logic_utils.py and fix the reversed hint bug. The AI pointed out that the hints were backwards, so when a guess was too high it should say “Go LOWER,” and when a guess was too low it should say “Go HIGHER.” I verified that by running the app in Streamlit and testing both high and low guesses. I also ran python3 -m pytest and confirmed the tests passed.
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).
One AI suggestion that was misleading was a pytest for the New Game reset bug. The AI suggested making a regular dictionary, changing values like status to "playing", and then asserting that the value changed. That did not really test the actual Streamlit app or st.session_state, so it was not a strong test for the real bug. I verified that by reading the test carefully and noticing it was not connected to the real game flow. Instead, I checked the fix by running the app, finishing a game, clicking “New Game,” and making sure the app accepted guesses again.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?
I decided a bug was really fixed by checking it in more than one way. First, I ran the Streamlit app and tested the behavior directly in the browser to make sure the game actually worked the way a player would expect. Then I used python3 -m pytest to confirm the logic changes also passed automated tests. For example, after fixing the reversed hint bug, I manually tested guesses that were too high and too low and confirmed the app gave the correct “Go LOWER” and “Go HIGHER” messages. I also ran pytest and used tests that checked the check_guess function returned the correct outcome and hint message. AI helped me design and understand some of the tests by suggesting test cases for the hint logic and helping update older tests after check_guess was refactored to return both an outcome and a message. At the same time, I had to review the AI’s test suggestions carefully, because one proposed test for the New Game reset bug was misleading and did not really test the actual Streamlit behavior.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?
In the original app, the secret number kept changing because Streamlit reruns the whole script every time the user interacts with the app, like when clicking a button or entering a guess. Since the secret number was being generated during those reruns, a new random number could get created again instead of keeping the same one for the whole round. I would explain Streamlit reruns to a friend by saying that Streamlit basically refreshes your Python script from top to bottom every time something happens in the app. Session state is what lets you keep important values, like the secret number, attempts, or game status, from getting reset every time that rerun happens. The change that finally gave the game a stable secret number was storing it in st.session_state so it stayed the same across reruns until the player started a new game.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.
One habit I want to reuse in future labs is fixing one bug at a time and testing after each change instead of trying to fix everything at once. That made it a lot easier to understand what each change was doing and to catch problems early. Next time I work with AI on a coding task, I would be even more specific with my prompts from the start and keep the scope narrow so the AI does not try to refactor too much at once. This project changed the way I think about AI-generated code because it showed me that AI can be really helpful for debugging and brainstorming, but I still need to review everything carefully, test it myself, and decide whether the suggestion actually makes sense.
