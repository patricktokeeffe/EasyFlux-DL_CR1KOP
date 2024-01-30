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
