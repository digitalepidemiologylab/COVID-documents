# COVID-19: Digital Contact Tracing and Quarantine

Author: Prof. Marcel Salathé, EPFL

Last updated: April 22, 2020

This document is continuously updated to reflect my current thinking around digital contact tracing and quarantining. This is not an official document, but a personal record keeping. I want to do this in the open becuase a) I believe transparancy is paramount for these issues; b) I will be wrong on many things, and open discussion is the fastest way to correct things; and c) it could help others, in the best case.

## Overview
A digital contact tracing system to fight COVID is based on the notion that droplets are a major transmission route. This is the current thinking in the scientific community, and reflected in the [WHO Situation Report 73](https://www.who.int/docs/default-source/coronaviruse/situation-reports/20200402-sitrep-73-covid-19.pdf?sfvrsn=5ae25bc7_6)  released on April 2: "Data from published epidemiology and virologic studies provide evidence that COVID-19 is primarily transmitted from symptomatic people to others who are in close contact through respiratory droplets, by direct contact with infected persons, or by contact with contaminated objects and surfaces." A digital system that capture close proximity contacts should be able to caputre the first two types of contacts.

Worryingly, a substantial fraction of transmission ([anywhere](https://www.nature.com/articles/s41591-020-0869-5) between [40% and 60%](https://www.medrxiv.org/content/10.1101/2020.03.05.20031815v1)) occurs in the pre-symptomatic stage, i.e. before the onset of symptoms. Thus, a containement strategy that only focuses on the isolation of symptomatic cases is bound to fail. Contact tracing can help identify contacts of an index case and quarantime them before the onset of symptoms, thereby preventing ongoing submissions. [Previous work has shown that this is possible](https://science.sciencemag.org/content/early/2020/04/09/science.abb6936), specifically also with the aid of digital contacting tracing.

Digital contact tracing, which is thought to complement classical contact tracing, is leveraging the fact that the vast majority of people use bluetooth-enabled smartphones. While the bluetooth protocol was not developed to measure the distance between devices, it does contain information about the signal strength which can be leveraged to estimate distance. This is not trivial, but ongoing work is showing that it is feasible. It's of course not going to be precise down to the centimeter, but let's not forget the droplet range (~2 meters) is an equally rough estimate. Overall, one should be able to estimate if two devices have been in sufficient proximity, for a sufficient amount of time, to conclude that a droplet transmission from an  infected to a susceptible person could have occured.

Recent discussions around the development of such digital contact tracing systems have for some time focused on the question of "centralized vs. decentralized". Centralized approaches argue that contact data should be collected on a trusted central server. Decentralized approaches argue that contact data should remain on devices, without the need to store such data on a server. A privacy and security risk evaluation of digital proximity tracing systems by the DP3T (decentralized privacy-preserving proximity tracing) group can be found [here](https://github.com/DP-3T/documents/blob/master/Security%20analysis/Privacy%20and%20Security%20Attacks%20on%20Digital%20Proximity%20Tracing%20Systems.pdf). Whatever the approach, digital contact tracing systems always need an input, i.e. the trigger of an infected person; and they always produce an output, i.e. the alerts of contacts of the infected person. Thus, any strategy involving digital contact tracing system needs to address two key questions: 1. Who triggers the process, and how; and 2. what happens after the contacts have been alerted?

In this document, I hope to address some of the questions around this process. Again, this is work in progress - if you have  comments, questions, or any other input, please let me know.

## Epidemiology

### Who needs to go into quarantine?
A substantial fraction of transmisison ([anywhere](https://www.nature.com/articles/s41591-020-0869-5) between [40% and 60%](https://www.medrxiv.org/content/10.1101/2020.03.05.20031815v1)) occurs in the pre-symptomatic stage, 1-3 days before the onset of symptoms. Thus, because people can be contagious without having symptoms (yet), quarantine should not depend on the presence of symptoms, but on the suspicion of being infected (through contacts with a confirmed infected case). In addition, quarantine should not be conditional on testing. After exposure to an infected person, a negative PCR test at time point `t` cannot exclude that a person will become contagious at timepoint `t+1`. It simply means that the viral load in the potentially infected person has not yet reached sufficiently high levels to be detected by PCR tests at time `t`. As this phenomenon cannot be excluded during the entire quarantine time, PCR tests are not necessary for quarantine protocols, but should be used for epidemiological data collection (if test capacities allow).

The definition of a potential contact should follow standard protocols. Most protocols define a close contact [as being < 2  meters distance for at least 15 minutes](https://www.hpsc.ie/a-z/respiratory/coronavirus/novelcoronavirus/guidance/contacttracingguidance/National%20Interim%20Guidance%20for%20contact%20tracing_v8_03.04.2020.pdf).

### What is the duration of quarantine?
The temporal distribution of the incubation period is estimated to have a median of around 5 days, up to 14 days (longer incubation periods have been [reported](https://jamanetwork.com/journals/jama/fullarticle/2762028) but are extremely rare). Given that [the 95% percentile was reported at 12.5 days](https://www.nejm.org/doi/full/10.1056/NEJMoa2001316), and the fact that most contacts were a few days before the contact was alerted, a quarantine duration of 10 days would be justified.

### What is the role of tests?
In order to trigger contact tracing, an index case needs to be diagnosed as SARS-CoV-2 positive. Such a diagnosis should ideally be confirmed by a PCR test, but should ultimately be made by a health care professional (who may decide that the symptoms are clear enough for a diagnosis, and PCR tests may be limited). Following such a diagnosis, a contact tracing process should be again, which can either be traditional, or digital (or both). In the digital version, the patient would obtain a code from the entity that made the diagnosis, which also encodes the estimated onset date of symptoms. Upon entering this code, the DP3T-based app then broadcasts the users identifiers, and other apps will locally check whether the index case  has been in contact with them during the epidemiological relevant time window (see above - up to 3 days before the onset of symptoms). If so, the app will show an alert with the invitation to contact the health authorities.

Serological tests are of limited use in a contact tracing system. People with established immunity are not susceptible anymore, and most likely not infectious. Thus, neither isolation nor quarantine protocols apply to them. However, establishing immunity with sufficient accuracy is challenging, and given the currently low prevalence estimates almost everywhere, serology  test should be used with great care.

Importantly, PCR tests should not be used to *determine* quarantine of the contacts. Upon exposure from a confirmed index case, a contact may habe been infected, but not have a high enough viral load for a PCR test to detect. Thus, a negative PCR test cannot exclude, at any time during the quarantine period, that the person will soon become contagious. That said, regular testing with quarantined people will be important from an epidemiological and clinical perspective.

### What fraction of the population needs to participate for this to be effective?

Early results have shown that 

## Operational

### How many contact tracers are needed?
As per a report by the [Center for Health Security](https://www.centerforhealthsecurity.org/our-work/pubs_archive/pubs-pdfs/2020/a-national-plan-to-enable-comprehensive-COVID-19-case-finding-and-contact-tracing-in-the-US.pdf), the estimated human resources (contact tracers) are between 4 - 81 per 100,000 population (15 in Massachusetts, 4 in New Zealand, 81 in Wuhan, 7 in Iceland). The numbers are of course dependent on disease incidence. Overall, a contact tracing capacity of ~100-150 per Million seems adequat.
