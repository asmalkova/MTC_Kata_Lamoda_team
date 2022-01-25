# MTC_Kata_Lamoda_team
There is our solution of architecture katas for MTC company.
Team members: 
- Boblova Anna, 
- Dubachev Mark,
- Malkova Anastasiya, 
- Marusova Ekaterina,
- Teminovskaya Anastasia,
- Rysin Nikita,
- Yartsev Dmitriy.


**Overview**
ABS Information System is a system that provides the information about ABS maintenance using predictive analytics based on data received from telemetry and other data sources.
ABS Information System consists of

- datamarts and dashboard for ABS condition monitoring
- datamarts and dashboard for ABS exploitation monitoring
- datamarts and dashboard for ABS external problems monitoring
- datamarts and dashboard for ABS plan/fact maintenance monitoring
- data mart, forecasting model, dashboard for ABS maintenance 


**Business Case and Goals**

Prerequisites for the implementation of this problem:
- implementation of the smart city concept - the creation of integrated intelligent solutions for real-time management.
- increase in efficiency - increase in safety, loss prevention and optimization
resource use.
- personalization and improvement of the quality of services - better resource management, provision of personalized services and recommendations to reduce consumption


**Stakeholders**
| **Stakeholder** | **Concerns** |
| --- | --- |
| Customer| Timely correct network operation for personal tasks |
| Maintenance Team | Correct distribution of workload and working hours |
| Operational attendants | Timely recorded incidents |
| Other operators | Ability to share MBS |
| Management| The ability to evaluate and track the stability of work | 


**Constraints**
Limited number of external selected factors to control
Restrictions on the number of technical personnel and different load on the MBS

**Assumptions**
It is important for maintenance teams to know in advance about possible incidents and breakdowns in order to more effectively distribute the load and plan work
Technical availability of MBS monitoring systems in the following areas: weather conditions, humidity, fires, burglaries, power supply, condition of components

**ABS Information System Structure Description **

1) ABS condition monitoring
Using Automated systems for monitoring cellular base stations, we obtain the following information about the state of the base station:
- data about electricity from digital electricity meters
- battery status data
- temperature data
- power rack data
2) ABS exploitation monitoring
To ensure the quality of mobile communication and operation of the ABS, a metrological system is used - Mobile Backhaul Service Assurance. Specially designed probes of the system allow you to control from the switching center simultaneously up to ten thousand base stations in real time.
3) ABS external problems monitoring
Applying a special cube-controller on top of the ABS, we obtain data on the following external factors that affect the ABS:

| **External factor** | **ABS Controller Module** |
| --- | --- |
| Hacking ABS, Equipment theft| Opening control |
| Fire affecting ABS | Fire control|
| Abnormal decrease/increase in outside temperature | Temperature control |
| ABS alarms | Station alarm control|
| Abnormal decrease/increase in outside humidity| Humidity control | 

Additional Resources on External Factors:
- Available number of employees for maintenance - internal data of ERP systems
- Information about emergencies in the nearest territories - parsing data of news resources
- Weather forecast - external data from weather stations
- Data on external physical threats - data from cameras for external monitoring of the state of the MBS

4) ABS plan/fact maintenance

**ABS Information System Elements Integration Description**
![alt-текст](https://drive.google.com/file/d/19x73r3oSQRXlZ5dHP8Zqh5CViv-Wlf3j/view?usp=sharing)

Network layer - contains three different quality tracking controllers, that were mentioned above: condition sensor, controller sensor, mobile communication quality system

Meditation layer - service that is needed to connect two layers: network and data storage. In our solution case there are two adapters: streaming and text files, that edit information in required form.

Data storing - all metadata, failures, logs and others are stored in DB Apache HBASE (that is already implemented in MTS).

Management system layer - is necessary to accumulate information and analyze what failures exist, what guilty side is in each case and erc.

Presentation layer - represented in two forms: reporting system is presented in the form of a bot that sends an alert to technicians (in case the machine learning system could not offer a solution to the problem) and in the form of a dashboard that accumulates information and statistics.

Data Model


**List of significant architectural properties**


List of major architectural decisions and their rationale

| **architectural solution** | **justification** |
| --- | --- |
| Apache HBASE for data storing| The open source NoSQL DBMS is already used in the company. Runs on top of the HDFS distributed file system and provides BigTable capabilities for Hadoop, providing a fault-tolerant way to store large amounts of sparse data |
| Meditation layer for communication of two levels | The need to convert data from sensors into one of the established forms for storage. For this, two types of adapters were chosen:  streaming and text files|
|Reporting system is presented in the form of a bot |t
The need to automate the process of manually registering incidents and assigning service teams in view of reducing the time for solving problem situations |
|Grafana for for monitoring data visualization |The need to monitor indicators and metrics to assess the condition of the equipment, as well as the effectiveness of its maintenance. Chosen because it is a multi-platform open source analytics and interactive visualization platform. It is designed to provide context-rich visualizations, primarily through graphs, but it also supports other methods of presenting data due to its plug-in panel architecture. Each control panel is customizable to meet the needs of a particular project.|


**Key benefits:**

• Increased network utilization and availability. 

• Minimize and/or even predict outages. 

• Holistic view of the communication service provider network - health status. 

• Reduce customer churn and improve customer experience. 

• Provide key data for network planning from maintenance activities. 

• Reduce operational expenses by increasing personnel productivity, allowing them to manage complex networks.


