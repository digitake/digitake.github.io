---
layout: post
title:  "How to create sprite frames dynamically in Phaser"
date:   2016-06-22 20:19:00 +0700
categories: PhaserJS, GameDev
---

Note: I use v2.5.0 at the time this article is written.

Today, I spent one hour to figure it out how to create a spritesheet programmatically.
Because most of examples use pre-generated files and load it to memory. However, when you want to
generate sprite frames, you have to do following steps:

* Generate a spritesheet and add it to cache for later use
    1. Create bitmapData with width = frameWidth*<totalFrames>
    
            // For example, I want to generate a spritesheet with two frames and draw white and black circle on each.
            var width = r*2;
            var height = r*2;
            var bmd = game.add.bitmapData(width*2, height);  //Create empty canvas.    

    2. Draw the image to each frame
        
            //Draw circles
            bmd.circle(r,r,r, '#FFFFFF');        // White
            bmd.circle(r*3,r,r, '#000000');      // Black (note that r*3 is the circle's x-origin of the second frame

    3. Add bitmapData to cache for later use.

            //Add the spritesheet to cache, first param is the sheet's name aka 'spriteKey'.
            //Second param is the path to asset which is null because we generate them in this case.
            //Third is the canvas of bitmapData
            //The last param is a number of frame.
            game.cache.addSpriteSheet('mySpriteKey', null, bmd.canvas, width, height, 2);
    
* Use the generated spritesheet
    1. Create sprite with the spritesheet's key
    
            mySprite = game.add.sprite(0, 0, 'mySpriteKey');
    
    2. Alter the frame
    
            mySprite.frame = 1; // Change to second frame
            mySprite.frame = 0; // Change back to the first frame(index start with 0)
            
At this point you should be able to use and alter the frame for your generated sheet.