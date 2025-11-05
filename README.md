# **SCIENTIFIC COMPUTING**
# **Development of an ESP32-Based Reference Instrument for Calibrating the Triple Point Temperature of Water.**

# Index

1. [Clonar github](#1-installing-of-necesareis-libraries)
   - [Enviroment env](#enviroment-env)
2. [Directory Structure](#2-directory-structure)
3. [Abstract](#3-abstract)
4. [Data Structure](#4-data-structure)
5. [Preprocessing](#5-preprocessing)
6. [Statical Analysis](#6-statical-analysis)
7. [Conclusions](#7-conclusions)
8. [Bibliographic Reference](#8-Bibliographic-Reference)



# 1. Installing of Necesareis Libraries 

To work with this repository, you should follow the instructions below.

Note: These instructions are only applicable for Linux systems.

## Enviroment env

```sh
git clone https://github.com/hernancardenasposada/MMPC14-1_SCIENTIFIC_PROGRAM.git
cd MMPC14-1_SCIENTIFIC_PROGRAM
```
# 2. Directory Structure 

```sh
hernancardenasposada/MMPC14-1_SCIENTIFIC_PROGRAM
│
├── Data/
|   |
|   └── 1_DataTime_Point_TPW.csv/
|
├── Preprocessing/
|   |
|   └── 1_First_lab.ipynb
|
├── Statical Analysis/
|   |
|   └── 2_Second_Lab.ipynb
|
├── Figures
|   |
|   └── data_64AQM_SNR_20_level110.csv
|
├── rerults_AQM
|
├── .gitignore
|
└── requirements.md

```

# 3. Abstract

The work describes the calibration facilities, the procedure, the uncertainty analysis, and the quality control measures. It addresses the challenge of balancing metrological accuracy with efficiency, employing a strategy that includes statistical control and internal consistency measures to ensure device reliability during calibrations.

 The objective is to develop a standard prototype for temperature calibration at 0 °C using an ESP32 microcontroller and a specific sensor that supports calibrations with the water triple point device. Once the measurement system has been obtained, we must perform stability, repeatability, and validation tests with all sources of uncertainty associated with the process.


# 4. Data Structure

Data loading and initial visualization:


*  *Date:* date of measurement.
*  *Day:* day of measurement.
*  *Time:* time at which the measurement was taken.
*  *Triplepointw:* measuring device used, in which 0 °C is guaranteed.
*  *SprtTemperature:* reference prototype implemented with an SPRT (standard platinum resistance thermometer) sensor.
*  *ReferenceTemperature:* reference thermometer used for direct comparison.
*  *SprtOhms:* values taken by the SPRT transducer in ohms.

A database with measurements taken during February 2025 was selected to visualize the behavior of the implemented instrument (SprtTemperature) and to obtain measurements at the triple point of water. It was also considered necessary to obtain the ohm value of the SPRT sensor (SprtOhms) and a reference instrument for direct comparison during temperature measurement (ReferenceTemperature). Since the triple point of water generates the necessary conditions to measure the 0 °C point, the above database allows the behavior of the implemented instrument (SprtTemperature) to be verified.


# 5. Preprocessing

In this section, `Preprocessing/1_First_lab.ipynb`, you may find various data preprocessing steps, including:

- **Description of the research problem**: In the network of laboratories accredited by ONAC, the explicit use of the PTA is not clearly reflected in the published technical scope of accreditation, which mentions temperature ranges but not the associated reference method. Thus, direct traceability to the PTA is not always transferred to the secondary or industrial level, creating gaps in metrological uniformity between the national standard and the instruments used in the field. In this context, there is a need to develop the validation of a method for the calibration of direct-reading digital thermometers at the triple point of water, raising the question of how the validation of this method could improve metrological traceability and social impact in the area of thermodynamics in Colombia, with special emphasis on the Antioquia region.

- **Data loading and initial visualization**: In this first stage, we describe the characteristics of the database and observe the behavior of the implemented instrument (SprtTemperature) and the reference instrument (ReferenceTemperature).
The measurements are taken during the month of February in order to evaluate the average of the daily measurements and the dispersion of their data with the standard deviation in the implemented instrument.
As a practical exercise in this section, the correction is applied to the instrument under test and its behavior is observed over time.


- **Data analysis channeling**: Object-oriented programming is used to create classes to select the day and amount of study data in order to perform a daily analysis of our database.
Visualization graphs and histograms are generated using the TimeFilter class based on SprtTemperature, ReferenceTemperature, and SprtOhms, the three variables related to time.


- **Numerical derivation of data**: In this section, we calculate the derivative of the SprtTemperature variable with respect to time using the TimeSeriesBase class as a starting point for the DataPrep and DerivativeCalculator subclasses, which inherit the basic attributes for operating with the derivative.


- **Matrix operations**: In this section, multivariate analysis is implemented on the database used to align the series over time and calculate Z-scores, covariances, and correlations for SprtTemperature, ReferenceTemperature, and SprtOhms.


# 6. Statical Analysis

In this section, `Statical Analysis/2_Second_Lab.ipynb`, You can find several stages for exploratory data analysis, separability between groups, and hypothesis testing:


- **Advanced data management with Pandas**: The Pandas library is used to clean, preprocess, and structure the dataset for further analysis. Possible missing data and outliers or inconsistencies within the dataset are reviewed. 


- **Feature extraction using object-oriented programming**: In this section, exploratory analysis is prepared by thoroughly cleaning the structure and types. The creation of variables such as Correction and Time allows the accuracy, stability, and repeatability of the SPRT to be studied in comparison with the reference thermometer.
Depending on the type of schedule or shift, the stability and repeatability of the system between different shifts is summarized graphically to detect consistency, differences, evaluate uniformity, and identify outliers.
In this section, we can observe and analyze the separability between classes per shift and the two-dimensional relationships between physical variables. The diagonal (KDE) shows the distribution of each variable per shift. 


- **Feature extraction**: This section uses ANOVA, Fisher's Discriminant Test, and PCA to determine whether the means of the variables are significant between the morning, afternoon, and night shifts.


- **Performance metrics**: The database contains continuous and temporal variables such as ReferenceTemperature, SprtTemperature, SprtOhms, and correction, among others. For this reason, it should be evaluated using continuous or time series models:

* RMSE: measures the root mean square error in °C.
* MAE: measures the mean deviation in °C.
* r: near-perfect linear correlation.
* R²: SPRT explains almost all the variation in the reference.

# 7. Conclusions

* The separability analysis performed using histograms, KDE curves, boxplots, and pairplots showed that the main variables of the process ReferenceTemperature, SprtTemperature, and SprtOhms have highly coincident distributions among the different groups defined in the database. The density curves and scatter plots showed an overlap between classes, indicating that the data come from a very stable and uniform environment. The variations observed in the measurements can be attributed solely to natural noise in the measurement system due to environmental conditions and not to systematic differences between the groups.

* The two-dimensional separability graphs reinforce the conclusion that no regions or characteristic data were observed where any class was grouped differently, nor were any geometric patterns or boundaries identified that would indicate the existence of subpopulations within the dataset. This overlap confirms that the behavior of the SPRT and the reference system remained stable over time and that there are no effects derived from the shift or measurement schedule.

* The results of hypothesis tests such as ANOVA agree that there are no statistically significant differences between the groups compared on the measurement days. The high “p” values in all tests show that the means, medians, and complete distributions are equivalent between classes. This confirms that the groups do not represent measurements with significant differences.

* No external factors were detected that could affect measurements between days, nor was there any additional variability associated with the defined classes. This behavior confirms that the experiment was carried out under controlled conditions and that both the triple point of water and the SPRT remained in a stable and uniform state of thermal equilibrium throughout the process.


# 8. Bibliographic Reference

* Wiandt, T. J. (2007). SPRT Calibration Uncertainties and Internal Quality Control at a Commercial SPRT Calibration Facility

* Comité Internacional de Pesas y Medidas [CIPM]. (1989). Escala Internacional de Temperatura de 1990 (EIT-90). París: Bureau International des Poids et Mesures (BIPM).

* Bohórquez, A. J., Hernández, J. D., & Castro, H. (2023). Implementación de un nuevo sistema de calibración de termómetros de contacto por puntos fijos en el Instituto Nacional de Metrología. Revista EIA, 20(39), 1–18. https://doi.org/10.24050/reia.v20i39.1639