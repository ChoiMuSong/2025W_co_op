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