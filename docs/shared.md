# SHARED
<!-- From these links:
https://www.lib.uchicago.edu/about/news/uchicago-launches-shared-a-new-data-platform-for-research-collaboration-and-discovery/ -->

## What is SHARED?

The University of Chicago has received funding from the National Science Foundation (NSF) under Award No 2346746, to develop SHARED, the Secure Hub for Access, Reliability, and Exchange of Data. This new storage platform will advance research through robust capabilities for data storage, accessibility, sharing and integration with national and global data federations. It will provide critical storage capacity for research and supporting data science curricula development and education. For more
information please see [the reference](https://dl.acm.org/doi/10.1145/3708035.3736042).

Designed as a cornerstone of UChicago's data lifecycle strategy, from collection and analysis to publication and archiving, SHARED will integrate with the University’s institutional repository, Knowledge@UChicago, and connect to national research networks like the Open Science Grid (OSG). The SHARED project and platform is led by the University of Chicago Library and Research Computing Center (RCC), with contributions from University IT Services, Data Science Institute, and Physical Sciences Division.

The SHARED platform will be essential for enabling partner faculty to meet federal requirements for data management and sharing. By supporting projects in fields ranging from cosmology and particle physics to linguistics and neuroscience, SHARED will help scientists store, access, and share massive datasets that drive discovery. Examples include data from dark matter searches, cosmic microwave background surveys, large-scale astrophysical simulations, high energy physics experiments, and research on language, learning, and memory. Specific projects include Cosmic Reionization on Computers, Function of Coordinated Hippocampal-cortical Activity in Learning, Grammatical Variation and Change in Sign Languages, How Children Use Gestures with Language, Kinetic Simulations of Astrophysical Plasmas, KOTO particle physics experiment probing rare Kaon decay, and, XENON underground physics experiment searching for dark matter using liquid Xenon detectors, and the South Pole telescope that studies the cosmic microwave background from Antarctica.

## Allocations

The storage allocations for SHARED are prescribed by the grant. The group ownership of the project directories under `/shared` has been assigned to the main PIs of the SHARED grant. 

There are reservations of 50 TB will be reserved for educational, broader impact, and outreach activities, including open pedagogical data sets. In addition, an initial 50 TB will be reserved for open access data repositories for published research findings and the data that can be used to verify the published findings in accordance with FAIR principles. Allocation policies will be reviewed periodically by the SHARED executive committee.

## Access

For the group members of the PIs of the grant, the SHARED storage system can be accessed via:

* Mount point in the Midway3 login nodes `/shared`
* Mount point in the Midway2 and DaLI login nodes `/shared`
* Through gateway services such as the [Globus](globus/share-files.md) endpoint `UChicago RCC SHARED`

Data can be transferred between `/shared` and other [storage spaces](storage/main.md) in the Midway ecosystem using command line interface tools such as `cp`, `scp`, `rsync` and `rclone`.

## Troubleshooting

For further assistance, please send an email to [shared@rcc.uchicago.edu](mailto:shared@rcc.uchicago.edu) and [contact our Help Desk](https://rcc.uchicago.edu/support-and-services/consulting-and-technical-support){:target="_blank"}
