# node-red-hue-api.v2-flows

Hey,

this small respository is actually just an Example Flow.
It includes everything you need to communicate with your HUE-Bridge directly using https-request via API V2.
You wont be dependent on badly maintined contribs anymore, controlling your lamps.

Thanks to user ralfhille, who created the header node!

Sorry if this does not look very professional here, its my first repository :)


This flow just needs a very cool contrib, that need zero maintainance! 
------------

https://github.com/yadomi/node-red-contrib-philipshue-events

Thanks to yadomi making this one!

Before importing my Flow, it is important to install yadomi´s contrib first!
--------------------------------------

Just import the Data from the HUE API V2 HTTP REQUEST.json into a new Flow Tab

The Flow has a lot of Comments, it should be easy to figure everything out.
Depending on how much lights you have, this can take a reasonable amount of time to set it up...
But believe me, its absolutely worth it!

First you need to fill in your Data in the Nodes, after that you need to discover your device ID´s and RID´s.
You are doing this using the specific Inject Nodes for the Endpoints you want to disscover, then unfold the whole payload.
The Name of everthing you have given in the App, will be in the Metadata payload, so you know, which ID you just discoverd.

I attached some pictures how the payload looks like.

It would make me happy if some of you could end your struggle with not working contribs!

If you need help, pull a request or start a discussion, Thanks!



Lamps:
-------

![light](https://user-images.githubusercontent.com/76150626/173955018-5741e7fb-ef3d-42c7-8629-99135bcef0ab.PNG)

-----------------------------------------------------------

Rooms/Zones:
------------
![rooms](https://user-images.githubusercontent.com/76150626/173955041-0097529e-0e40-4473-b7d4-28fe3282b258.PNG)

-----------------------------------------------------------

Motion:
------------
![motion](https://user-images.githubusercontent.com/76150626/173955078-c922dcb2-ad4c-4501-b574-07f4d8da416a.PNG)

-----------------------------------------------------------

Scenes:
------------
![scene](https://user-images.githubusercontent.com/76150626/173955095-50fd8649-7bf1-4074-bd7f-7624cbffb7c6.PNG)
