# Rule-Based Chatbot

def chatbot_response(user_input):
    user_input = user_input.lower()

    # Greetings
    if "hello" in user_input or "hi" in user_input:
        return "Hello! How can I help you today?"

    # Asking about chatbot
    elif "who are you" in user_input or "what are you" in user_input:
        return "I am a simple rule-based chatbot created to help you."

    # About AI
    elif "what is ai" in user_input:
        return "AI stands for Artificial Intelligence. It enables machines to think and learn like humans."

    # Asking about time
    elif "time" in user_input:
        from datetime import datetime
        return "Current time is: " + datetime.now().strftime("%H:%M:%S")

    # Asking about date
    elif "date" in user_input:
        from datetime import date
        return "Today's date is: " + str(date.today())

    # Goodbye
    elif "bye" in user_input or "goodbye" in user_input:
        return "Goodbye! Have a great day ahead!"

    # Fallback
    else:
        return "I'm sorry, I don't understand that. Can you rephrase?"

# Running chatbot loop
if __name__ == "__main__":
    print("Chatbot: Hello! I am your assistant. Type 'bye' to exit.")
    while True:
        user_input = input("You: ")
        response = chatbot_response(user_input)
        print("Chatbot:", response)
        if "bye" in user_input.lower():
            break
