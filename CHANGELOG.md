# Changelog

## Unreleased

* Adds new choice for soil water content reflectometers: Option 3 - zero to three
  Acclima TDR-series soil reflectometers. Sensors use identical input channel and
  SDI-12 sensor addresses as default CS655 option. If TCAV is not used, sensors
  also provide soil temperature measurements.
* Adds new option for zero to six Acclima TDR-series soil sensors for profile measurements.
  Sensors must be sequentially addressed with a maximum address of 9. 
  Data is acquired independently of gas flux and energy balance, and can be stored in
  separate data table *Flux_Extra* or as additional columns following *Flux_Notes* columns.

## 2.01 (2022-07-21)

* For CR6OP: [17 change(s) - 07-21-2022](https://www.campbellsci.com/revisions/611-1704#revisions)
* For CR1000XOP: [17 change(s) - 07-21-2022](https://www.campbellsci.com/revisions/681-1705#revisions)
