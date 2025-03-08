<a href="https://nicopedrazaportfolio.netlify.app/">Back to My Portfolio</a>

# 🌡️ Streaming and Analyzing Live Data

This project is designed to stream real-time temperature and humidity data using a Dockerized MQTT (Mosquitto) broker and Python’s Paho MQTT client, seamlessly integrating with ThingsBoard and Firebase Realtime Database for automated storage and visualization. Leveraging containerized microservices to orchestrate sensor-to-cloud data pipelines, the system ensures robust and modular data ingestion and processing. The alarm rule chain in ThingsBoard detects threshold-exceeding data, sending critical alerts to Firebase for immediate oversight. By uniting Docker, MQTT, and cloud-based platforms, this project demonstrates a full-stack IoT solution, showcasing the potential for proactive data-driven insights and real-time analytics.


## Steps to run this project
1. Either fork or download the folder in this repository and open it in your code editor
2. Install all necessary dependencies
3. In your Terminal, navigate to StreamingAnalyzingLiveData/MQTT/mosquitto and run `docker compose up` to initialize the Mosquitto container
4. Navigate to your home folder and create two folders named ".mytb-data" and ".mytb-logs"
5. In your terminal, navigate to StreamingAnalyzingLiveData/MQTT/Thingsboard and run `docker compose up` to initialize the ThingsBoard container
6. Open a Terminal window in your code editor and run the TBPublish.py file
7. In a browser window, navigate to http://localhost:8080/. Log in to ThingsBoard using Login:tenant@thingsboard.org and Password:tenant
8. Navigate to Google Firebase and create a real-time database. Add two fields in the database: "temperature" and "alarm"
9. Navigate to the Root Rule Chain in ThingsBoard. Add a "rest API call" node and name it Firebase. In the "Endpoint URL pattern" field, paste the link to your Realtime database from Firebase followed by "/temperature.json". Connect the "Firebase" node to the "Message Type Switch" node. Add "Post telemetry" as the link label
10. Create a new rule chain titled "CreateAndClearAlarms". Add a "script" node and name it "TempThreshold". Modify the script to set the threshold you desire. Add a "clear alarm" node and name it "ClearAlarm". Modify the script to:
```JavaScript
var details = {};

if (metadata.prevAlarmDetails) {

    details = JSON.parse(metadata.prevAlarmDetails);}

return details;
```
Add a "create alarm" node and name it "CreateAlarm". Modify the script to be the same as "ClearAlarm". Connect "ClearAlarm" and "CreateAlarm" to "TempThreshold", add “False” as the link label between "CreateAlarm" to "TempThreshold" and "True" as the link label between "ClearAlarm" to "TempThreshold"

11. Create another rule chain and name it "TempToFirebase". Add a "rest API call" node and name it "TempToFirebase". Replace the default link with your Firebase database "temperature" field link
12. Create another rule chain and name it "AlarmToFirebase". Add a "rest API call" node and name it "AlarmToFirebase". Replace the default link with your Firebase database "alarm" field link
13. Add and connect your "TempToFirebase" and "AlarmToFirebase" rule chains to the "CreateAndClearAlarms" rule chain
14. Open the Root Rule Chain in ThingsBoard. Add a "rule chain" node. Name it "CreateAndClearAlarm" and select CreateAndClearAlarm as the rule chain. Select "Add" to add the CreateAndClearAlarm node to your Rule Engine
15. Connect the SaveTimeseries and CreateAndClearAlarm nodes. Add “Success” as the link label
16. Navigate to Firebase and open the alarm and temperature fields to check the results

## Features
- Simulated stream of temperature and humidity data
- Live collection of simulated IoT data
- Fully integrated rule chain in ThingsBoard
- Alarm set up for threshold
- Automated storage and visualization in Firebase
  
  ## Future Features
- Add more IoT devices
- Do live data analysis on the data: graphs, trends, predictions, etc...

## Tools:
* Python
* JSON
* JavaScript
* ThingsBoard
* Firebase
* Libraries: Paho.mqtt

## What the project looks like

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/9637ccd4-a2ce-4295-806e-8a93766d1d5c" />

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/dfd03612-fd8c-482d-adc8-0552012aebe6" />

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/0966807e-59bf-49e0-93ce-7588cd905664" />

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/2ae7b3bd-f9ad-4b91-aa7d-054adbdb61f0" />

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/f2b99108-051e-4ba6-913d-b069b7920169" />







