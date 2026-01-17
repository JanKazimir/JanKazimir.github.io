+++
toc = true
readingTime = true
draft = false
image = ''
date = '2025-12-03T12:36:49+01:00'
title = 'PomodorUp And adventures in Vibe Coding'
description = 'How I learned to Relax and Ride the Vibes'
tags = [
    "Python",
    "Project",
    "Programming",
]
categories = [
    "Programming",
    "Project Showcase",
]
series = [""]
aliases = [""]

+++
# PomodorUp And adventures in Vibe Coding

0/ Does “vibe coding” deserve PascalCase?

I made an app. I use it all the time!
It’s called PomodorUp, because it’s a Pomodoro timer... that counts Up! Groundbreaking. As hard as it is to believe, I actually *wanted* this, to the point that I made it. I also hoped to learn from the process, and, and I *sorta* did. 
Let me explain. 

I think the best learning comes from trying to achieve a result.
Reality forces you to solve problems every step of the way, that’s expected, but importantly, *unexpected problems* arise.

This is why vibe coding is strange: it sits in between you and the goal, you and the problem: you’re managing an ai agent, that hopefully solves the problem. If you never look at the code and approve blindly, would you learn anything? 
As it turn out, yes, to some extent. 

Building pomodorUp I have seen the code of a full program; many interacting functions summing up to a whole program. The way classes are used, and how much research into libraries is involved with doing something as simple as a timer. 
I learned what a virtual environment is, how to run a script, and (much, *much*) later that there is a button for that in vscode (top right of the main window). 
This is what I learned from vibe coding. The useful result.
I also have an app that i use all the time and that’s cool.

But did I learn to code better? 
Not really, no. I didn’t write a single function. I modified things, like the position of text appearing on the menu bar icon. 
But that’s not all there is to it to programming, and *that*, is something I learned. Deployment, envrironment, library research, interacting with macOS, all those are necessary parts of a running program.
Speedrunning through the process of writing a program is incredibly useful: I know what I’m getting into with much more clarity now. 
I can’t code better, but it made me a better *programmer*. 

## The process

I started simple with making a set detailed prompts that I was carefully  going to feed, one at time, going bit by bit.

This was my initial prompt:

> So here is the idea; i want to create a simple mac os app : a pomodoro timer that counts UP instead of down. Amazing, groundbreaking, i know.  
> This is the first time i create an application of any kind. I do know some python, which is why i want the app to be done in python, but i have no idea of the libraries i might need or anything like that. i would like the app to live in the menu bar of the mac, and have a graphical interface, altough we can keep that for later if it's easier to just do it with a terminal commands or something.  
> So let's start with the basic:

And there I mistakenly pressed `enter` instead of `shift` + `enter`. 
Off it went, riproaring through the task like a toddler on red bull: you sit back, wait and hope nothing expensive breaks.

It flattered me for my genius idea, recommended and built a virtual environment, and wrote this script: <!-- tk: this section should collapse -->


```python
import time
import threading
from datetime import datetime, timedelta
import pystray
from PIL import Image, ImageDraw
import sys

class PomodoroTimer:
    def __init__(self):
        self.start_time = None
        self.is_running = False
        self.timer_thread = None
        self.icon = None
        
    def create_icon(self, text="00:00"):
        # Create a simple icon with the timer text
        width = 64
        height = 64
        image = Image.new('RGB', (width, height), color='white')
        draw = ImageDraw.Draw(image)
        
        # Draw a simple circle for the icon
        draw.ellipse([8, 8, 56, 56], fill='red', outline='darkred')
        
        # Add timer text
        try:
            draw.text((width//2, height//2), text, fill='white', anchor='mm')
        except:
            # Fallback if text drawing fails
            pass
            
        return image
    
    def get_elapsed_time(self):
        if self.start_time:
            elapsed = datetime.now() - self.start_time
            return elapsed
        return timedelta(0)
    
    def format_time(self, elapsed):
        total_seconds = int(elapsed.total_seconds())
        minutes = total_seconds // 60
        seconds = total_seconds % 60
        return f"{minutes:02d}:{seconds:02d}"
    
    def update_icon(self):
        while self.is_running:
            if self.start_time:
                elapsed = self.get_elapsed_time()
                time_text = self.format_time(elapsed)
                new_icon = self.create_icon(time_text)
                self.icon.icon = new_icon
            time.sleep(1)
    
    def start_timer(self):
        if not self.is_running:
            self.start_time = datetime.now()
            self.is_running = True
            self.timer_thread = threading.Thread(target=self.update_icon, daemon=True)
            self.timer_thread.start()
            print("Timer started!")
    
    def stop_timer(self):
        if self.is_running:
            self.is_running = False
            self.start_time = None
            self.icon.icon = self.create_icon("00:00")
            print("Timer stopped!")
    
    def reset_timer(self):
        self.stop_timer()
        print("Timer reset!")
    
    def quit_app(self):
        self.stop_timer()
        self.icon.stop()
        sys.exit()
    
    def create_menu(self):
        menu = pystray.Menu(
            pystray.MenuItem("Start Timer", self.start_timer),
            pystray.MenuItem("Stop Timer", self.stop_timer),
            pystray.MenuItem("Reset Timer", self.reset_timer),
            pystray.Menu.SEPARATOR,
            pystray.MenuItem("Quit", self.quit_app)
        )
        return menu
    
    def run(self):
        # Create initial icon
        initial_icon = self.create_icon("00:00")
        
        # Create the system tray icon
        self.icon = pystray.Icon("PomodorUP", initial_icon, "PomodorUP Timer", self.create_menu())
        
        # Run the app
        self.icon.run()

if __name__ == "__main__":
    timer = PomodoroTimer()
    timer.run()
```


It *worked*. 
It was ugly, but it *worked*.
<!-- tk: insert images here -->
[First try](static/img/PU1.png)



Little by little, I began to feed it higher level prompts; my experience has been that the models are now pretty good at guessing intent, while filling in every detail takes time, and is more likely to confuse the AI. It will sometimes be wrong and confidentely go for it, so I’ve had to go back to undo things, but it also means I can be somewhat vague, point to something and get a good result. Sometimes.
The confidence can be entertaining... and grating.
One pitfall I noticed is that when trying to do a complex task, or many small taks in one prompt, the model will miss the most important task but go way too deep on some detail.

#### It’s gambling. 
I have read that analogy several times by now, and there is a lot of truth to it. Sometimes a vague direction returns working code *fast*. There is a thrill to that, it’s a rush, it’s fun... 
But then you can rewrite the same prompt 10 times, going back and forth around the same tasks, hoping that pulling that bandit’s arm *one more time* will deliver the goods. 
Nope, it didn’t.
But maybe *this* time?

You often win, especially small, easy tasks. But I also nearly drove myself nuts trying to make the “drift +1” function be triggered by a single left click on the icon. It was never going to work, but it wasn’t *telling me that*. Not until I changed the model.

So it’s good, but not great, annoying but helpful, a great teacher, sometimes, an annoying prick on occasion. 
A tool, we all have to decide when and where to use it. 
This is what it looks like right now: 
<!-- insert image here -->
[PomodorUp now](static/img/PU2.png)



