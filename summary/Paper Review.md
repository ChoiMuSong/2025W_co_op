This document is raw memo.
Summary will be refined soon.

trigger-based recording, inadequate time synchronization, and
insufficient trust preservation
This paper presents
a novel black box system designed to overcome these chal
lenges by integrating GPS-based time synchronization and
continuous Electronic Control Unit authentication leveraging
Unified Diagnostic Services.
connected vehicles
A major challenge in automotive digital forensics is data
collection, as highlighted by [8]. Few studies have proposed
reliable forensic tools or extraction techniques, and the lack of
established guidelines or standards renders the field relatively
immature.

 Event Data Recorder (EDR), telem
atics/infotainment (T/I) systems, Electronic Control Units
(ECUs), eCALL units, key fobs, cameras, and Vehicle Con
trol History (VCH) data. 

Additionally, both EDR and VCH are trigger-based
systems—data is only recorded following predefined events
(e.g., a collision) and may be overwritten if no trigger occurs.

A
lack of global time synchronisation across ECUs leads to
inconsistencies in event reconstruction, weakening the accu
racy of forensic timelines.

The absence of trust preservation
mechanisms, such as continuous ECU authentication, raises
concerns about data authenticity, as logs could originate from
unauthorised sources. 

Notably, the T/I system—identified by
[9] as a key source of time and location data—is also a com
mon target for cyberattacks, as it often serves as the primary
access point.

To address these critical gaps, this study proposes a novel
black box system to improve forensic readiness in modern
vehicles.

Time Synchronisation: None of the reviewed works ad
equately address the need for independent and reliable
global time synchronisation, which is essential for accu
rate event reconstruction.
• Trust Preservation: Existing cryptographic approaches
often neglect Zero Trust principles, leaving networks
vulnerable to persistent malicious attacks [19]. Continu
ous authentication is critical to verify ECU, which is the
source for every CAN frame.
• Comprehensive Logging: Many proposed systems focus
on specific components (EDR) and fail to introduce ad
ditional features that would support fundamental require
ments of a digital forensic, e.g. time synchronization and
trust preservation

1. Identify Problem: Insufficient data for Automotive Dig
ital Forensic.
2. DefineObjectives: Develop a system to increase vehicle
digital forensic readiness.
3. Design and Development: Black box logger with added
GPS time, location, and ECU authentication.
4. Demonstration: Proof of concept with commercially off
the shelf hadware and custom software.
5. Evaluation: Asses effectiveness, performance, and secu
rity. From this particular step, it is possible for the DSR
process to cycle around to step "Define Objectives" or
"Design and Development".
6. Communication: Submitted to journal or conference.

 black boxes typically include the
following features:
• Crash-Survivable Memory;
• Continuous Data Recording with Pre-Event Buffering;
• Tamper-Proof Design;
• Multimodal Data Capture;
• Independent Power Supply.

Based on [22], the
general features of an automotive black box include:
• Tamper-Evident Enclosure;
• High Frequency Sampling;
• Submersion Resistance;
• Time Synchronisation;
• Multi-Type Data Recording

Black box systems offer various advanced features, but this
study focuses on three essential functions: time synchroni
sation, multi-type data recording, and continuous authentica
tion—key to ensuring reliable forensic evidence and support
ing legal admissibility.

The black box system comprises three core components: a
hardware module, a GPS module, and an authentication sys
tem. 

The
black box software reads GPS output and appends time and
location data alongside CAN data and the internal clock (used
as a secondary time source). Both timestamps are recorded
simultaneously to provide redundancy and ensure reliable
temporal data in case of failure in either system.

a CAN
network simulates three critical ECUs (Engine Control, Brake
Control, Airbag Control Modules)

Contin
uous authentication maintains a legitimate ECU inventory
on the CAN bus, while logging provides temporal evidence
of unauthorised modifications or intrusions. 

For instance, sudden brake failure can be traced
to driver error (through input logs), manufacturing defects
(through ECU performance history), or malicious interfer
ence (through ECU authentication logs).

By incorporating GPS-based time synchro
nisation, continuous ECU authentication, and comprehensive
data collection capabilities, the system improves upon the
existing logging mechanisms. The integration of temporal
and spatial data coupled with authentication mechanism
enhances the credibility and legal admissibility of forensic
evidence. 