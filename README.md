# temple-game-v3!
name: Ren'Py setup          
  uses: Ayowel/renpy-setup-action@v2.0.1 
# link to powerpoint overview of game and issues we had: 
# link to game play: [https://share.icloud.com/photos/01aAbq9do2EYcWQAyu1SIwuFA](https://youtu.be/TSZI67vG6bA)
define e = Character()

define pov = Character("[player_name]")  
define professor = Character ("Professor [Professor]")
define narrator = Character("Narrator")
define Canvas = Character("Canvas")

default currentgpa = 3.0
default maxgpa = 4.0

default currenthunger = 25
default maxhunger = 50
label start:
play music "bgmusic.mp3" loop
screen gpabar:
    text "GPA: [currentgpa]/[maxgpa]" xalign 0.0 yalign 0.05 color "#FFFFFF"
    bar value currentgpa range maxgpa xalign 0.0 yalign 0.1 xmaximum 200

scene bg uni copy
narrator "Hi, in this game, you will be playing as a student here at Temple University! Please enter your name to get started."



$ player_name = renpy.input("What is your name?")  

narrator "Hello [player_name], welcome to Temple Univerity! Please choose what you want to major in during your stay here."

menu:
        "Finance":
            $ major = "Finance"
            play sound "select.mp3"
            "Great choice!"

        "Computer Science":
            $ major = "Computer Science"
            play sound "select.mp3"
            "Oh, ok choice!"

        "Art History":
            $ major = "Art History"
            play sound "select.mp3"
            "Fun choice!"

        "Psychology":
            $ major = "Psychology"
            play sound "select.mp3"
            "Interesting choice!"

        "English":
            $ major = "English"
            play sound "select.mp3"
            "Cool choice!"

show screen gpabar
narrator "Up on the right-hand corner, you will see a GPA bar. Depending on how well you do on your assignments and exams, your GPA can go up or down!"

narrator "Your all set [player_name] to start your college life! Good luck!"
jump after_menu
label after_menu:

if major == "Finance":
    $ Professor = "Ofra Bazel"
    $ Class = "Financial Management 3101"
elif major == "Computer Science":
    $ Professor = "Andrew Rosen"
    $ Class = "Introduction to Python 1051"
elif major == "Art History":
    $ Professor = "Shinya Watanabe"
    $ Class = "Arts of Asia 1801"
elif major == "Psychology":
    $ Professor = "Peter James"
    $ Class = "Critical Thinking in Psychology 1004"
elif major == "English":
    $ Professor = "Madelyn Winkler"
    $ Class = "Interpreting Literature 2001"

scene black with dissolve
play sound "c.mp3"
$ renpy.pause(1)
scene dorm

narrator "Hurry, wake up! Its finally your first day at Temple University."
narrator "Your day looks packed, yikes. Your first class of the day is [Class] with [Professor]."
narrator "Do you want to attend your first class of the semester or do you want to skip since they might only review the syllabus?"
menu:
    "Attend first class of the day":
        play sound "select.mp3"
        "Great choice!"
        stop sound
        jump attend_class
    "Skip first class and sleep in":
        play sound "select.mp3"
        "risky choice..."
        stop sound
        jump skip_class

label attend_class:
    scene lecture hall
    narrator "You are currently in your first class of the day."
    narrator "Professor [Professor] welcomes you all in with a big smile!"
    Professor "Welcome to [Class]! I'm sure you all had read our syllabus before class, as I stated in the announcement I sent out. You will need it for the syllabus quiz we will be taking today :)"
narrator "There was a syllabus quiz as soon as you walked in! Thankfully you didn't decide to skip class!"
$ currentgpa += .5
narrator "Your GPA increased by .5! Your current GPA is [currentgpa]."
jump lunch_break

label skip_class:
scene black with fade
narrator " You decided to skip your first class and sleep in instead. "
$ renpy.pause(1)

scene dorm with dissolve
narrator "You wake up feeling nice and refreshed. You realize you have a notification on Canvas from [Class], which was the class you skipped."
Canvas "Syllabus Quiz: %%0"
narrator " You received a ZERO for a syllabus quiz the professor gave!!!"
play sound "dundundun.mp3"
$ currentgpa -= 1.0
narrator "You GPA went down 1.0! Your current GPA is [currentgpa]."
jump lunch_break

