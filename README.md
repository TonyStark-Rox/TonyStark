# jarvis_bot.py
A chatbot that talks to you about Marvel cuz your friends don't. Nerd. 
import streamlit as st
import openai

# Load your OpenAI API key from Streamlit secrets or set it directly (NOT recommended)
openai.api_key = st.secrets["OPENAI_API_KEY"]  # Make sure you add this key in Streamlit Cloud secrets

st.title("JarvisBot - Your Marvel Chatbot 🤖🦸‍♂️")

st.write("Ask me anything about the Marvel Universe!")

def get_jarvis_response(prompt):
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "You are Jarvis, an AI assistant who only talks about Marvel superheroes, movies, comics, and lore."},
            {"role": "user", "content": prompt},
        ],
        max_tokens=200,
        temperature=0.7,
    )
    return response.choices[0].message.content.strip()

user_question = st.text_input("Your question:")

if user_question:
    with st.spinner("Jarvis is thinking..."):
        answer = get_jarvis_response(user_question)
    st.markdown(f"**Jarvis:** {answer}" 
