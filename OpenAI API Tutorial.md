# Introduction to OpenAI API
***
The OpenAI API allows developers to access and utilize OpenAI's artificial intelligence models in their applications. This document aims to provide a brief overview and examples of how to interact with the OpenAI API.

## Setting the API Key
***
Before using the OpenAI API, you need to authenticate yourself. This is done by setting an API key. The API key is a secret key provided by OpenAI for authenticating API requests. It should be kept confidential.

```python
import openai
openai.api_key = "your-key-here"
```

Your OpenAI API key can be found in your OpenAI account dashboard under the API keys section. It is recommended to not hard-code the API key in your scripts. Instead, consider setting it as an environment variable and then fetching it in your script. Be very cautious to not expose it publicly, as it would give anyone access to your OpenAI account and could lead to misuse.

## Making a Request to the Completion Endpoint
***
You can make a request to the API using the `openai.Completion.create()` method. This method takes in several parameters, including `model` and `prompt`. The `model` parameter specifies the AI model to be used (for example, `text-davinci-003`), and `prompt` is the starting text that the AI model will complete.

```python
response = openai.Completion.create(
    model = "text-davinci-003",
    prompt = "Who developed ChatGPT"
)
```

OpenAI provides different models, each with its own strengths and use cases. For example, `text-davinci-003` is a versatile model that can be used for a wide range of tasks. Always refer to the OpenAI API documentation to choose the model that best fits your specific needs.

## Extracting the Response
***
The API response is a JSON object that includes information about the created completion. You can extract the generated text from the response with this line of code:

```python
print(response["choices"][0]["text"])
```

The response contains many other fields that provide additional information about the request. For instance, `response["model"]` gives the model used for the request, `response["id"]` gives the unique identifier for the request, and `response["created"]` gives the timestamp of when the request was created. The actual AI-generated text is located within `response["choices"][0]["text"]`.

## OpenAI's Text and Chat Capabilities
***
### Text Completion

The OpenAI API can generate new text outputs based on a given text prompt. For text completion, you can specify a `prompt`, the `model`, and optionally, the maximum number of tokens (`max_tokens`) you want the output to contain. The `temperature` parameter controls randomness (lower values make output more focused, higher values make it more diverse).

```python
response = openai.Completion.create(
  model = "text-davinci-003",
  prompt = prompt,
  max_tokens = 100,
  temperature = 0.2  # Optional: controls randomness of output.
)
```

Text completion can be applied to a variety of tasks, such as drafting emails, writing code, answering questions, and more. Here are some examples:

#### Text Completion for Find and Replace Task

This example demonstrates how the OpenAI API can be used to replace a word (car) with another word (plane) and adjust the rest of the text accordingly.

```python
prompt = """ Replace car with plane and adjust phrase:
A car is a vehicle that is typically powered by an internal combustion engine or an electric motor. It has four wheels, and is designed to carry passengers and/or cargo on roads or highways. Cars have become a ubiquitous part of modern society, and are used for a wide variety of purposes, such as commuting, travel, and transportation of goods. Cars are often associated with freedom, independence, and mobility."""

# Create a request to the Completion endpoint
response = openai.Completion.create(
  model = "text-davinci-003",
  prompt = prompt,
  max_tokens = 100
)

# Extract and print response text
print(response["choices"][0]["text"])
```

#### Text Summarization

In this example, the OpenAI API is used to summarize a given text into two concise bullet points.

```python
prompt="""Summarize the following text into two concise bullet points:
Investment refers to the act of committing money or capital to an enterprise with the expectation of obtaining an added income or profit in return. There are a variety of investment options available, including stocks, bonds, mutual funds, real estate, precious metals, and currencies. Making an investment decision requires careful analysis, assessment of risk, and evaluation of potential rewards. Good investments have the ability to produce high returns over the long term while minimizing risk. Diversification of investment portfolios reduces risk exposure. Investment can be a valuable tool for building wealth, generating income, and achieving financial security. It is important to be diligent and informed when investing to avoid losses."""

# Create a request to the Completion endpoint
response = openai.Completion.create(
  model = "text-davinci-003",
  prompt = prompt,
  temperature = 0.2, # controls degree of randomness of output
  max_tokens = 400
)
```

