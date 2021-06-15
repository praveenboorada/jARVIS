# jARVIS
#it's an voice assistant


import speech_recognition as sr
import pyttsx3
import datetime as dt
import pywhatkit as pk
import wikipedia as wiki

listener = sr.Recognizer()
speaker = pyttsx3.init()

""" RATE"""
rate = speaker.getProperty('rate')   # getting details of current speaking rate
print (rate)                        #printing current voice rate
speaker.setProperty('rate', 150)     # setting up new voice rate

def speak(text):
    speaker.say("yes boss "+text)
    speaker.runAndWait()
va_name = 'jarvis'
speak('i am your '+va_name+' tell me boss')


def take_command():
    command=''
    try:
        with sr.Microphone() as source:
            print('listening.......')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if va_name in command:
                command = command.replace(va_name + ' ', '')
               # print(command)
                #speak(command)

    except:
        print("sorry i didn't hear")
    return command
    
    
while(True):
  user_command=take_command()
  #print(user_command)
  #speak(user_command)
  if 'close' in user_command:
      print('see you again boss')
      speak('see you again boss')
      
      
  elif 'time' in user_command:
      curr_time = dt.datetime.now().strftime("%I:%M %p")
      print(curr_time)
      speak(curr_time)
      
      
  elif 'play' in user_command:
      user_command=user_command.replace('play ','')
      print('playing'+user_command)
      speak('playing' + user_command+'enjoy boss')
      pk.playonyt(user_command)
      break
      
      
  elif 'search' in user_command or 'google' in user_command:
      user_command=user_command.replace('search ','')
      user_command = user_command.replace('google', '')
      speak('searching '+ user_command)
      pk.search(user_command)
      
      
      
  elif 'who is ' in user_command :
      info = wiki.summary(user_command,2)
      speak(info)
