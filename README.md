![IMG_2180](https://user-images.githubusercontent.com/76150626/174133694-50b4d23b-7ee6-42a3-8d64-24de60890dde.jpeg)

# Please read the readme before use!

This respository is an example flow how to communicate using https-request with the HUE-Bridge, using HUE's Restful API V2 (Clip API) 
It includes various sample flows, sub-flows, descriptions and a lot more.

As using almost only built-in NodeRed nodes, this repository has one small dependence. It is Yadomi's contrib philipshue-events or the contrib-sse, depending on the setup you prefer.

https://github.com/yadomi/node-red-contrib-philipshue-events

### change! instead of using the yadomi contrib, use the approach with the "sse-event-stream" all infos below. This works flawless for me without any issues for more than a year now
(Before importing this flow, it is important to install yadomi's contrib previously. Do not deploy without, this might Node-RED to stop the flows.)

———————————————

### Installation Instructions:
- Install "@yadomi/node-red-contrib-philipshue-events" in NodeRed
- Import the Data from the :arrow_right: **HUE-CLIP-API_Node-Red-Flows.json** :arrow_left: into a new Flow Tab, deploy
- In the flow are labels with **step1-step7**, follow step-by-step
- **step1** generate a username for this flow in the Bridge, first add the Bridge IP in the labeled node, deploy.
Press the button on your Bridge. Inject the Request Node, the debug window will show the username
- **step2** Configure the hue-events node with your IP and just discovered username
- **step3** add the same data into the HEADER V2 node, deploy
- **step4** Inject the "Request all Data" node. This process will take a couple of seconds, the Data will be stored in context (memory)
- **step5** Now you can use the Inject nodes for different API Endpoints. The data will be shown in the debug window. Discover lights or rooms for the next step
- **step6** Double click on the blue "HUE Light Receiver" Node. Add the ID (for a light) or the RID (for a Room) inside the node, deploy. 
Now use your App, turn on / off the light in the room, the subflow will output true/false. Repeat for all lights and rooms / zones, that need to have status events for your flows. Do the same for motion sensors and buttons.
- **step7** In the flow are several examples how to send actions to the bridge. You can just try it out and see what happens. The description is the node name.
Discover your scenes, (like in step 5) and add a scene ID into the "Recall a Scene" Node, deploy. Use the inject to activate the scene, repeat for all scenes that are needed.
- Done! You can now start to create your setup.

- Worth to mention: There are some flow examples for special things in the flows subfolder of this repository. Some are described here in the readme, others are not. The name is a hint what it is, just try it out. 

https://github.com/andesse/hue-clip-api.node-red-flows/blob/main/HUE-CLIP-API_Node-Red-Flows.json

### Recomendations / Informations:
- Do it room-by-room 
- Build the whole HUE-setup in a single Flow-Tab, use link-in / link-out nodes to connect it to your Rooms
- Label those link-in / link-out nodes, otherwise it will be too confusing
- Trigger scenes and not single lights, too much requests at once will be refused by the bridge
  The Bridge is just able to receive max! 5 light / 1 group request per second, less is better. If problems do occure, use the alternative request flow (step3)
- additional flows are in the "flows" folder in this repository and can be downloaded there
- Colors get more complicated. These are x/y values now. To determine the right value I recommend to change the color in the app and watch the EventStream. Open the color payload until you find the x/y values and use these.
- For a full API Documentation you could create an Account at: https://developers.meethue.com/                              

### If your Bridge stops sending Events from yadomi's node (this can be related to Network connectivity loss) try to re-deploy the node, or get a new api token. Restarting Node-RED might work as well.

If you need help, start a discussion and when you are pleased with this repository, click donate and buy me a coffee :) Thanks

### Shoutout to everyone who participated with great ideas, code, and/or additional flows, that made this repository even better, Thank you! Credits below

Main Flow (HUE-CLIP-API_Node-Red-Flows.json):
------------
![HUE-CLIP-API_Node-Red-Flows_json](https://user-images.githubusercontent.com/76150626/188687612-092979bd-2711-4c24-9345-51c438d5056e.JPG)

______________

## Version 5.3.2 Update

**NEW:** Battery Status Subflow

I created a subflow Node and made some changes at the Helper Flow, its now easy to determine the battery levels,
and also to output Device Name + Battery status if the level falls under a specified value. 

You will find the file battery_status.json in the flows section for download. Or use this link:
https://github.com/andesse/HUE-CLIP-API.Node-RED-Flows/blob/main/flows/battery_status.json

All necessary infos are included in the file as comments. 
Please read the Instructions at top left first.

![IMG_8187](https://github.com/user-attachments/assets/620c8ae5-8359-45aa-814a-6f1b05cb23a3)

![IMG_8186](https://github.com/user-attachments/assets/49d03ee6-3803-4564-b97e-0f12397a4876)

______________

## Version 5.3.1 Update

I just discovered that it is possible to determine which scene is turned on in the eventstream.

A new subflow is added in the flows folder: flows/scene_active.json  
Simply add the discovered scene ID and it gives you a true when the scene is turned on.
This might be useful in some scenarios. 


![IMG_1205](https://github.com/andesse/HUE-CLIP-API.Node-RED-Flows/assets/76150626/f23223ff-66f1-431d-92ae-e2b47450ee20)



Version 5.3
---
I made an all-in-one Subflow for: Candle, Fire, Alarm Light, Alarm Group, dynamic Scene effects. It is pretty convenient to use.
It should work out of the box immediatly. You just need to add the ID in the subflow when you double click it.
There are some description in the Flow as usual. You can find the file un the flows subfolder. hue_effects.json
https://github.com/andesse/hue-clip-api.node-red-flows/blob/main/flows/hue_effects.json

Edit: normal scene added as well, not shown in the picture

![IMG_2784](https://user-images.githubusercontent.com/76150626/193901650-85ff3179-56eb-4592-bac2-22e159ec6b52.jpeg)


———————————————

Version 5.2
---
The motion_sensor_bahavior.json flow got replaced, you can find it in the flows folder.It would be a super long text to explain it here, short: this controls a motion sensor thats not configurized in the app. I made it to define the times more accurately. Import it and have a look, there are quite a lot of comments in the flow. No additional contrib needed like before. Looks super big on the picture, but when everything is in place and with link in / out nodes its fine. There are also some additional things as well, probably not needed  

![IMG_2773](https://user-images.githubusercontent.com/76150626/193459271-a1f7a9e7-c947-45e1-8981-3fce228231dc.jpeg)



Version 5.1
---
- one file added into the flows subfolder >>> motion_sensor_update.json
- the updated flow for the motion endpoint receivers has a benefit, you can see the sensor state (enabled/disabled).
- this is just nice to have, try it and decide if its useful for your setup.

![IMG_2726](https://user-images.githubusercontent.com/76150626/192052817-32535569-39c1-4c79-b8f9-2dbc019ca83b.jpeg)


Version 5.0
---

- Merged the V2 approach from FredBlo with the original flow
- Complete update of the readme, with easy installation instructions
- Array Splitter function node from FredBlo

### Another change is coming with upcoming Bridge Firmware, read below. (this is important for everyone already using the flow)

HUE changed the Event-Flow output for groups in the API with a new Beta Firmware. I got the beta release 1.53.1953188010

Instead of sending payloads for every light/group seperately they changed it into a payload with one big array.
For the reason that the response data for the group is not always at the same position the array need to be split to single payloads first. 
Everything else seem to work like before.

The array splitter is set in between your event node (SSE or Yadomi) and the output is connected to the receivers.
https://github.com/andesse/hue-clip-api.node-red-flows/blob/main/flows/array_splitter.json


Array Splitter separately:
-----------
![array_splitter](https://user-images.githubusercontent.com/76150626/188687682-3bceea2c-4d40-495e-9eed-42d041415508.JPG)


These change can be done already, even when you dont have this Firmware. You just need to add the node into your setup to be prepared before the public Firmware rollout. 
>ALWAYS BACKUP YOUR OLD FLOW BEFORE, TO AVOID DOUBLE EFFORT IF YOU HAVE AN ISSUE!

-----------------------------------------------------------

Action Change Nodes:
---
![IMG_2723](https://user-images.githubusercontent.com/76150626/192001918-178e9a6e-8075-4a92-9e0d-f6bfe5792d95.jpeg)

-----------------------------------------------------------

Helper Functions for RID / ID discovery (concept by user marc-gist - THANKS!)
---
![helper_functions_flow_v2](https://user-images.githubusercontent.com/76150626/174495416-dbb394b5-c012-482c-a119-eb16cd073171.PNG)


SSE_Event_Stream:
---

![IMG_2261](https://user-images.githubusercontent.com/76150626/176202424-8f7e53db-bb9a-41aa-8ce4-c71f1b153fa5.jpeg)


credits and thanks to:
---
- ralfhille (first concept idea)
- yadomi (hue-events contrib)
- marc-gist (helper flow, to determine the ID/RID in a convenient way)
- FredBlo (new approach, with a lot of functional improvements for the flow)

Sponsor Link, buy me a coffee :)
