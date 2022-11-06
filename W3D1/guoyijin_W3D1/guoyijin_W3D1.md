## Limits to popelining

### 1. Structural Harzards

### 2. Data Harzards

RAW、WAR、WAW

#### Forwarding to Avoid Data Hazard

<img src="C:\Users\guoyijin-繁花似锦\github\Arch2022-Notes\W3D1\guoyijin_W3D1\image-20221001172639064.png" style="zoom:33%;" />

#### HW Change for Forwarding

<img src="C:\Users\guoyijin-繁花似锦\github\Arch2022-Notes\W3D1\guoyijin_W3D1\image-20221001172809825.png" style="zoom:33%;" />

#### Data Hazard Even with Forwarding 

<img src="C:\Users\guoyijin-繁花似锦\github\Arch2022-Notes\W3D1\guoyijin_W3D1\image-20221001181051431.png" style="zoom:33%;" />

#### Software Scheduling to Avoid Load Hazards

S/W：code moving

H/W：forwarding

### 3. Control Harzards

#### Four Branch Harzards Alternatives

###### 1.stall until branch direction is clear

###### 2.predict branch not taken

###### 3.predict branch taken

##### 4.**delayed branch**

1 slot delay allows proper decision and branch target address in 5 stage pipeline

1)intsructions to fill branch delay slot : 

before branch instruction

from the target address

from fall through

2)compiler effectiveness  :  fills 60% of branch delay slots

3)delayed branch downside  :  7-8 stage pipelines, multiple instructions issued per clock (superscalar)

