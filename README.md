![IMG_2180](https://user-images.githubusercontent.com/76150626/174133694-50b4d23b-7ee6-42a3-8d64-24de60890dde.jpeg)
 

## Please read the whole readme before use!

This respository is an example flow how to communicate using https-request with the HUE-Bridge, using HUE's Restful API V2 (Clip API) 
It includes various sample flows, sub-flows, descriptions and a lot more. You won't be dependent on badly maintained contribs anymore. 

As using almost only built-in NodeRed nodes, this repository has one small dependence, it is Yadomi's contrib philipshue-events.

https://github.com/yadomi/node-red-contrib-philipshue-events

### Before importing this flow, it is important to install yadomi's contrib previously. DO NOT DEPLOY WITHOUT!

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
Now use your App, turn on / off the light in the room, the subflow will output true/false. Repeat for all lights and rooms / zones, that need to have status events for your flows.Do the same for motion sensors and buttons.
- **step7** In the flow are several examples how to send actions to the bridge. You can just try it out and see what happens. The description is the node name.
  Discover yor scenes, (like in step 5) and add a scene ID into the "Recall a Scene" Node, deploy. Use the inject to activate the scene, repeat for all scenes that are needed.
- Done! You can now start to create your setup.

https://github.com/andesse/hue-clip-api.node-red-flows/blob/main/HUE-CLIP-API_Node-Red-Flows.json

### Recomendations / Informations:
- Do it room-by-room 
- Build the whole HUE-setup in a single Flow-Tab, use link-in / link-out nodes to connect it to your Rooms
- Label those link-in / link-out nodes, otherwise it will be too confusing
- Trigger scenes and not single lights, too much requests at once will be refused by the bridge
  The Bridge is just able to receive max! 5 light / 1 group request per second, less is better. If problems do occure, use the alternative request flow (step3)
- additional flows are in the "flows" folder in this repository and can be downloaded there
- Colors get more complicated. These are x/y values now. To determine the right value I recommend to change the color in the app and watch the EventStream. Open the color payload until you find the x/y values and use these.
- seperate flows can be found in the "flows" subfolder
- For a full API Documentation you could create an Account at: https://developers.meethue.com/                              

If you need help, start a discussion, Thanks!



### Shoutout to everyone who participated with great ideas, code, and/or additional flows, that made this repository even better, Thank you! Credits below

———————————————

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




Main Flow (HUE-CLIP-API_Node-Red-Flows.json):
------------
![HUE-CLIP-API_Node-Red-Flows_json](https://user-images.githubusercontent.com/76150626/188687612-092979bd-2711-4c24-9345-51c438d5056e.JPG)

-----------------------------------------------------------

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


credits and thanks to:
---
- ralfhille (first concept idea)
- yadomi (hue-events contrib)
- marc-gist (helper flow, to determine the ID/RID in a convenient way)
- FredBlo (new approach, with a lot of functional improvements for the flow)
