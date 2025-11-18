```mermaid
graph TB

%% --- TOP LAYER ---
U["User"]

%% Dummy vertical connector
U --> U2
U2 --> Modules

%% --- MODULE LAYER ---
subgraph Modules["PROCESS LAYER"]
  direction TB
  PM["Patient Management"]
  DM["Doctor Management"]
  AM["Appointment Management"]
  SM["Search Module"]
  REP["Summary & Reports"]
end

Modules --> DataStores

%% Commands to modules
U -->|Commands| PM
U -->|Commands| DM
U -->|Commands| AM
U -->|Search Query| SM
U -->|Request Summary| REP

%% --- DATA STORE LAYER ---
subgraph DataStores["DATA STORE LAYER"]
  direction TB
  DS1["Patient Records"]
  DS2["Doctor Records"]
  DS3["Appointment Records"]
  DS4["Treatment History"]
end

%% --- FLOWS TO DATA STORES ---
PM -->|Save Patient Data| DS1
PM -->|Save Treatment Info| DS4
DM -->|Save Doctor Data| DS2
AM -->|Create Appointment| DS3
SM -->|Read Patients| DS1
SM -->|Read Doctors| DS2
REP -->|Access All Data| DS1
REP -->|Access All Data| DS2
REP -->|Access All Data| DS3
REP -->|Access All Data| DS4

%% --- DATA STORES RETURN FLOWS ---
DS1 -->|Patient List| PM
DS2 -->|Doctor List| DM
DS3 -->|Schedules| AM
DS4 -->|Treatment History| PM
