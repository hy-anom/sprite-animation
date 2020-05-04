# sprite-animation


Sprite is from a game called "Braid" it's an amazing platformer-puzzle game with an ability to rewind the time itself! Absolutely a must play if you haven't.

extracted by
Simon Frost 

https://medium.com/@simonhfrost/pixi-js-sprite-animation-1546867f64ae


## how to make it?

The method I used is quite simple. Have a look at this snippet.


```CSS
.sprite {
  width: 74.5px;
  height: 86px;
  margin: 2em auto;
  background: transparent url('./bride-sprite.png') 0 0 repeat;
  animation: bridewalk-v 0.3s steps(7) infinite,
  bridewalk-h 1.2s steps(4) infinite;
}

```

First locate the spritesheet and load it as background image and put it on top left position.

Then give our animation it's dimensions. You can get it by measuring the width and height of a single sprite frame using this formula.

```frame width = spritesheet width / amount of frame column```
```frame height = spritesheet height / amount of frame rows```

You might want to adjust by a few pixels. And then if everything gone well, you should be able to see a perfectly placed single frame. 


Next for a bit tricky part, is the animation. Since our spritesheet is in 2 dimension we need to 'move' it in two direction right and down. Let's go!


```CSS
.sprite {
  animation: bridewalk-v 0.3s steps(7) infinite,
  bridewalk-h 1.2s steps(4) infinite;
}

@keyframes bridewalk-v {
  100% {
    background-position-x: -522px;
  }
}
@keyframes bridewalk-h {
  100% {
    background-position-y: -344px;
  }
}
```

As you can see on the snippet above, you might think 'where are the numbers come from?'. So this is where the numbers come from.

First is to animate the sprite vertically hence I named it `bridewalk-v`. There are two basic elements in animation, how many frames does it have, and how long to complete the whole sequence.
For how many frame do we have, it's clear that we have 7 frame (vertically). And for how long to complete, first decide how many fps this animation will be. For example if want your animation at 25fps, you can calculate it like this ```vertical animation duration =  number of frames / frames per second ``` . 

Then the keyframe part it may or may not the same as the width of the spritesheet though but it's quite close usually just few pixels apart. So just to be safe use this formula ```keyframe background position = frame width * number of steps```. and since we basically 'move' the sheet to left therefore, make the number negative.


Next part is how do we select the next row. Basic principle is remain still the same as above, replace ```width``` with ```height```. EXCEPT for animation duration being ```horizontal animation duration = time to complete vertical animation * number of horizontal steps```.


#TLDR aka Summary

```CSS
.sprite {
  width: $frameWidth = $spriteSheetWidth / $frameColumns
  height: $frameHeight = $spriteSheetHeight / $frameRows

  background: transparent url('./bride-sprite.png') 0 0 repeat;

  animation: 
    bridewalk-v 
    infinite 
    $verticalDuration = $frameColumns / $preferedFPS
    steps($frameColumns),
    bridewalk-h 
    infinite
    $horizontalDuration = $verticalDuration * $frameColumns
    steps($frameRows);
}

@keyframes bridewalk-v {
  100% {
    background-position-x: -($spriteSheetWidth);
  }
}
@keyframes bridewalk-h {
  100% {
    background-position-y: -($spriteSheetHeight);
  }
}
```