#### Content Generation

This example shows how the OpenAI API can be used to generate creative content, such as a slogan for a new fine-dining Italian restaurant.

```python
# Create a request to the Completion endpoint
response = openai.Completion.create(
  model = "text-davinci-003",
  prompt = "Create a slogan for a new fine-dining Italian restaurant",
  max_tokens = 100
)
```

#### Text Completions for Classification Tasks

In this example, the OpenAI API is used to classify the sentiment of different statements as either negative, positive or neutral.

```python
# Create a request to the Completion endpoint
response = openai.Completion.create(
  model = "text-davinci-003",
  prompt = """
  Classify the sentiment of the following statements as either negative, positive or neutral:
  1. Unbelievably good!
  2. Shoes fell apart on the second use.
  3. The shoes look nice, but they aren't very comfortable.
  4. Can't wait to show them off!
  """,
  max_tokens = 100
)
```

#### Categorizing Companies

This example shows how the OpenAI API can be used to categorize companies. The model can be directed to categorize companies into specified categories by providing a more specific prompt.

```python
# Without specification of categories
response = openai.Completion.create(
  model="text-davinci-003",
  prompt="""Categorize the following companies:

 
  Apple, Microsoft, Saudi Aramco, Alphabet, Amazon, Berkshire Hathaway, NVIDIA, Meta, Tesla, and LVMH
  """,
  max_tokens=100,
  temperature=0.5
)

# With specification of categories (Adjust prompt accordingly)
prompt="Categorize the following companies into the 4 categories of Tech, Energy, Luxury Goods or Investment: ..."
```

***
### Chat Completions API

The OpenAI API also supports multi-turn conversations. These are similar to text completions, but instead of a single prompt, you give the model a list of messages. Each message has a role (either "system", "user", or "assistant") and content. The model generates a response based on the entire conversation.

```python
response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "system", "content": "You are a helpful data science tutor."},
    {"role": "user", "content": "What is the difference between a for loop and a while loop?"}
  ]
)
```

This form of interaction is particularly useful for creating conversational agents, such as chatbots. The "system" role is used to set the behavior of the "assistant", and the "user" and "assistant" roles represent the conversation turns.

Here are some examples:

#### Code Explanation

In this example, the OpenAI API is used to explain what a piece of Python code does in one sentence.

```python
instruction = """Explain what this Python code does in one sentence:
import numpy as np

heights_dict = {"Mark": 1.76, "Steve": 1.88, "Adnan": 1.73}
heights = heights_dict.values()
print(np.mean(heights))
"""

# Create a request to the ChatCompletion endpoint
response = openai.ChatCompletion.create(
  model="gpt-3.5-turbo",
  messages = [
    {"role": "system",
     "content": "You are a helpful data science tutor."},
    {"role": "user",
    "content": instruction}
  ],
  max_tokens=100
)
```

#### In-Context Learning

In this example, the OpenAI API is used to explain what the `type()` function does in Python. The model is trained in-context by providing it with an example of the `min()` function first.

```python
response = openai.ChatCompletion.create(
   model="gpt-3.5-turbo",
   # Add a user and assistant message for in-context learning
   messages=[
     {"role": "system", "content": "You are a helpful Python programming tutor."},
     {"role": "user", "content": "Explain what the min() function does."},
     {"role": "assistant", "content": "The min() function returns the smallest item from an iterable."},
     {"role": "user", "content": "Explain what the type() function does."}
   ]
)
```

#### Multi-turn Chat Completions with GPT

In this example, the OpenAI API is used to create a chatbot that can explain mathematical concepts.

