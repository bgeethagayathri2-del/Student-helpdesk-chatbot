# Improvement: more examples + an "out_of_scope" intent
intents["placements"]["patterns"] += [
    "how do placements work", "what is the procedure for campus placements",
    "how are students placed in companies", "placement eligibility criteria",
    "how can i get a job through college", "which companies come for recruitment"]
intents["exam_schedule"]["patterns"] += [
    "when are the end semester exams", "when do internal exams begin",
    "what is the exam pattern timing", "exam time table release date"]
intents["thanks"]["patterns"] += [
    "thanks for the help", "okay thank you", "cheers thanks", "that helps thank you"]
intents["out_of_scope"] = {
    "patterns": ["what is the temperature outside", "will it rain tomorrow",
                 "who is the prime minister", "tell me a joke",
                 "what is the score of the match", "recommend a good movie",
                 "what is the capital of france", "how is the traffic today",
                 "what should i eat for dinner", "play some music"],
    "response": "Sorry, I can only help with exams, fees, the library, hostel and placements."}

rows = [(p, i) for i, d in intents.items() for p in d["patterns"]]
df = pd.DataFrame(rows, columns=["text", "intent"])
print("Total training examples:", len(df))

X_train, X_test, y_train, y_test = train_test_split(
    df["text"], df["intent"], test_size=0.25, random_state=42, stratify=df["intent"])
model.fit(X_train, y_train)
print("Test accuracy:", round(accuracy_score(y_test, model.predict(X_test)), 3))
print("Cross-validation accuracy:",
      round(cross_val_score(model, df["text"], df["intent"], cv=5).mean(), 3))

model.fit(df["text"], df["intent"])   # final model uses all examples

for msg in tests:
    reply, intent, conf = chatbot(msg)
    print(f"You: {msg}")
    print(f"Bot: {reply}")
    print(f"     [intent: {intent}, confidence: {conf:.2f}]\n")
