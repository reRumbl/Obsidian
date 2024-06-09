**SpeechRecognition** - это библиотека для Python, реализующая возможность распознавания голоса.

![[SpeechRecognition.png]]

**Установка через cmd или terminal:**

```Python
pip install SpeechRecognition
```

**Подключение в проект:**

```Python
import speech_recognition
```

**Простая программа для распознавания фразы, сказанной в микрофон:**

```Python
def recognize_speech_from_mic():  
    recognizer = speech_recognition.Recognizer()  
  
    with speech_recognition.Microphone() as source:  
        recognizer.adjust_for_ambient_noise(source)  
        print('Say something...')  
        audio = recognizer.listen(source)  
        try:  
            text = recognizer.recognize_google(audio, language='ru-RU')  
            print(f'You say: {text}')  
        except speech_recognition.UnknownValueError:  
            print('Unable to recognize speech')  
        except speech_recognition.RequestError as e:  
            print(f'Recognition service error: {e}')  
  
  
if __name__ == "__main__":   
    recognize_speech_from_mic()
```