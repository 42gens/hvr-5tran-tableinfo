#### hvr-5tran-tableinfo - Partition your HVR pipe-line by table activity

##### A:  Who and When:
Creator: ctijerina 
Creation time: 2018 changes thru 2022

#### B: Word Legend: 
1. CDC = change data capture - capturing inserts, updates and deletes
2. Client = the user of this script - can be you too.
3. Channel = this houses your pipe-line, it's like a project folder and your pipe-lines will be inside your Channel,
             every channel will produce 1 hvr.out file and this is the key file this script will run against.
             If you have many pipi-lines in 1 chanel, not to worry, this script will account for each pipe-line, remember
             all hvr channels will have 1 hvr.log file.
4. Compute = Total cost of CPU, Memory, IO even disk space.
NOTE: Compute can increase by an os job, db job, sql, a 3rd party cdc tool.
This script is not an OS/DB performance analyzing tool, it's desinged to help
HVR users better understand their application tables for better thru put.         

#### C: This script runs on:
1. Linux
2. Mac Terminal
3. Windows(but must use WSL bash - it's a linux sub system on windows)

#### D: The goal:
1. Is to parse the hvr.out file for all CAPTURE activity for a given run time.
2. If no capture key word then integrate processed rows will be calculated

#### E: Steps to prep for this script:
NOTE: you don't have to have hvr/5tran installed to run this script, you can put your
      hvr.out file on any linux os along with this file and run this file.
1. The client will be asked to setup a Capture and allow it to run for 24+ hours (2 days)
   NOTE: If you're currently running hvr, even bettter, use this current hvr.log file.
   If you backup hvr.log and let's say you have 10 logs, Concat all 10 files into 1 big file,
   then use this 1 big file with this script. 

#### F: Where to put this script and how to run
1. Best place is the hvr_config/log/yourHubName
2. chmod +x hvrBusyTables_v13.2.bash
3. ./hvrBusyhvrBusyTables_v13.2.bash
----
4. download hvrBusyTables_v13.2.bash to server1 in /home/myName
5. Copy your current hvr.out to server1 in /home/myName
6. chmod +x hvrBusyTables_v13.2.bash
7. run the script:  ./hvrBusyTables_v13.2.bash

#### G. End Results - output to console and to text files
1. Total # of Application Tables in your CDC Replication Pipelines/Channels
2. Total # of Changed Rows - changed by Insert, Update or Delete - broTip: this is CDC
3. A list of all tables with the total amount of changed rows
4. Post programatically analyzing: Small - Medium - Busy groups based on calculation  sum/tableTotalchanged*100

#### H. BENEFITS - what to do with the output from this script
1. Determine how to parallelize your downstream pipelines/hvr channels for better thru put, get near real-time deivery of your data
##a. if you have a SLA of 1 min, and your data is breaking the SLA by 5 minutes, this tool will help you achieve near-real time delivery.
2. Use this data to proavtively determine capacity sizing.
##a. Every Insert means a new customer, which means more storage and os/db compute will be utilized
#####

HVR-5Tran-TableInfo: Enhance Your HVR Pipeline Performance
Overview: The hvr-5tran-tableinfo tool empowers users to analyze and partition their HVR pipelines based on table activity, enabling optimal data throughput and efficient resource utilization.

Metadata:
Author: ctijerina
Date of Creation: 2018
Latest Update: 2022
Glossary:
CDC: Change Data Capture (capturing inserts, updates, and deletes).
Client: User of this script. This could be you!
Channel: Represents the HVR pipeline, analogous to a project folder. All channels generate a single hvr.out file, which this script parses.
Compute: Cumulative cost of resources like CPU, Memory, IO, and disk space. External factors like OS jobs, DB jobs, SQL, or third-party CDC tools can influence compute.
Platform Compatibility:
Linux
Mac Terminal
Windows (via WSL bash)
Objective:
Parse the hvr.out file for all CAPTURE activity for a designated runtime. If no capture keyword is found, integrated processed rows will be calculated.

Setup:
You don't need HVR/5Tran installed. Just place your hvr.out file and this script on any compatible system.
For optimal results, set up a Capture for 24+ hours. Existing HVR users can utilize their current hvr.log file. Multiple logs can be concatenated into a single file for this script.
Usage:
Download hvrBusyTables_v13.2.bash to a directory (e.g., /home/myName on server1).
Copy your hvr.out to the same directory.
Provide execution permissions: chmod +x hvrBusyTables_v13.2.bash.
Run the script: ./hvrBusyTables_v13.2.bash.
Output:
Total count of application tables in your CDC Replication Pipelines/Channels.
Cumulative changed rows segmented by Insert, Update, or Delete.
An analytic breakdown of tables based on the volume of changed rows.
Benefits:
Optimized Data Delivery: Improve the parallelization of your downstream pipelines for near real-time data delivery, especially beneficial if you're striving for stringent SLAs.
Capacity Forecasting: Leverage insights from the script to proactively determine capacity sizing, preparing for incremental data and its associated resource needs.
