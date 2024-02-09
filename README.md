from tkinter.ttk import *
from tkinter import *
from tkinter import ttk
from ttkthemes import ThemedTk
import random
import pyttsx3
import speech_recognition
import pyaudio

Score = 0
i = speech_recognition.Recognizer()


def SpeakText(command):

    engine = pyttsx3.init()
    rate = engine.getProperty('rate')
    engine.setProperty('rate',rate-80)
    engine.say(command)
    engine.runAndWait()

def Pc():
    a = random.randint(1,3)
    if a == 1:
        Pclbl.configure(Image = rock)
    elif a == 2:
        Pclbl.configure(Image = paper)
    else:
        Pclbl.configure(Image = scissors)

def Listen():
    with speech_recognition.Microphone() as source2:

        i.adjust_for_ambient_noise(source2,duration=1)
        SpeakText("Say Rock,Paper or Scissors to choose")

        audio2 = i.listen(source2)

        try:
            Mytext = i.recognize_google(audio2)
            Mytext = Mytext.lower()
            print(Mytext)

        except:
            SpeakText("Didnt understand you")
            SpeakText("Try again")
            Listen()
            return
    if Mytext.__contains__("rock"):
        Playerlbl.configure(Image = rock)
    elif Mytext.__contains__("paper"):
        Playerlbl.configure(Image=paper)
    elif Mytext.__contains__("scissors"):
        Playerlbl.configure(Image=scissors)


def Start():
    Listen()





window = ThemedTk(theme = "yaru")
window.configure(themebg="yaru")
window.geometry("800x600")

rock = PhotoImage(file = "rock.png")
scissors = PhotoImage(file = "scissors.png")
paper = PhotoImage(file = "paper.png")
RPC = PhotoImage(file = "RPC.png")

Titlelbl = ttk.Label(window,text="Rock Paper Scissors Game vs Computer!",justify=CENTER,font = ("Mangal", 20,'bold'))
Titlelbl.place(x= 120,y=0)

Playerlbl = ttk.Label(window,image =RPC)
Playerlbl.place(x=125,y=230)

Pclbl = ttk.Label(window,image =RPC)
Pclbl.place(x=520,y=230)

Label1 = ttk.Label(window,text = "You:",font = ("Mangal", 15,'bold'))
Label1.place(x=143,y=180)

Label2 = ttk.Label(window,text = "Pc:",font = ("Mangal", 15,'bold'))
Label2.place(x=577,y=180)

Scorelbl = ttk.Label(window,text = "Score:" + str(Score),font = ("Mangal", 15,'bold'))
Scorelbl.place(x=350,y=70)


Startbtn = ttk.Button(window,text = "Start",command = Start)
Startbtn.place(x=350,y=420)

window.mainloop()
