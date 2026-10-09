# Streamlit chatbot demo

A small chatbot web app built with Streamlit and the OpenAI API. It keeps the conversation in Streamlit's session state, lets you change the assistant's personality from the sidebar, and trims old messages to stay within a token budget.

Forked from [acstrahl/streamlit_chatbot_demo](https://github.com/acstrahl/streamlit_chatbot_demo).

## Files

| File | Description |
|------|-------------|
| `starter_code.py` | The command-line chatbot the app starts from |
| `final.py` | The finished Streamlit app |

## Setup

```bash
pip install -r requirements.txt
```

Provide your OpenAI API key in one of two ways:

```bash
# as an environment variable
export OPENAI_API_KEY="your-api-key"
```

or in `.streamlit/secrets.toml` (already ignored by git):

```toml
OPENAI_API_KEY = "your-api-key"
```

## Running the app

```bash
streamlit run final.py
```

## How it works

- **Session state:** `st.session_state.messages` holds the conversation, so it survives Streamlit's reruns.
- **Sidebar controls:** max tokens, temperature and the system message (two presets or a custom one). "Apply New System Message" swaps the system prompt mid-conversation; "Reset Conversation" starts again.
- **Token budget:** before each request, the oldest messages after the system prompt are dropped until the history fits in `TOKEN_BUDGET` tokens, counted with `tiktoken`.

## Changes in this fork

- The app no longer crashes on start when there is no `secrets.toml`; it falls back to the `OPENAI_API_KEY` environment variable and shows a clear message if neither is set
- A failed API request shows an error instead of a traceback, and the unanswered message is removed from the history
- Added this README
