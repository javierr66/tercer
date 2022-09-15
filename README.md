# tercer
import pyttsx3 
import speech_recognition as sr
import subprocess as sub
from datetime import datetime

engine = pyttsx3.init()

voices=engine.getProperty('voices')

engine.setProperty('voice', voices[1],id)

engine.setProperty('rate', 140)

def say(text):
    engine.say(text)
    engine.runAndWait()

while True:
    recognizer=sr.Recognizer()
#activar microfono
    with sr.Microphone() as source:
        print('Escuchando...')
        audio=recognizer.listen(source, phrase_time_limit=3)
    
    try:# si se entiende nuestra peticion entramos a la logica principal
        comando=recognizer.recognize_google(audio, language='es-MX')
        print(f'Creo  que dijiste "{comando}"')

        comando=comando.lower()
        comando=comando.split('  ')

        if 'computadora' in comando:
            if 'abre' in comando or 'abrir' in comando:

                sites={
                    'google':'google.com',
                    'youtube':'youtube.com',
                    'instagram':'instagram.com'
                }
                for i in list(sites.keys()):
                    if i in comando:
                        sub.call(f'start brave.exe {sites[i]}', shell=True)
                        say(f'Abriendo {i}')

            elif 'hora' in comando:
                time=datetime.now().strftime('%H:%M')
                say(f'Son las {time}')

            if 'termina' in comando or 'terminar' in comando or 'termino' in comando or 'terminó' in comando:
                    say('Sesion finalizada')
                    break

    except:# si no se entiende nos da este mensaje 
        print('no te entiendo, porfavor vuelve a intentarlo')


