# Text_Speech_Converter

# Objective:
Create a web application that converts user-inputted text to speech.

# Languages Used:
1. HTML: Structure the web page.
2. CSS: Style the web page for a better user interface.
3. JavaScript: Implement the TTS (Text to Speech)  functionality.

# speechSynthesis API
The SpeechSynthesis API is part of the Web Speech API, which allows you to incorporate speech synthesis (text-to-speech) functionality into web applications.

# Key Components
1.SpeechSynthesis Interface:
The main controller interface for speech synthesis. It allows you to start, pause, resume, and cancel speech.

2.SpeechSynthesisUtterance:
Represents the speech request. It contains properties for the text to be spoken, voice to be used, pitch, volume, rate, etc.

3.Voices:
A list of all the voices available on the device that can be used for speech synthesis.

# Working of speechSynthesis API in JavaScript 

# 1. SpeechSynthesisUtterance Initialization

let speech = new SpeechSynthesisUtterance();

This creates a new instance of SpeechSynthesisUtterance which will represent the speech request.

# 2. Voice Array and Select Element

let voices = [];
let voiceSelect = document.querySelector("select");

An empty array voices is declared to store the available voices.
voiceSelect is a reference to a <select> element in your HTML where the available voices will be displayed as options.

# 3. Populating the Voices Array

window.speechSynthesis.onvoiceschanged = () => {
    voices = window.speechSynthesis.getVoices();
    speech.voice = voices[0];
    
    voices.forEach((voice, i) => (voiceSelect.options[i] = new Option(voice.name, i)));
};

An event listener for onvoiceschanged is added. This event is triggered when the list of voices is loaded or changed.

window.speechSynthesis.getVoices() fetches the list of available voices and stores them in the voices array.

speech.voice = voices[0] sets the first available voice as the default voice.

The forEach loop populates the <select> element with the available voices. Each voice is added as an option to the select element, 
where voice.name is the visible text and i is the value.
   
# 4. Changing the Voice

voiceSelect.addEventListener("change", () => {
    speech.voice = voices[voiceSelect.value];
});

An event listener is added to the <select> element to detect when the user changes the selected voice.

speech.voice = voices[voiceSelect.value] sets the speech voice to the selected voice based on the index from the voices array.

# 5. Speaking the Text

document.querySelector("button").addEventListener("click", () => {
    speech.text = document.querySelector("textarea").value;
    window.speechSynthesis.speak(speech);
});

An event listener is added to a <button> element. When the button is clicked:

speech.text is set to the value from the <textarea> element.

window.speechSynthesis.speak(speech) initiates the speech synthesis with the provided text and selected voice.
