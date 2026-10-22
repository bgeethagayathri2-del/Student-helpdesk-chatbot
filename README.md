# Student Helpdesk Chatbot

An intent-based chatbot that answers common student questions about exams, fees, the library, hostel and placements, and replies "I did not understand" when it is not confident.

- **Method:** TF-IDF features (single words and two-word phrases) and Logistic Regression to classify each message into an intent, then reply with the answer for that intent
- **Training data:** 64 example questions across 8 intents (8 per intent), written by me
- **Results:**
  - Test accuracy: 0.938 (on only 16 test examples)
  - Cross-validation accuracy: 0.799 (the more reliable number)
- **Confidence threshold:** 0.3 (messages below this get a "did not understand" reply)
- **Demo results (8 test messages):**
  - 5 on-topic questions were answered correctly (greeting, library, hostel, exam schedule, thanks).
  - "what is the placement process" was wrongly rejected (confidence 0.28, just under the threshold).
  - "who won the cricket match" was correctly rejected (confidence 0.27).
  - "what is the weather today" was wrongly answered with the fees reply (confidence 0.36).
- **Conclusion:** The chatbot understands questions on its 8 topics well, but the small training set causes two kinds of mistakes: it can reject a valid question, and it can answer an off-topic question with a wrong intent. No single confidence threshold fixes both, because the correct and wrong cases have similar confidence scores.

## Future improvements
Add more varied example questions for each intent, and add an "out of scope" intent with off-topic examples so the bot learns what it should not answer.

## Limitations
The bot only knows the 8 topics it was trained on, and the answers are sample text (replace them with your college's real information). It selects from fixed answers, so it does not generate new sentences like ChatGPT.

## How to run
Open `Helpdesk_chatbot.ipynb` in Google Colab and click Run all.
