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
| TDR #1/#2/#3<br />(Addresses 4/5/6) | 0 to 3 | SDI-12 data | Blue | **U3** | **C3** |
| | | SDI-12 power | Red | **+12 V** | **+12 V** |
| | | SDI-12 reference | White | **G** | **G** |

## 4. Operation

### 4.4 Output tables

> The following revisions apply to section 4.4.

For **Table 4-9: Data fields in the Flux_AmeriFluxFormat output table**:

* In the *Data field included* column, replace all references to "CS65X" with "CS65X or TDR".

For **Table 4-10: Data fields in the Flux_CSFormat output table**:

| Change Type | Data Field Name | Units | Description | Data Field Included |
|:-:|:-:|:-:|:-:|:-:|
| Update row | TS_1_1_x | deg C | Average soil temperature; x of 1 to 3 is an index for the number of soil temperature measurements made | If TCAV, CS65X or TDR is used (if both, TCAV temperature is used) |
| Update row | SWC_1_1_x | % [^1] | | |
| Insert 3 rows after CS65x_ec_1_1_x | TDR_E_1_1_x | unitless | Soil permittivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |
| | TDR_bulkEC_1_1_x | dS m-1 | Soil bulk electrical conductivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |
| | TDR_poreEC_1_1_x | dS m-1 | Soil pore water electrical conductivity; x of 1 to 3 is an index for the number of soil sensors | If TDR is used |


[^1]: Minor typo in user guide. 
