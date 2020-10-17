---
layout: single
title: "./mouse-scroll.sh"
date: 2020-7-15
# categories: creative-coding
permalink: /mouse-scroll/
header:
  # image: /assets/post-assets/generative-spirals/1.png
  overlay_image: /assets/post-assets/mouse-scroll/Screenshot at 2020-10-17 01-45-29.png
  # show_overlay_excerpt: false
  teaser: /assets/post-assets/generative-spirals/1.png
  tagline: 



---


I love linux but it has it's quirks.

And these quirks that can potentially throw someone into an existential dread. One such instance occured when I left from college for my mid term break with nothing but my laptop and a change of clothes, assuming that I'll be back 3 days later and life will go back to normal. But oh how things turn out. Pointing out the obvious, first case of COVID-19 hit noida the very same day and rest as we say.. is history (?? never ending reality ??).

Besides leaving everything: all my clothes, items and my life in my dorm room I also left my wireless mouse that I had been using for about 3 years. After not being able to work effectively with the touchpad, I managed to convince my brother to share his. However that involved removing the reciever time and again each time The Great Mouse Exchange took place. But where is the problem in that, you might ask?

Linux Mint, by default has natural scrolling enabled which contrary to the name is not the way one would naturally scroll using a mouse. Manually disabling it takes about 2-3 minutes each time since the variables tend to after each instance. After a week of manually disabling it each time in agony, I decided to do what every lazy person would do: automate it.

This also provided a nice way for me to learn some bash scripting and feel some command lines heroine vibes for about 2 seconds(till the next bitersweet quirk :p) 

Here is a short bash script that made me learn a lot and made a life a little bit simpler :)

```
#!/bin/bash
set -x 

x=$(xinput | grep -i "Logitech Wireless Mouse" | awk '{print $6}' | cut -b 4-5)
 
y=$(xinput list-props $x | grep -i "libinput Natural Scrolling Enabled (" | awk '{print $5}' | cut -b 2-4)

xinput set-prop $x $y 0

echo "done"
```