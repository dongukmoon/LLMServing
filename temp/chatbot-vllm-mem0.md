# Building chatbot with vLLM backend running gpt-oss and Mem0 incorportaed

## 1. build python chatbot
Refer to [1]

```python
import openai

# Modify OpenAI's API key and API base to use vLLM's API server.
openai_api_key = "EMPTY"
openai_api_base = "http://localhost:8000/v1"

# Function to interact with OpenAI
def chat_with_openai(user_input):
    client = OpenAI(
        # defaults to os.environ.get("OPENAI_API_KEY")
        api_key=openai_api_key,
        base_url=openai_api_base,
        )

    models = client.models.list()
    model = models.data[0].id

    # Chat Completion API
    chat_completion = client.chat.completions.create(
           messages=[
            {"role": "system", "content": "You are a helpful assistant."},
            {"role": "user", "content": user_input},
        ],
        model=model,
    )

    return chat_completion

# Function to start the chatbot
def start_chatbot():
    print("👋 Welcome! I'm your chatbot. Type 'exit' to end the chat.\n")

    while True:
        user_input = input("You: ")
        if user_input.lower() == 'exit':
            print("Goodbye! 👋")
            break
        response = chat_with_openai(user_input)
        print(f"Bot: {response}\n")

# Start the chatbot
if __name__ == "__main__":
    start_chatbot()
```


## 2. Setup vLLM and connect it to chatbot


## 3. Mem0 integration


## Reference
1. https://dev.to/abhinowww/how-to-build-a-simple-chatbot-in-python-using-openai-step-by-step-guide-hfg
