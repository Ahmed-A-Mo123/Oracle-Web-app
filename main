from flask import Flask, render_template, request
import requests


app = Flask(__name__)
answers = []


@app.route('/', methods=['GET', 'POST'])
def home():
    if request.method == 'POST':
        question = request.form['question']
        answer = oracle(question)
        dicty = {"question": question,
                 "answer": answer}
        answers.append(dicty)
        return render_template("index.html", answers=answers)
    return render_template("index.html")


def oracle(question):
        url = "https://chatgpt53.p.rapidapi.com/"
        prompt = f"User question is {question})"
        payload = {
            "messages": [
                {
                    "role": "user",
                    "content": f"{prompt}"
                }
            ],
            "temperature": 1
        }
        headers = {
            "content-type": "application/json",
            "X-RapidAPI-Key": "0c5d4fbc0amsh136a99e06add104p1d8436jsn34b5198a9f5c",
            "X-RapidAPI-Host": "chatgpt53.p.rapidapi.com"
        }

        response = requests.post(url, json=payload, headers=headers)
        dictionary = response.json()
        answer = dictionary["choices"][0]["message"]["content"]
        return answer


if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
