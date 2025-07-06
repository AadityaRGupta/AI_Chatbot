import os
import openai
from flask import Flask, render_template, request
from dotenv import load_dotenv

# Load environment variables from .env file
load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")

app = Flask(__name__)

def ask_openai(message):
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[
                {"role": "system", "content": "You are a helpful assistant."},
                {"role": "user", "content": message}
            ],
            max_tokens=150,
            temperature=0.7
        )
        return response['choices'][0]['message']['content'].strip()
    except Exception as e:
        return f"Error: {e}"

@app.route("/", methods=["GET", "POST"])
def index():
    user_message = ""
    ai_response = ""
    if request.method == "POST":
        user_message = request.form["message"]
        ai_response = ask_openai(user_message)
    return render_template("index.html", user_message=user_message, ai_response=ai_response)

if __name__ == "__main__":
    app.run(debug=True)
