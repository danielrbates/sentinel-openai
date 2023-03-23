# Sentinel + OpenAI
Integrating Microsoft Sentinel with Azure OpenAI.

![image](https://user-images.githubusercontent.com/25780196/226948056-3269a1e7-a97a-4a00-bf3f-52bd84d2b681.png)

This project uses two Logic Apps to bring in context from ChatGPT on Azure OpenAI Service.  The first logic app is the "orchestrator"; it has a Sentinel incident trigger and is used to initiate the automation and write comments or tasks back to the Sentinel incident.  The second logic app contains the ChatGPT query itself.  This modular approach allows us to add additional functionality to the playbook without overburdening the main logic app.
