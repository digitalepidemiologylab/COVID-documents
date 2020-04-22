# COVID-19: Digital Contact Tracing and Quarantine

Author: Prof. Marcel Salathé, EPFL

Last updated: April 21, 2020

This document is continuously updated to reflect my current thinking around digital contact tracing and quarantining. This is not an official document, but a personal record keeping. I want to do this in the open becuase a) I believe transparancy is paramount for these issues, b) I will be wrong on many things and open discussions is the fastest way to correct things, and c) it could help others, in the best case.

## Overview
A digital contact tracing system to fight COVID is based on the notion that droplets are a major transmission route. This is the current thinking in the scientific community, and reflected in the [WHO Situation Report 73](https://www.who.int/docs/default-source/coronaviruse/situation-reports/20200402-sitrep-73-covid-19.pdf?sfvrsn=5ae25bc7_6)  released on April 2: "Data from published epidemiology and virologic studies provide evidence that COVID-19 is primarily transmitted from symptomatic people to others who are in close contact through respiratory droplets, by direct contact with infected persons, or by contact with contaminated objects and surfaces." A digital system that capture close proximity contacts should be able to caputre the first two types of contacts.

Worryingly, a substantial fraction of transmisison ([anywhere](https://www.nature.com/articles/s41591-020-0869-5) between [40% and 60%](https://www.medrxiv.org/content/10.1101/2020.03.05.20031815v1)) occurs in the pre-symptomatic stage, i.e. before the onset of symptoms. Thus, a containement strategy that only focuses on the isolation of symptomatic cases is bound to fail. Contact tracing can help identify contacts of an index case and quarantime them before the onset of symptoms, thereby preventing ongoing submissions. [Previous work has shown that this is possible](https://science.sciencemag.org/content/early/2020/04/09/science.abb6936), specifically also with the aid of digital contacting tracing.

Digital contact tracing, which is thought to complement classical contact tracing, is leveraging the fact that the vast majority of people use bluetooth-enabled smartphones. While the bluetooth protocol was not developed to measure the distance between devices, it does contain information about the signal strength which can be leveraged to estimate distance. This is not trivial, but ongoing work is showing that it is feasible. It's of course not going to be precise down to the centimeter, but let's not forget the droplet range (~2 meters) is an equally rough estimate. Overall, one should be able to estimate if two devices have been in sufficient proximity, for a sufficient amount of time, to conclude that a droplet transmission from an  infected to a susceptible person could have occured.

Recent discussions around the development of such digital contact tracing systems have for some time focused on the question of "centralized vs. decentralized". Centralized approaches argue that contact data should be collected on a trusted central server. Decentralized approaches argue that contact data should remain on devices, without the need to store such data on a server. A privacy and security risk evaluation of digital proximity tracing systems by the DP3T (decentralized privacy-preserving proximity tracing) group can be found [here](https://github.com/DP-3T/documents/blob/master/Security%20analysis/Privacy%20and%20Security%20Attacks%20on%20Digital%20Proximity%20Tracing%20Systems.pdf). Whatever the approach, digital contact tracing systems always need an input, i.e. the trigger of an infected person; and they always produce an output, i.e. the alerts of contacts of the infected person. Thus, any strategy involving digital contact tracing system needs to address two key questions: 1. Who triggers the process, and how; and 2. what happens after the contacts have been alerted?

In this document, I hope to address some of the questions around this process. Again, this is work in progress - if you have  comments, questions, or any other input, please let me know.

## Epidemiology

### Who needs to go into quarantine?
A substantial fraction of transmisison ([anywhere](https://www.nature.com/articles/s41591-020-0869-5) between [40% and 60%](https://www.medrxiv.org/content/10.1101/2020.03.05.20031815v1)) occurs in the pre-symptomatic stage, 1-3 days before the onset of symptoms. Thus, because people can be contagious without having symptoms (yet), quarantine should not depend on the presence of symptoms, but on the suspicion of being infected (through contacts with a confirmed infected case). In addition, quarantine should not be conditional on testing. After exposure to an infected person, a negative PCR test at time point t cannot exclude that a person will become contagious at timepoint t+1. It simply means that the viral load in the potentially infected person has not yet reached sufficinetly high levels to be detected by PCR tests at time t. As this phenomenon cannot be excluded during the entire quarantine time, PCR tests are not necessary for quarantine protocols, but should be used for epidemiological data collection (if test capacities allow).

The definition of a potential contact should follow standard protocols. Most defintions define a close contact as being < 2  meters distance for at least  15 minutes.

## Operational

### How many contact tracers are needed?
As per a report by the [Center for Health Security](https://www.centerforhealthsecurity.org/our-work/pubs_archive/pubs-pdfs/2020/a-national-plan-to-enable-comprehensive-COVID-19-case-finding-and-contact-tracing-in-the-US.pdf), the estimated human resources (contact tracers) are between 4 - 81 per 100,000 population (15 in Massachusetts, 4 in New Zealand, 81 in Wuhan, 7 in Iceland). The numbers are of course dependent on disease incidence. Overall, a contact tracing capacity of ~100-150 per Million seems adequat.