screen hungerbar:
        text "Hunger: [currenthunger]/[maxhunger]" xalign 1.0 yalign 0.05 color "#000000"
        bar value currenthunger range maxhunger xalign 1.0 yalign 0.1 xmaximum 200

label lunch_break:
show screen hungerbar
scene lunchroom
narrator "Up on the right-hand corner, you will see a Hunger bar. If you skip breakfast, lunch or dinner too often you might experience some health issues."
narrator "Would you like to go back to your dorm and relax until your next class or eat lunch?"
menu:
    "Eat lunch":
        narrator "Where do you want to eat lunch?"

        menu:
            "chic-fil-a":
                narrator "The fries were nice and fresh YUM!"
                play sound "select.mp3"
                $currenthunger += 10
                jump after_lunch
            "Wingstop":
                narrator "You had to wait 40 min for your wings! It was delicious though."
                play sound "select.mp3"
                $currenthunger += 10
                jump after_lunch
            "second halal cart":
                narrator "Best chicken over rice you've ever had!"
                play sound "select.mp3"
                $currenthunger += 10
                jump after_lunch
            "Honey Truck":
                narrator "Looks delicious!"
                play sound "select.mp3"
                $currenthunger += 10
                jump after_lunch
            "Eat your packed lunch":
                narrator "Great way to save your money!"
                play sound "select.mp3"
                $currenthunger += 10
                jump after_lunch

    "Go back to your dorm instead":
        play sound "select.mp3"
        narrator "your stomach ended up growling non-stop. You lost 20 hunger points!"
        play sound "dundundun.mp3"
        $currenthunger -= 20
        jump after_lunch
   
label after_lunch:
scene club with dissolve

if major == "Finance":
    $ Professor2 = "Tom Intoccia"
    $ Class2 = "Investing for the Future 0822"
elif major == "Computer Science":
    $ Professor2 = "John Fiore"
    $ Class2 = "Program Design and Abstraction"
elif major == "Art History":
    $ Professor2 = "Ariel Pearce"
    $ Class2 = "The Art of Sacred Space 0803"
elif major == "Psychology":
    $ Professor2 = "Melissa Auerbach"
    $ Class2 = "Self-Regulation in Health Behaviors 3012"
elif major == "English":
    $ Professor2 = "Cara Adams"
    $ Class2 = "Creative Writing 2005"

narrator "You just received a message from your best friend asking if you want to go out but it's time for class right now..."
narrator "Are you going to choose class or your friend?"
menu:
    "Attend class":
        play sound "select.mp3"
        "Great choice!"
        jump attend_class2
    "Skip class to hang out with best friend":
        play sound "select.mp3"
        "have fun!"
        jump skip_class2
label attend_class2:
scene lecture hall
narrator "This professor has the best ratemyprof ratings!"
Professor2 "Today is going to be a chill day. We will just be going over the syllabus and any questions you may have about this course!"
Professor2 "Before we begin, I'm going to have you all just check in on canvas attendance as attendance is mandatory for this class."
menu:
    "CHECK IN":
        play sound "select.mp3"
        "good job!"
        $ currentgpa += .5
        narrator "Your GPA went up .5! Your current GPA is [currentgpa]."
        if currentgpa > 4.0:
            $currentgpa = 4.0
        jump Class3

    "forget to check in":
        play sound "select.mp3"
        "Oh no!"
        $ currentgpa -= 1.0
        if currentgpa<= 1.0:
            play sound "dundundun.mp3"
            "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
            jump you_lost
        narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."
        jump Class3


label skip_class2:
scene dorm
narrator "You just returned back to your dorm after hanging out with your friend. You suddenly receive a notification of a new grade inputted on Canvas from none other than [Class2]"
Canvas "Attendance: 0/1"
narrator " You didn't realize the class had mandatory attendance! Your first grade in that class is a zero%% now :("
play sound "dundundun.mp3"
$ currentgpa -= 1.0
narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."
if currentgpa<= 1.0:
    play sound "dundundun.mp3"
    "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
    jump you_lost
jump Class3
    
label Class3:

scene dorm
$Professor3 = "Micheal Neff"
$Class3 = "Intellectual Heritage 1 0851"

