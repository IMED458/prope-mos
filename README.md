import webbrowser

quiz_html = """<!DOCTYPE html>
<html lang="ka">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>გულის ტონების სავარჯიშო ქვიზი</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 700px;
      margin: auto;
      padding: 20px;
    }
    .question {
      margin-bottom: 30px;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 12px;
    }
    button {
      margin: 5px 0;
      display: block;
      padding: 10px;
      width: 100%;
      border-radius: 8px;
      border: 1px solid #888;
      cursor: pointer;
    }
    .correct {
      background-color: #c8f7c5;
    }
    .wrong {
      background-color: #f8d7da;
    }
    audio {
      margin: 10px 0;
    }
  </style>
</head>
<body>

<h2>გულის ტონების სავარჯიშო ქვიზი</h2>

<div id="quiz-container"></div>

<script>
const quizData = [
  {
    audio: "https://drive.google.com/uc?export=download&id=1RMyVF96Gif-A6H5gHkTbaEJmSXsiqUQI",
    correct: "გულის მესამე ტონი",
    choices: ["გულის მესამე ტონი", "გულის მე-4 ტონი", "პირველი ტონის გახლეჩა", "მეორე ტონის გახლეჩა-გაორება"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1gZPbTOgXRuWj95CBzLm_3ZZwbr6rpe2j",
    correct: "გულის მე-4 ტონი",
    choices: ["გულის მე-4 ტონი", "გულის მესამე ტონი", "ტკაცუნა პირველი ტონი", "ფუნქციური სისტოლური შუილი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=16qV5ySIdba0V8k_n0T7JB2Tf8wWzFxW3",
    correct: "პირველი ტონის გახლეჩა",
    choices: ["პირველი ტონის გახლეჩა", "მეორე ტონის გახლეჩა-გაორება", "პერიკარდიუმის ხახუნის ხმიანობა", "ჰოლოსისტოლური შუილი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1-YAnkTfyK6uv28P3FG10lmzp2mQNZjRu",
    correct: "მეორე ტონის გახლეჩა-გაორება",
    choices: ["მეორე ტონის გახლეჩა-გაორება", "პირველი ტონის გახლეჩა", "გულის მესამე ტონი", "კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1rqQD_g9dEicE1RZwuQg8lnLgEG8I7LDa",
    correct: "პერიკარდიუმის ხახუნის ხმიანობა",
    choices: ["პერიკარდიუმის ხახუნის ხმიანობა", "ტკაცუნა პირველი ტონი", "მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე", "ფუნქციური სისტოლური შუილი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1ZyVxeV_ZIN1h3RWcq20uWpz2Mu6iQakn",
    correct: "ტკაცუნა პირველი ტონი",
    choices: ["ტკაცუნა პირველი ტონი", "გულის მესამე ტონი", "გულის მე-4 ტონი", "მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1-xJeCFlM8GukAxm1GxTwu_5pjQRsSODr",
    correct: "მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე",
    choices: ["მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე", "მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე", "კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება", "ჰოლოსისტოლური შუილი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1o4F2GL6-djigT2DYpdGsyKWuZTeDEXVT",
    correct: "მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე",
    choices: ["მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე", "მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე", "ფუნქციური სისტოლური შუილი", "პერიკარდიუმის ხახუნის ხმიანობა"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1RQaEjjg2fEVgNV_zkQ9eHftOzgA0Q0rh",
    correct: "კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება",
    choices: ["კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება", "ფუნქციური სისტოლური შუილი", "ჰოლოსისტოლური შუილი", "გულის მესამე ტონი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1y4UyCiLlZnV-KItEiKU7DQrFkN2QNvNG",
    correct: "ფუნქციური სისტოლური შუილი",
    choices: ["ფუნქციური სისტოლური შუილი", "ჰოლოსისტოლური შუილი", "მეორე ტონის გახლეჩა-გაორება", "ტკაცუნა პირველი ტონი"]
  },
  {
    audio: "https://drive.google.com/uc?export=download&id=1kIJlUjIqNMI3Qqw49pHfaFn0Q5GAcNMt",
    correct: "ჰოლოსისტოლური შუილი",
    choices: ["ჰოლოსისტოლური შუილი", "ფუნქციური სისტოლური შუილი", "პერიკარდიუმის ხახუნის ხმიანობა", "მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე"]
  }
];

const container = document.getElementById('quiz-container');

quizData.forEach((q, index) => {
  const div = document.createElement('div');
  div.className = 'question';
  div.innerHTML = `
    <h3>კითხვა ${index + 1}</h3>
    <audio controls src="${q.audio}"></audio>
  `;

  q.choices.forEach(choice => {
    const btn = document.createElement('button');
    btn.textContent = choice;
    btn.onclick = () => {
      btn.classList.add(choice === q.correct ? 'correct' : 'wrong');
      if (choice !== q.correct) {
        Array.from(div.querySelectorAll('button')).forEach(b => {
          if (b.textContent === q.correct) b.classList.add('correct');
          b.disabled = true;
        });
      } else {
        Array.from(div.querySelectorAll('button')).forEach(b => b.disabled = true);
      }
    };
    div.appendChild(btn);
  });

  container.appendChild(div);
});
</script>

</body>
</html>
"""

# შექმნა HTML ფაილი
with open("quiz.html", "w", encoding="utf-8") as f:
    f.write(quiz_html)

# გახსენი ბრაუზერში
webbrowser.open("quiz.html")
print("✅ ქვიზის ფაილი შეიქმნა და გაიხსნა ბრაუზერში!")
