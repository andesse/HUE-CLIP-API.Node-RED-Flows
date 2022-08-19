![IMG_2180](https://user-images.githubusercontent.com/76150626/174133694-50b4d23b-7ee6-42a3-8d64-24de60890dde.jpeg)

# hue-clip-api.node-red-flows


Please read the whole readme before use!
---

Version 4.0 Update Info below

This respository is an example Flow how to communicate with the HUE-Bridge API V2 over https request  
It includes everything you need to communicate with your HUE-Bridge directly using https-request via the restful API V2 (CLIP API)
You wont be dependent on badly maintained contribs anymore. It has example nodes that can directly edited and used for your flow.

With Version 3.1 this is almost as easy to setup like some contribs that are available.
I am assuming a setup with 1 bridge, 30 lights, 4 motion sensors, 5 buttons, 25 scenes can be done in under 2 hours.
Dont be afraid, replace step-by-step, it will be easy. :)

Thanks to user ralfhille, who created the header node and the concept!


This flow has one contrib, that need zero maintainance! 
------------

https://github.com/yadomi/node-red-contrib-philipshue-events

Thanks to yadomi making this contrib!

Before importing my Flow, it is important to install yadomi´s contrib first
---
DEPLOYING THE FLOW WITHOUT THIS CONTRIB CAN LEAD TO A RESTART & BOOT LOOP OF YOUR NODE-RED!
---

Import the Data from the :arrow_right: ***HUE-CLIP-API_Node-Red-Flows.json*** :arrow_left: into a new Flow Tab, AFTER YOU READ THE FULL README!
                              
The Flow has a lot of Comments, it should be easy to figure everything out.
Depending on how much lights you have, this can take a reasonable amount of time to set it up...
But believe me, its absolutely worth it!

First you need to fill in your Data in the Nodes, after that you need to discover your device ID´s and RID´s.
This works using the specific inject Nodes for the Endpoints you want to discover, then unfold the whole payload.
The Name that you have given in the App for Lights, Rooms, etc., will be in the Metadata payload, so you know, which ID you just discoverd.

The additional files in this repository contain seperately the Sub-Flows, Change-Nodes, Helper Flow, a "get state" node and a different header node. These are already included in the main File. It might come handy to import these when you downloaded a previous release.

Github User marc-gist made a really nice concept for a "helper flow" that makes it easier to discover ID / RID. It's parsing the event-stream payload into a better format. The flow link in Node need to be connected to the http node. It is included in the updated main Flow and can also downloaded seperately. (helper_functions_flow_v2.json). I have attached a picture how it looks like and replaced the main picture as well. Thanks Marc!

Colors get more complicated. These are x/y values now. 
To determine the right value I recommend to change the color in the app and watch the Event stream.
Open the color payload until you find the x/y values and use these. 

Recommendation:
In general I recommend to trigger scenes and not controlling seperate lamps. The Bridge is just able to receive max! 5 light / 1 group request per second, less is better. Use delay Nodes in 200-400ms range if you might have a situation, that the http node returns an error.
Another recommendation is to setup your whole HUE System in one Flow Tab, using Link out/in Nodes to create connections to your Rooms. 
>> LABEL your Link in/out Nodes, otherwise it will be too confusing. ;)



I attached some pictures how the flows / payload / xy Color look like / helper function flow v2 / a screenshot of my own setup

For a full API Documentation you could create an Account at: https://developers.meethue.com/

Hope this ends the struggle with your HUE Setup. 
Mine runs completly zero issue since i made it, no trouble with my wife anymore. :sweat_smile:

If you need help, pull a request or start a discussion, Thanks!


Version 4.0 Update: (files have a V2 prefix)
---
User Fred.Blo created a new approach to setup this flow concept.

>If you have it already running with the initial release (up to v3.4), there is not much need to make these changes.

This will make it probably more easy to set it up initially. It also helps to have a cleaner looking Flow. There is one part of the Flow, that can be added seperately. It is an error handling mechanism for the Bridge timeout, "Event_Sender". 

>Using this new setup, it is very important that you can save context as file! Otherwise you should use the Header Function Node from the initial release! 

> 2 new Files:
> - V2_HUE-CLIP-API_Node-Red-Flows_Fred.Blo.json
> - V2_HUE_Event_Sender.json


- Existing Subflows (Light, Button & Motion Sensor receivers) are now 'configurable' for easier integration in existing system
  • ID / RID is set in insert node config