narrator "Its time for your third and final class. But the show your watching just ended on a serious cliffhanger! Do you want to skip class and watch the next episode or force yourself to go to class?"
menu:
    "Attend class":
        play sound "select.mp3"
        "Great choice!"
        jump attend_class3
    "Skip class and watch the next episode":
        play sound "select.mp3"
        "Enjoy!"
        jump skip_class3

label attend_class3:
scene lecture hall
narrator "This professor is supposedly really tough! Make sure to pay attention!"
Professor3 "Hello class, welcome to [Class3]. I assume you all have read your syllabus already before class as that is expected. So let's dive right into today's lesson."
Professor3 "Philosophy is the study of the fundamental nature of knowledge, reality, and existence"
Professor3  "An easy way to remember the meaning of Metaphysics is to know it basically means 'before physics'!"
Professor3 "We will continue learning more about the divided line theory next week! But before you leave today, please complete the lecture 1 quiz on Canvas! Good luck."
narrator "The only question on this quiz is..."
"What is the meaning of Metaphysics?"
menu:
    "Before physics":
        play sound "select.mp3"
        "great job!"
        $ currentgpa += .5
        narrator "Your GPA went up .5! Your current GPA is [currentgpa]."
        if currentgpa > 4.0:
            $currentgpa = 4.0

    "Matter and motion":
        play sound "select.mp3"
        "Oh no, you got it wrong! you should've paid attention in class!"
        play sound "dundundun.mp3"
        $ currentgpa -= 1.0
        if currentgpa<= 1.0:
            play sound "dundundun.mp3"
            "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
            jump you_lost
        narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."

    "After physics":
        play sound "select.mp3"
        "Oh no, you got it wrong! you should've paid attention in class!"
        play sound "dundundun.mp3"
        $ currentgpa -= 1.0
        if currentgpa<= 1.0:
            play sound "dundundun.mp3"
            "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
            jump you_lost
        narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."

    "Physical Sciences":
        play sound "select.mp3"
        "Oh no, you got it wrong! you should've paid attention in class!"
        play sound "dundundun.mp3"
        $ currentgpa -= 1.0
        if currentgpa<= 1.0:
            play sound "dundundun.mp3"
            jump you_lost
        narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."

jump after_class3

label skip_class3:
scene dorm
narrator "You watched the best episode of the season!"
narrator "You received a notification from Canvas about [Class3]. You received a 0%% on a Quiz!"
play sound "dundundun.mp3"
$ currentgpa -= 1.0
if currentgpa<= 1.0:
    play sound "dundundun.mp3"
    "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
    jump you_lost
narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."

jump after_class3

label after_class3:
scene dorm
narrator "You're nice and tucked in under your covers about to start a movie with your roommate. You still havent eaten dinner... do you want to make yourself a quick pasta?"
menu:
    "Yes":
        narrator "That hit the spot!"
        play sound "select.mp3"
        $currenthunger += 10
        jump after_dinner
        
    "No":
        narrator "If you say so..."
        play sound "select.mp3"
        $currenthunger -= 15
        if currenthunger<= 0:
            "OH NO! You haven't eaten properly and fainted as a result. You are being rushed to the Hospital!"
            scene hhh
            play sound "heart_rate.mp3"
            narrator "After spending a couple of hours at the hospital, you were able to leave."
            stop sound   
        jump after_dinner

label after_dinner:
scene dorm
narrator "You have a homework assignment due tonight. Are you going to work on it?"
menu:
    "Yes":
        play sound "select.mp3"
        "great job!"
        $ currentgpa += .5
        narrator "Your GPA went up .5! Your current GPA is [currentgpa]."
        if currentgpa > 4.0:
            $currentgpa = 4.0
        jump the_end
    "No":
        play sound "select.mp3"
        "Oh no! The teacher doesn't accept late assignments. You got a 0%% for it"
        play sound "dundundun.mp3"
        $ currentgpa -= 1.0
        if currentgpa<= 1.0:
            play sound "dundundun.mp3"
            "OH NO! Temple University has sent you a letter of dismissal because your GPA has dropped to a [currentgpa]."
            narrator "Your GPA went down 1.0! Your current GPA is [currentgpa]."
            jump you_lost

label the_end:
narrator "You survived your first day at Temple University as a [major] student. Great job! But remember, today was only the first day... you still have a whole semester in front of you. Good luck!"
scene underc
$ renpy.pause(3)
return

label you_lost:
scene gameover
$ renpy.pause(3)
return
