import tkinter as tk
import fnmatch
import os
from pygame import mixer

# Initialize the main window
canvas = tk.Tk()
canvas.title("Music Player")
canvas.geometry("600x600")
canvas.config(bg='black')

# Path to the directory containing music files
rootpath = "C:/Users/Lenovo/Music"
pattern = "*.mp3"

# Initialize the mixer
mixer.init()

# Function to safely load images
def load_image(path):
    try:
        return tk.PhotoImage(file=path)
    except Exception as e:
        print(f"Error loading image {path}: {e}")
        return None

# Load images for buttons
prev_img = load_image("C:/Users/Lenovo/Downloads/previous.png")
play_img = load_image("C:/Users/Lenovo/Downloads/play.png")
pause_img = load_image("C:/Users/Lenovo/Downloads/pause.png")
next_img = load_image("C:/Users/Lenovo/Downloads/next.png")

# Function to select and play a song
def select(event=None):
    selected_song = listBox.get("active")
    label.config(text=selected_song)
    mixer.music.load(os.path.join(rootpath, selected_song))
    mixer.music.play()

# Function to play the next song in the list
def play_next():
    current_selection = listBox.curselection()
    if current_selection:
        current_selection = current_selection[0]
        next_song = (current_selection + 1) % listBox.size()
        listBox.select_clear(current_selection)
        listBox.activate(next_song)
        listBox.select_set(next_song)
        select()

# Function to play the previous song in the list
def play_prev():
    current_selection = listBox.curselection()
    if current_selection:
        current_selection = current_selection[0]
        prev_song = (current_selection - 1) % listBox.size()
        listBox.select_clear(current_selection)
        listBox.activate(prev_song)
        listBox.select_set(prev_song)
        select()

# Function to pause and unpause the song
def pause_song():
    if pauseButton["text"] == "pause":
        mixer.music.pause()
        pauseButton["text"] = "play"
    else:
        mixer.music.unpause()
        pauseButton["text"] = "pause"

# Listbox to display songs
listBox = tk.Listbox(canvas, fg="cyan", bg="black", width=100, font=('DS-Digital', 14))
listBox.pack(padx=15, pady=15)
listBox.bind('<Double-Button-1>', lambda event: select(event))

# Label to display the currently playing song
label = tk.Label(canvas, text='', bg='black', fg='yellow', font=('DS-Digital', 14))
label.pack(pady=15)

# Frame to hold control buttons
button_frame = tk.Frame(canvas, bg='black')
button_frame.pack(padx=10, pady=20, anchor='center')

# Common button options
button_options = {'bg': 'gray', 'fg': 'white', 'borderwidth': 0, 'compound': 'top', 'width': 80, 'height': 80}

# Control buttons with proper size and spacing
prevButton = tk.Button(button_frame, text="Prev", image=prev_img, **button_options, command=play_prev)
prevButton.pack(side='left', padx=10)

playButton = tk.Button(button_frame, text="Play", image=play_img, **button_options, command=select)
playButton.pack(side='left', padx=10)

pauseButton = tk.Button(button_frame, text="Pause", image=pause_img, **button_options, command=pause_song)
pauseButton.pack(side='left', padx=10)

nextButton = tk.Button(button_frame, text="Next", image=next_img, **button_options, command=play_next)
nextButton.pack(side='left', padx=10)

# Load music files into the listbox
for root, dirs, files in os.walk(rootpath):
    for filename in fnmatch.filter(files, pattern):
        listBox.insert('end', filename)

# Start the main loop
canvas.mainloop()
