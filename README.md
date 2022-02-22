# AI-Voice-Assistent


   
import pyttsx3 as p
import speech_recognition as sr
from datetime import date
import wikipedia
import pywhatkit
import pyjokes
import sys
import webbrowser
import smtplib
import datetime



engine = p.init('sapi5')
rate= engine.getProperty('rate')
engine.setProperty('rate',180)
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[1].id)


def speak(text):
    engine.say(text)
    engine.runAndWait()


def wishme():
    hour= int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning")
        speak("How are yor ?")

    elif hour>=12 and hour<18:
         speak("Good Agternoon")
         speak("How are you?")
    else:
        speak("good Evening") 
        speak("Hoe are you") 
print("Clearing the background noise . Please wait...")         
speak("Clearing the background noise .please wait. ")
print("\n")
print("hello i am your voice assistent aleax.")
speak("hello i am your voice assistent aleax .")
         

def takeCommand():
    # it take text from micriphone user and return string output            
    r = sr.Recognizer()
    with sr.Microphone() as source:
         r.energy_threshold=500
         r.adjust_for_ambient_noise(source,1.2)
         r.pause_threshold=1
         print("listening...")
         audio = r.listen(source) 
    try:
        print("recognizing....") 
        text =  r.recognize_google(audio, language="en-in")
        print("User said:",text)  
    
    except Exception as e:
        print("say that again please...")
        return "None"
    return text 
def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('muskiagrawal81@gmail.com', 'muskan2456_')
    server.sendmail('muskiagrawal81@gmail.com', to, content)
    server.close()      
if __name__=="__main__":
    wishme()
    while True:
        text = takeCommand().lower()
    # loic for  exucting the task
        if 'wikipedia' in text:
           speak("searching wikipedia....")
           text= text. replace("wikipedia", "")
           results = wikipedia.summary(text,2)
           speak("According to wikipedia")
           speak(results)
        elif 'who are you' in text:
           print('I am mini alexa a k a your virtual assistant master')
           speak('I am mini alexa a k a your virtual assistant master. how can i help you ??')
        elif 'can you do' in text :
            print('''i can play songs on youtube , tell you a joke, search on wikipedia, tell date and time,find your location, locate area on map,
                     open different websites like instagram, youtube,gmail, git hub, stack overflow and searches on google.How may i help you ??''')
            speak('''i can play songs on youtube , tell you a joke, search on wikipedia, tell date and time,find your location, locate area on map,
open different websites like insta gram, youtube,gmail, git hub, stack overflow and searches on google. How may i help you ??''')
        elif 'play' in text:
            song = text.replace('play', '')
            print('Playing' +song)
            speak('Playing' +song)
            pywhatkit.playonyt(song)
        elif 'date and time' in text :
            today = date.today()
            time = datetime.datetime.now().strftime('%I:%M %p')
# Textual month, day and year
            d2 = today.strftime("%B %d, %Y")
            print("Today's Date is ", d2, 'Current time is', time)
            speak('Today is : '+ d2)
            speak('and current time is '+ time)
        elif 'time and date' in text :
             today = date.today()
             time = datetime.datetime.now().strftime('%I:%M %p')
# Textual month, day and year
             d2 = today.strftime("%B %d, %Y")
             print("Today's Date is ", d2, 'Current time is', time)
             speak( 'Current time is '+ time)
             speak('and Today is : '+ d2)   
        elif 'time' in text:
            time = datetime.datetime.now().strftime('%I:%M %p')
            print('The current time is' +time)
            speak('The current time is')
            speak(time)
        elif 'date' in text:
            today = date.today()
            print("Today's date:", date)
