# Youtube-Video-audio-Downloader
#Simple Project to Download YouTube Videos
from tkinter import *
from tkinter import ttk
from tkinter import filedialog
from pytube import YouTube #pip install pytube3

Folder_Name = ""

#file location
def openLocation():
    global Folder_Name
    Folder_Name = filedialog.askdirectory()
    if(len(Folder_Name) > 1):
        locationError.config(text=Folder_Name,fg="green")
    else:
        locationError.config(text="Please Choose Folder!!",fg='red')

#download Video
def DownloadVideo():
    choice = ytdchoices.get()
    url = ytdEntry.get()

    if(len(url)>1):
        ytdError.config(text="")
        yt = YouTube(url)

        if(choice == choices[0]):
            select = yt.streams.filter(progressive=True).first()

        elif(choice == choices[1]):
            select = yt.streams.filter(progressive=True,file_extension="mp4").last()

        elif(choice == choices[2]):
            select = yt.streams.filter(only_audio=True).first()

        else:
            ytdError.config(text="Paste Link again!!!",fg='red')

     #download Funtcion
    select.download(Folder_Name)
    ytdError.config(text='Download Completed!!',fg='green')


root = Tk()
root.title("Youtube1x Downloader")
root.geometry('350x400') #set window
root.columnconfigure(0, weight=1) #set all content in center.

#Ytd Link Label
ytdLabel = Label(root, text='Enter the URL of the Video', font=('jost', 15))
ytdLabel.grid()

# Entry Box
ytdEntryVar = StringVar()
ytdEntry = Entry(root, width=50, textvariable=ytdEntryVar)
ytdEntry.grid()

#Error Msg
ytdError = Label(root, text='Error Msg', fg='red', font=('jost', 10))
ytdError.grid()

#Asking Save file label
saveLabel = Label(root, text='Save the Video File', font=('jost', 15, 'bold'))
saveLabel.grid()

#btn of save file
saveEntry = Button(root, width=10, bg="red", fg="white", text="Choose Path",command=openLocation)
saveEntry.grid()

#Error Mag Location
locationError = Label(root, text='Error Msg', fg='red', font=('jost', 10))
locationError.grid()

#Download Quality
ytdQuality = Label(root, text='Selevt Quality', font=('jost', 15))
ytdQuality.grid()

#combobox
choices = ["720p", '144p', "Only Audio"]
ytdchoices = ttk.Combobox(root, values=choices)
ytdchoices.grid()

#download btn
downlandBtn = Button(root, width=10, bg="red", fg="white", text="Download",command=DownloadVideo)
downlandBtn.grid()

#developer Label
developerlabel = Label(root, text="Mohamed Al Chorbaji", font=('jost', 15))
developerlabel.grid()

root.mainloop()
