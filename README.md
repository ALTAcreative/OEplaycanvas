# Play Canvas intergration with Origami Engine

Here are the 3 main issues connected to the iOS/Android repos that discribe the basics of what we want to achieve.

**Issue 345  
This is to be able to add WebGL via playcanvas tool to Origami Engine. I'm looking for tight integration between the two.

We want to be able to export the files from playcanvas and just add them right into Origami Design. This is the most basic part. PlayCanvas or WebGL by default needs an internet connection. We need to be able to set it up so that when in OE, it does not need an internet connection.  

I want to be able to declare triggers/behavioris in playcanvase and give them names. then be able to read those names in Origami Design. This way we can build gui in OD that can contorl parts of the play canvas system.  

Play Canvas has the ability to add JS files to it's system. I suggest we have a JS files that makes it easy for OD to find predefined states or behaviors and it exposes them to the OE trigger system.  

Going the other way is something else. Being able to send trigger URLs to OE in a different thing. I guess in theory it should be easy but i don't know really how we would do it. We need to discuss it.


**Issue 368  
This is to be able to define events in a OE specific way so that OE can see them and expose them in a trigger panel in OD. This will then allow us to fire triggers that cause something to happen inn the specific play canvas.  

In the same way that a touch event can cause something to happen in play canvas we will have events coming from OE to cause the firing of events in Play Canvas.  

I expect this will require some OE specific coding/JS/behavior to be written in the play canvas project.  

I'm not sure how events work in play canvas or JS. I'm basing by throughts on how you define functions in PHP. Then you can expose those functions and the parameters you can pass to them.  


**Issue 369  
This is basically the opposite of #368 Here you can find the Play Canvan object in the target dropdown and under that are all of the events you can. In a JS file you will define these elements and specify the way you can affect them (basically passing a variable to them connected to the trigger.  
