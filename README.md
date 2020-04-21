# COVID-19: Digital Contact Tracing and Quarantine

Author: Prof. Marcel Salathé, EPFL

Last updated: April 21, 2020

This document is continuously updated to reflect my current thinking around digital contact tracing and quarantining. This is not an official document, but a personal record keeping. I want to do this in the open becuase a) I believe transparancy is paramount for these issues, b) I will be wrong on many things and open discussions is the fastest way to correct things, and c) it could help others, in the best case.

## Overview
A digital contact tracing system to fight COVID is based on the notion that droplets are a major transmission route. This is the current thinking in the scientific community, and reflected in the [WHO Situation Report 73](https://www.who.int/docs/default-source/coronaviruse/situation-reports/20200402-sitrep-73-covid-19.pdf?sfvrsn=5ae25bc7_6)  released on April 2: "Data from published epidemiology and virologic studies provide evidence that COVID-19 is primarily transmitted from symptomatic people to others who are in close contact through respiratory droplets, by direct contact with infected persons, or by contact with contaminated objects and surfaces." A digital system that capture close proximity contacts should be able to caputre the first two types of contacts.

Worryingly, a substantial fraction of transmisison ([anywhere](https://www.nature.com/articles/s41591-020-0869-5) between [40% and 60%](https://www.medrxiv.org/content/10.1101/2020.03.05.20031815v1)) occurs in the pre-symptomatic stage, i.e. before the onset of symptoms. Thus, a containement strategy that only focuses on the isolation of symptomatic cases is bound to fail.

