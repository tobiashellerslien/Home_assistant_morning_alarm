# Home assistant morning alarm
A morning alarm made in home assistant.

# Introduction
I made this because I wanted to use home assistant for my alarm, so that I can set it on my smart display. The lights will then gradually turn on, with an automation from [this](https://community.home-assistant.io/t/wake-up-light-alarm-with-sunrise-effect/255193) blueprint. Then, a song of my choice will play from my google nest mini.

You set the alarm time using input_numbers for hour and minutes. This is then combined into a timestamp, which is used to trigger the alarm automation. I have 2 alarms: 1 main alarm and an optional backup alarm. The backup alarm uses 1 input_number to tell how many minutes should pass from the main alarm to the backup alarm.

# Setup
This was made using multiple helpers. I am sure many of them can be combined togehter, but I haven't bothered changing them after I got it working. You will need a smart speaker (I have a Google Nest mini, that home assistant casts the audio to) and some mp3 files of alarm songs you want. The .yaml files for the template sensors are found above. **Remember to change the sensor names to the correct ones for you.**

### 1. Create input_numbers
Two for the main alarm (hours and minutes) and one for the backup alarm. I have set the step size to 5.

### 2. Create the combining template sensor
This will combine the two input_numbers to a HH:MM format output. Use the .yaml code above

### 3. Create the alarm date template sensor
This takes in the HH:MM from the previous sensor and returns the date for this time the next day. The unit class needs to be "date".

### 4. Create the timestamp template sensors
This will take in the outputs of the two previous sensors, and return a timestamp for when the alarm should go off. Create two with the .yaml files above, one for each alarm. The template sensors needs to be set to "timestamp" under unit class.

### 5. Create input_boolean to turn both alarms on or off

### 6. Music
Import some .mp3 files of the songs you want for your alarm into the media folder in home assistant. Make input_select for both alarms, and add all the filenames with the .mp3 to the list.

### 5. Create the automation
I made it so the sunrise alarm from the blueprint above uses the alarm timestamp. Then, as post-sunrise actions, I call the play_media action on my google nest with the template from the .yaml file above. It then plays my chosen song (often a calm one for the first alarm). I also trigger a script that gradually increases the volume. I then created a second automation, that plays the backup alarm song (often a more intense song) at the backup alarm timestamp. Make sure these automations are controlled by the input_booleans as well.

### Extra
I also created a script that plays the correct season of Vivaldis "Four seasons" based on the actual season. I used the season sensor for this.

# Showcase
In my smart display, it looks like this:
![In my smart display, it looks like this:](https://github.com/user-attachments/assets/642c689e-1ba7-48e1-ba63-7a1bdf580960)
Use the .yaml code above on a template card to create the card that shows how it is before the alarm goes off