# Textual month, day and year
            d2 = today.strftime("%B %d, %Y")
            print("Today's Date is ", d2)
            speak('The todays date is')
            speak(d2)
        elif 'tell me about' in text:
             text= text.replace('tell me about' , '')
             info = wikipedia.summary(text, 1)
             print(info)
             speak(info)

        elif 'what is' in text:
             text= text.replace('what is ' , '')
             info = wikipedia.summary(text, 1)
             print(info)
             speak(info)
        elif 'who is ' in text:
             text = text.replace('who is' , '')
             info = wikipedia.summary(text, 1)
             print(info)
             speak(info)
        elif 'what is ' in text :
             search = 'https://www.google.com/search?q='+text
             print(' Here is what i found on the internet..')
             speak('searching... Here is what i found on the internet..')
             webbrowser.open(search)
        elif 'joke' in text:
             _joke = pyjokes.get_joke()
             print(_joke)
             speak(_joke)
        elif 'search' in text :
            search = 'https://www.google.com/search?q='+text
            speak('searching... ')
            webbrowser.open(search)
        elif "my location" in text:
             url = "https://www.google.com/maps/search/Where+am+I+?/"
             webbrowser.get().open(url)
             speak("You must be somewhere near here, as per Google maps")
        elif 'locate ' in text :
             speak('locating ...')
             loc = text.replace('locate', '')
             if 'on map' in loc :
                loc= loc.replace('on map',' ')
             url = 'https://google.nl/maps/place/'+loc+'/&amp;'
             webbrowser.get().open(url)
             print('Here is the location of '+loc)
             speak('Here is the location of '+loc)
        elif 'on map' in text :
             speak('locating ...')
             loc = text.split(" ")
             print(loc[1])
             url = 'https://google.nl/maps/place/'+loc[1] +'/&amp;'
             webbrowser.get().open(url)
             print('Here is the location of '+loc[1])
             speak('Here is the location of '+loc[1])

        elif 'location of' in text :
              speak('locating ...')
              loc = text.replace('find location of', '')
              url = 'https://google.nl/maps/place/'+loc+'/&amp;'
              webbrowser.get().open(url)
              print('Here is the location of '+loc)
              speak('Here is the location of '+loc)
        elif 'where is ' in text :
              speak('locating ...')
              loc = text.replace('where is', '')
              url = 'https://google.nl/maps/place/'+loc+'/&amp;'
              webbrowser.get().open(url)
              print('Here is the location of '+loc)
              speak('Here is the location of '+loc)
        elif 'bootcamps' in text :
              search = 'http://tathastu.twowaits.in/index.html#courses'
              speak('opening boot camps')
              webbrowser.open(search)
        elif 'boot camps' in text :
              search = 'http://tathastu.twowaits.in/index.html#courses'
              speak('opening boot camps')
              webbrowser.open(search)
        elif 'python bootcamp' in text :
              search = 'http://tathastu.twowaits.in/kickstart_python.html'
              speak('showing pythonboot camp')
              webbrowser.open(search)
        elif 'data science bootcamp' in text :
              search = 'http://tathastu.twowaits.in/kickstart_data_science.html'
              speak('showing data science and ml bootcamp')
              webbrowser.open(search)
        elif 'open google' in text :
             print('opening google ...')
             speak('opening google..')
             webbrowser.open_new('https://www.google.co.in/')
        elif 'gmail' in text :
              print('opening gmail ...')
              speak('opening gmail..')
              webbrowser.open_new('https://mail.google.com/')
        elif 'open youtube' in text :
              print('opening you tube ...')
              speak('opening you tube..')
              webbrowser.open_new('https://www.youtube.com/')
        elif 'open instagram' in text :
              print('opening instagram ...')
              speak('opening insta gram...')
              webbrowser.open_new('https://www.instagram.com/')
        elif 'open stack overflow' in text :
              print('opening stackoverflow ...')
              speak('opening stack overflow...')
              webbrowser.open_new('https://stackoverflow.com/')
        elif 'open github' in text :
              print('opening git hub ...')
              speak('opening git hub...')
              webbrowser.open_new('https://github.com/')
        elif 'bye' in text:
             print('good bye, have a nice day !!')
             speak('good bye, have a nice day !!')
             sys.exit()
        elif 'thank you' in text:
            print("your welcome")
            speak('your welcome')
        elif 'stop' in text:
             print('good bye, have a nice day !!')
             speak('good bye, have a nice day !!')
             sys.exit()
        elif 'tata' in text:
             print('good bye, have a nice day !!')
             speak('good bye, have a nice day !!')
             sys.exit()
        elif 'email to Muskan' in text:
            try:
                speak("What should I say?")
                content = takeCommand()
                to = "muskanagrawal0401@gmail.com"    
                sendEmail(to, content)
                speak("Email has been sent!")
            except Exception as e:
                speak("Sorry my friend . I am not able to send this email")       
        else:
             print(' Here is what i found on the internet..')
             speak('Here is what i found on the internet..')
             search = 'https://www.google.com/search?q='+text
             webbrowser.open(search)  
