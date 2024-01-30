# Supplemental Documentation for EasyFlux-DL CR6OP and CR1000XOP

> The following revisions apply to *EasyFlux-DL Product Manual For CR6 or CR1000X and Open-Path Eddy-Covariance Systems (Revision 03/2022)*.
>
> Online: https://s.campbellsci.com/documents/us/manuals/easyflux-dl-cr6op.pdf

## 1. Introduction

Make the following additions to the list of supported sensors (in bold):

* Radiation measurement instrument
    * Option 1
        * CS301 or CS320 pyranometer (qty 0 to 1)
        * CS310 **or LI190** quantum sensor (qty 0 to 1)
        * SI-111 infrared radiometer (qty 0 to 1)
* Soil water content reflectometer (qty 0 to 3)
    * Option 1: CS650
    * Option 2: CS655
    * **Option 3: Acclima TDR series**
* **Array of soil sensors (qty 0 to 6)**
    * **Option 1: Acclima TDR series**

## 3.1 Wiring

### 3.1.6 Radiation measurements, Option 1

An LI-190 series quantum (PAR) sensor (LI-COR Biosciences) may be used in place
of a CS310 quantum sensor. Wire the sensor using the table below and then:

1. Set constant `SENSOR_CS310` to True.
1. Update unique constant `QUNTM_MULT` with the sensor-specific multiplier (&micro;mol/m^2/s/mV).

| Sensor | Quantity | Wire Description | Color | VOLT116 terminal |
|:-:|:-:|:-:|:-:|:-:|
| LI-190 series quantum sensor | 0 or 1 | Signal | Red | **Diff 8H** |
| | | Signal reference | Black | **Diff 8L** |
| | | Signal ground (-R series) | White | **AG&#x23DA;** |
| | | Shield | Clear | **AG&#x23DA;** |

### 3.1.10 Soil water content reflectometers

This version of ***EasyFlux DL OP*** supports three models of soil water content reflectometers:
Campbell Scientific CS650 or CS655, or Acclima TDR series sensors. 
Up to three sensors of any one model may be selected, or zero sensors may be selected.
The default wiring for CS650 and CS655 is shown in Table 3-11 (p. 13).
The default wiring for TDR series is substantially identical and shown in the table below.

| Sensor | Quantity | Wire Description | Color | CR6 terminal | CR1000X terminal |
|:-:|:-:|:-:|:-:|:-:|:-:|
| TDR #1/#2/#3<br />(Addresses 4/5/6) | 0 to 3 | SDI-12 data | Blue | **U3** [^1] | **C3** [^1] |
| | | SDI-12 power | Red | **+12 V** [^2] | **+12 V** [^2] |
| | | SDI-12 reference | White | **G** | **G** |

### 3.1.11 Array of soil sensors, Option 1

This version of ***EasyFlux DL OP*** supports from zero to six additional Acclima TDR series sensors,
for soil measurements independent of energy balance calculations (e.g. vertical profiling).
Sensors are queried from a separate scan and data is optionally output to separate data table *Soil_Profile*.
The sensor SDI-12 addresses must be sequential and the starting address and quantity
must be specified using unique program constants.

By default, sensor quantity is 3 and sequential SDI-12 addresses are 7, 8, 9. 
Data field output labels (from 1 up to 6) correspond to these addresses, from low to high.
The default wiring uses the same SDI-12 input channel as soil water content reflectometers:

| Sensor | Quantity | Wire Description | Color | CR6 terminal | CR1000X terminal |
|:-:|:-:|:-:|:-:|:-:|:-:|
| TDR #1..6 | 0 to 6 | SDI-12 data | Blue | **U3** [^1] | **C3** [^1] |
| | | SDI-12 power | Red | **+12 V** [^2] | **+12 V** [^2] |
| | | SDI-12 reference | White | **G** | **G** |

## 4. Operation

### 4.4 Output tables

> The following revisions apply to section 4.4.

For **Table 4-5: Data output tables**, insert this additional row:

| Table name | Description | Recording interval | Memory on CR6 or CR1000X CPU | Memory on microSD card |
|:-:|:-:|:-:|:-:|:-:|
| Soil_Profile | Statistical data from soil profile measurements | OUTPUT_INTERVAL (default 30 min) | NUM_DAY_CPU (default 7 days) | Broken up into 30-day files; see Table 4-4 |

For **Table 4-9: Data fields in the Flux_AmeriFluxFormat output table**:

* In the *Data field included* column, replace all references to "CS65X" with "CS65X or TDR".

For **Table 4-10: Data fields in the Flux_CSFormat output table**:

| Change Type | Data Field Name | Units | Description | Data Field Included |
|:-:|:-:|:-:|:-:|:-:|
| Update row | TS_1_1_x | deg C | Average soil temperature; x of 1 to 3 is an index for the number of soil temperature measurements made | If TCAV, CS65X or TDR is used (if both, TCAV temperature is used) |
| Update row | SWC_1_1_x | % [^3] | | |
| Insert 3 rows after CS65x_ec_1_1_x | TDR_E_1_1_x | unitless | Soil permittivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |
| | TDR_bulkEC_1_1_x | dS m-1 | Soil bulk electrical conductivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |
| | TDR_poreEC_1_1_x | dS m-1 | Soil pore water electrical conductivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |

Insert new table, **Table 4-11: Data fields in the Soil_Profile output table:**

| Data Field Name | Units | Description | Data Field Included |
|:-:|:-:|:-:|:-:|
| SWC_2_2_x | % | Soil volumetric water content; x of 1 to 6 is an index for the number of soil sensors | If PROFILE_TDR is used |
| TS_TDR_2_2_x | deg C | Soil temperature; x of 1 to 6 is an index for the number of soil sensors | IF_PROFILE_TDR is used |
| TDR_E_2_2_x | unitless | Soil permittivity; x of 1 to 6 is an index for the number of soil sensors | If PROFILE_TDR is used |
| TDR_bulkEC_2_2_x | dS m-1 | Soil bulk electrical conductivity; x of 1 to 6 is an index for the number of soil sensors | If PROFILE_TDR is used |
| TDR_poreEC_2_2_x | dS m-1 | Soil pore water electrical conductivity; x of 1 to 6 is an index for the number of soil sensors | If PROFILE_TDR is used |

[^1]: Multi-circuit spring-clamp terminal blocks are recommended for multiplexing wires to the logger terminals.
[^2]: Powering sensor(s) from the datalogger's +12V source instead of 12V terminal is recommended.
[^3]: Minor typo in user guide.