- New subflow added 'Light Sender' to send commands to lamps easily, using node config :
  • ID / RID is set in inserted node config
  • type of light (light point or group of light)
- The 'bridge link' (receiver & sender) was revamped:
  • single centralized grouped nodes for all calls
  • handles 'overflows of calls' (i.e. when the HUE bridge refuses calls because it rate is > 5/sec, they are queued for repeat)
  • a return value is sent to allow continuing the flow after command was sent
- removed / merged the 'technical' subflows (only used in configuration part to find the ID's / RID's
- A bit of 'UI'
  • Re-organized nodes in groups to make it easier reading / configuring / accessing
  • Some comments are directly readable without opening them (i.e. double click on it)
  • added output names to subflows to easily know what to expect as output when reading flow using such nodes (without having to open subflow)

V2_HUE-CLIP-API_Node-Red-Flows_Fred.Blo.json
![IMG_2573](https://user-images.githubusercontent.com/76150626/185602553-eb6f75fc-3c3c-4097-80da-adafb1bb4f51.jpeg)

V2_HUE _Event_Sender.json
![IMG_2575](https://user-images.githubusercontent.com/76150626/185602590-88ba71d4-9aca-4250-9858-ef5c053bff66.jpeg)




Version 3.4 Update:
--
Motion Sensor Behaviour Flow added, for Sensors that have no configuration. It will trigger Scenes, dim down, and turn off rooms.
Descriptions in the Flow labels.

Version 3.3 Update:
--
Alarm Flow added to flash a light red for 5 seconds. It will return to previous state.
README included in the Flow as usual. Have Fun!

Version 3.2 Update:
--
New File "SSE_Event_Stream.json"

This flow can replace the node from "@yadomi/node-red-contrib-philipshue-events"
First you need to Install the contrib "node-red-contrib-sse-client" before deploying this flow.
All other Informations are in the Labels of the Flow itself. (Double Click)

If you don’t have any problems with yadomis contrib, there is no need to replace it.
You can still download this as a backup or try it out.


Version 3.1 Update:
--
This version comes with an upgraded "Helper Function Flow"
It let you easily discover:

- Room IDs / RIDs
- Zone IDs / RIDs
- Lamp IDs
- Motion Sensor IDs
- Button IDs

These are stored in context (default) until they are overwritten or erased.
With another Flow additional included, you can recall all these Informations as an array, or seperately.


Main Flow:
------------
![HUE-CLIP-API_Node-Red-Flows](https://user-images.githubusercontent.com/76150626/174495403-8744d481-e0d6-40d5-8497-0bf7abebe022.PNG)


-----------------------------------------------------------

Sub-Flows:
---
![subflows](https://user-images.githubusercontent.com/76150626/174089869-b67e6d15-8ba7-4ab2-8b22-57a2dc43b39e.PNG)

------------------------------------------------------------

Action Change Nodes:
---
![change nodes](https://user-images.githubusercontent.com/76150626/174089961-f4e00eb9-8726-44b9-8d44-d422000f133e.PNG)

-----------------------------------------------------------

Helper Functions for RID / ID discovery (concept by user marc-gist - THANKS!)
---
![helper_functions_flow_v2](https://user-images.githubusercontent.com/76150626/174495416-dbb394b5-c012-482c-a119-eb16cd073171.PNG)


SSE_Event_Stream:
---

![IMG_2261](https://user-images.githubusercontent.com/76150626/176202424-8f7e53db-bb9a-41aa-8ce4-c71f1b153fa5.jpeg)


Alarm Flow:
---
![alarm_flow](https://user-images.githubusercontent.com/76150626/183428922-b1e3e627-eaae-4777-ba6b-d8bcc7738d00.JPG)


Motion Sensor Behaviour Flow / Subflow
---
![motion sensor behaviour](https://user-images.githubusercontent.com/76150626/183702760-19102a84-9174-4fba-ad38-53cd191c94b3.JPG)


My own setup with 2 Bridges / 46 Lights / 6 Motion Sensors / 6 Button / Scenes
---
everything in one Flow Tab, using named link in nodes to connect it to my rooms.
You also may recognise some pink delay nodes as described.
Splitting up rooms on seperate header / http nodes for even better reliability.

![IMG_2199](https://user-images.githubusercontent.com/76150626/174289138-f115d757-b054-4122-9439-16d89cb370d3.jpeg)
