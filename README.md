# Task-1-in-iot-speech-to-text

html 
<!DOCTYPE html>

<html>

<body>
    <div>
        <button id="speak">Type to Speak</button>
        <p id="textarea"></p>
    </div>
</body>

<script>
    var speak = document.getElementById('speak');
    var textarea = document.getElementById('textarea');
    var SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
    var recognition = new SpeechRecognition();
    speak.addEventListener('click', function () {
        recognition.start();
        textarea.innerHTML = '...speaking';
    })
    recognition.onresult = function (e) {
        var transcript = e.results[0][0].transcript;
        textarea.innerHTML = transcript;
    }

</script>

</html>
javascript
const texts = document.querySelector(".texts");

window.SpeechRecognition =
  window.SpeechRecognition || window.webkitSpeechRecognition;

const recognition = new SpeechRecognition();
recognition.interimResults = true;

let p = document.createElement("p");

recognition.addEventListener("result", (e) => {
  texts.appendChild(p);
  const text = Array.from(e.results)
    .map((result) => result[0])
    .map((result) => result.transcript)
    .join("");

  p.innerText = text;
  if (e.results[0].isFinal) {
    if (text.includes("how are you")) {
      p = document.createElement("p");
      p.classList.add("replay");
      p.innerText = "I am fine";
      texts.appendChild(p);
    }
    if (
      text.includes("what's your name") ||
      text.includes("what is your name")
    ) {
      p = document.createElement("p");
      p.classList.add("replay");
      p.innerText = "My Name is Cifar";
      texts.appendChild(p);
    }
    if (text.includes("open ")) {
      p = document.createElement("p");
      p.classList.add("replay");
      p.innerText = "opening link";
      texts.appendChild(p);
      console.log("opening ");
      window.open("link");
    }
    p = document.createElement("p");
  }
});

recognition.addEventListener("end", () => {
  recognition.start();
});

recognition.start();
