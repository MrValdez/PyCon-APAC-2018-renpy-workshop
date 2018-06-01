Making a visual novel using Ren'Py

# Introduction

Ren'py is a game engine that have its own scripting language built especially for visual novels. Ren'py is built on Python and Pygame. You can run your own python or pygame code within the engine.

Visual novels are a genre of video games similar to choose-your-own-adventure books. VNs can get a following and it is uncommon to find [VNs adapted as an anime](https://www.anime-planet.com/anime/tags/based-on-a-visual-novel). Ren'py have [many games created and sold online](https://games.renpy.org/). My personal favorite is [Long Live the Queen](https://store.steampowered.com/app/251990/Long_Live_The_Queen/)

# Pre-requisites

1. Download Ren'py from https://www.renpy.org/
1. If you do not have an IDE (that is capable of turning tabs into spaces), I recommend getting and installing [notepad2](http://www.flos-freeware.ch/notepad2.html).
1. Open Ren'py. Wait for it to run. It takes a while.
 a. Click preferences
 b. Change Text Editor to "System Editor"
 c Click return to get out of the preferences.
 text editor preferences.png
1. Click on "script.rpy". On Windows, you should get a dialog for setting the program to run when .rpy files are opened. Find your IDE. If you can't find your IDE, expand the dialog box and navigate to your IDE's executable.
 rpy association.png
1. Click on "script.rpy" again. It should open up your IDE.

# Creating your first project

1. Click on Create New Project. If this is the first time you run ren'py, it will ask you where you would want to put your project files. Select a directory.
1. For project name, call it "PyCon APAC". Just select the default resolution and choose a color scheme you like. You can change these properties later in options.rpy.
1. Make sure that "PyCon APAC" is highlighted on the projects list. Click on "script.rpy"
projects select.png

# Creating your first visual novel

1. Select all the text in "script.rpy". Delete them all. We will not be using this for our first visual novel
1. Type in the following:

[code]
label start:
    "Hello World"
    return
[/code]

1. Run the project. Take note that the indentation uses space and not tabs.

Explanation:
> label start:  # this is the entry point for the visual novel
> "Hello World" # its obvious, but try to explain to yourself what this line does.
> return        # this exits the game

1. Once you understand the above code, make this modification:

[code]
label start:
    "Your name" "Hello World"
    return
[/code]

Change "Your name" to your real/fake name. Try to explain to yourself what adding this does.

...

Explanation:

"Hello World" by itself shows the narrator [1] speaking the words. By adding a string to the left side, we can have a character speak the words.

[1] traditionally, in visual novels, an unnamed voice comes from the narrator.

1. It can be inconvenient to hardcode the names of your characters. What if we have a long script and need to change the name of one of our characters? In ren'py, we can make variables

[code]
define r = Character("Your name")

label start:
    r "Hello World"
    return
[/code]

Like variables in programming, you can name your variables with anything you want.

1.

[code]
define r = Character("Your name")

label start:
    r "I am happy"
    return
[/code]

Run the above program. Now, while the game is still running, go back to the editor and do the following modifications:

[code]
define r = Character("Your name")

label start:
    r "I am shocked"
    return
[/code]

Go back to the running program. No surprise, the text still reads "I am happy". Now, press Shift+R. This should reload the script and change the text. This is how you reload your game so you can immediately see the changes.

1.

[code]
define r = Character("Your name")

label start:
    r "I am shocked"
    r "What is that?"
    return
[/code]

Run the above program. In visual novels, to go to the next dialogue, either press any key or click on the screen. To go back to the previous dialogue, press PgUp or mouse scroll up.

1.

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    r "I am shocked"
    r "What is that?"
    return
[/code]

Run the above program. This adds a background called black. "with fade" is a command to transition from one scene to the other. There are other examples of transitions that you can look at the online manual

1.

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    show firstname sad
    r "I am shocked"
    r "What is that?"
    return
[/code]

Add the line above but change "firstname" to your own first name (small letters).

The show command is how you present a character to the player. You might notice that the character is a blank paper doll. This is the default image for characters in ren'py. 

Tip: When making games, one of the excuses I heard is that people need to have the BEST art before doing work on the game. This default paper doll image can be used while your game script is being developed.

1. Time to add some images. Go back to the projects selection and click on the images directory.

images folder select.png

Go to the Internet and find images for one background and one character. Save the two images in the image directory (you can use png, jpg or jpeg) and name them "bg black" and "firstname sad" (again, use your own first name).

images folder view.png

Run the game. If nothing went wrong, you should be able to see both images.

Try to explain to yourself how scene and show works with images.

1. You might have noticed that the character image is at the bottom of the screen. We can change the position with the "at" keyword:

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    show firstname sad at top
    r "I am shocked"
    r "What is that?"
    return
[/code]

There are other locations that can be used such as center and truecenter. You can check them out in the manual.

1. Let's add a new character

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    show firstname sad at top
    r "I am shocked"
    r "What is that?"

    show villain at left
    with moveinright

    "villain" "BWAHAHAHA"
    return
[/code]

Based on what you've learned, try to explain to yourself the newly added lines. Explaining things to yourself is helpful when learning something new

1. Now let's add a decision for the player:

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    show firstname sad at top
    r "I am shocked"
    r "What is that?"

    show villain at left
    with moveinright

    "villain" "BWAHAHAHA"

    menu:
        "What should you do?"
        "Dodge":
            jump dodge_ending
        "Don't Dodge":
            jump bad_ending

label dodge_ending:
    "Good ending"
    return

label bad_ending:
    "Bad ending"
    return
[/code]

"menu" is the keyword to add user interactivity. "jump" will bring the user to the label somewhere in the script (script management is something you need to learn if you started working on long scripts. But as a beginner, I recommend starting small).

Reminder that "return" exits the program.

1. Hiding characters and adding special effect

[code]
define r = Character("Your name")

label start:
    scene bg black
    with fade

    show firstname sad at top
    r "I am shocked"
    r "What is that?"

    show villain at left
    with moveinright

    "villain" "BWAHAHAHA"

    menu:
        "What should you do?"
        "Dodge":
            jump dodge_ending
        "Don't Dodge":
            jump bad_ending

label dodge_ending:
    hide villain
    with dissolve
    "I am just your imagination"
    return

label bad_ending:
    hide firstname
    with vpunch
    "UWAAAHHHH"
    return
[/code]

Finally, the "hide" command will remove a character from the screen. vpunch should be a nice surprise for you.

# what's next?
1. For your next project, I suggest starting with a simple 3-act story. The 3 acts will be the introduction, the conflict, and the resolution.
1. First think of a genre. It can be romance, horror, action, or anything you want. Romance is one of the easier genres to write.
1. Next think of 3 location for each act.
1. The first act will be the introduction of 3 characters: the hero, the villain, and the supporting character (or second love interest in most romance stories)
1. The second act will be the conflict. Make the story on how the conflict happens
1. The final act will be all about the resolution. How should the story end? What decisions will lead to the different endings?

# Recommended reading
1. Run the Tutorial project. It contains a lot of examples including how to play movies, add minigames using pygame, inputs from other players, different transitions, and custom animation.
1. Run The Question. This is a simple visual novel to demonstrate how to make a simple game. You can look into the source code and learn how they made the game.
1. You can look for examples of transitions and positions in the Tutorial project and in the documentation manual (found at the bottom-left of Ren'Py)

documentation.png

# Common issues
1. Ren'py exclusive use spaces for indentation, not tabs. It will complain if you used tabs. Your IDE should have an option to convert tabs into spaces.


# End

Good luck and I hope to play your visual novel someday.