```python
messages = [{"role": "system", "content": "You are a helpful math tutor."}]
user_msgs = ["Explain what pi is.", "Summarize this in two bullet points."]

for q in user_msgs:
    print("User: ", q)
    
    # Create a dictionary for the user message from q and append to messages
    user_dict = {"role": "user", "content": q}
    messages.append(user_dict)
    
    # Create the API request
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages = messages,
        max_tokens=100
    )
    
    # Convert the assistant's message to a dict and append to messages
    assistant_dict = dict(response["choices"][0]["message"])
    messages.append(assistant_dict)
    print("Assistant: ", response["choices"][0]["message"]["content"], "\n")
```

## Other Capabilities
***
### Text Moderation

OpenAI's API can be used to identify inappropriate content in text. This involves sending a request to the Moderation endpoint and checking the response's category scores.

```python
response = openai.Moderation.create(
    model = "text-moderation-latest",
    input = "My favorite book is How to Kill a Mockingbird."
)
```

This can be useful in applications like content moderation in online forums, comment sections, etc.

### Speech-to-Text Transcription (Whisper)

The Whisper model is OpenAI's automatic speech recognition (ASR) system. It can transcribe spoken language into written text. This can be used on an audio file to create a transcript.

```python
# Open the openai-audio.mp3 file
audio_file = open("openai-audio.mp3", "rb")

# Create a transcript from the audio file
response = openai.Audio.transcribe("whisper-1", audio_file)

# Extract and print the transcript text
print(response["text"])
```

### Speech Translation with Whisper

The Whisper model can also be used to translate spoken language into another language. This involves specifying a prompt to help the model generate a better response.

```python
# Open the audio.wav file
audio_file = open("audio.wav", "rb")

# Write an appropriate prompt to help the model
prompt = "The transcript is about a recent World Bank report"

# Create a translation from the audio file
response = openai.Audio.translate("whisper-1", audio_file, prompt = prompt)

print(response["text"])
```

### Chaining Models

Chaining, or combining models, can be very powerful. Here's an example of using the output of the Whisper model as an input to the text completion model to identify the language spoken in an audio file.

```python
# Open the audio.wav file
audio_file = open("audio.wav", "rb")

# Create a transcription request using audio_file
audio_response = openai.Audio.transcribe("whisper-1", audio_file)

# Create a request to the API to identify the language spoken
chat_response = openai.ChatCompletion.create(
    model = "gpt-3.5-turbo",
    messages = [
        {"role":"user", "content": "What is the language of the transcript: " + audio_response["text"]}
    ]
)
print(chat_response)
```

#### Creating Meeting Summaries

This example shows how the OpenAI API can be used to summarize a meeting transcript into bullet points. It involves transcribing an audio file of the meeting using the Whisper model, and then summarizing the transcript using the GPT model.

```python
# Open the datacamp-q2-roadmap.mp3 file
audio_file = open("datacamp-q2-roadmap.mp3", "rb")

# Create a transcription request using audio_file
audio_response = openai.Audio.transcribe("whisper-1", audio_file)

# Create a request to the API to summarize the transcript into bullet points
chat_response = openai.ChatCompletion.create(
    model = "gpt-3.5-turbo",
    messages = [
        {"role":"user", "content":"Summarize the given meeting transcript in bullet points:" + audio_response["text"]}
    ]
)
print(chat_response["choices"][0]["message"]["content"])
```

## Conclusion
***
The OpenAI API provides a wide range of capabilities for developers to leverage powerful AI models in their applications. From text generation and summarization, to content moderation, to speech transcription and translation, OpenAI's models can be applied to a variety of use cases. By understanding how to use the OpenAI API effectively, you can unlock the potential of these models to enhance your applications and services.

### Additional Resources

For further learning and help, refer to the [OpenAI documentation](https://beta.openai.com/docs/), [OpenAI Community forum](https://community.openai.com/), and [OpenAI Support](https://beta.openai.com/support/).