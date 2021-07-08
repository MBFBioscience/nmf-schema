.. image:: Figures/MBFLogo_GrayScale.jpg
    :width: 108px
    :align: right
    :height: 70px
    :target: https://www.mbfbioscience.com/


Development Process
===================

Neuromorphological Format Editors
---------------------------------

The Neuromorphological File Format :doc:`Editors </Election>` are devoted experts who approve official specification documents, correct errors, assess enhancement proposals, and manage revisions to Neuromorphological Data File. They are elected by the Neuromorphological Data File community and serve for 3-year terms as volunteers. The current Neuromorphological Data File editorial board may be contacted via their mailing list, nmf-editors@mbfbioscience.com. The process by which members of the Neuromorphological Data File editorial board are elected is documented :ref:`here <electionprocess>`.

Requests and Issue Reports
--------------------------
| **Procedure Version Date: June 25th, 2021**
| Anyone (whether they are a member of the neuromorphological file format community or not) may raise an issue or record a request using this `webform <https://docs.google.com/forms/d/e/1FAIpQLSfpZp01OH4UGimf8U3ynUGXPT2_UdQGHYU43HAPUE9yTylcZg/viewform?usp=sf_link>`_. Any changes to the file format proposed by MBF Bioscience must also follow the requests and issue reports and approval process described below. The Neuromorphological File Format Editors also use the format’s Wrike space to log issues and discussions about those issues.


The following is the intended sequence of events in the life of an issue. 

1. Preliminary Actions
^^^^^^^^^^^^^^^^^^^^^^

   a. The issue is entered into the Wrike tracking system by someone. The tracking system defaults new issues to a status of Needs Attention and adds these tickets to either the NMF Reported or Proposed folder. The Neuromorphological File Format Editors mailing list will be automatically notified of the new issue.

   b. The first available person from the Neuromorphological File Format Editors to examine the report will do a preliminary evaluation of whether the issue is genuine. Spam may be deleted. Otherwise, they may assign the ticket to themselves, signifying that the issue is genuine, and beginning to moderate discussion among the Neuromorphological File Format Editors in analyzing and discussing the issue. 

2. Evaluation and discussion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   a. The Editors will begin by investigating whether the issue is new or not. If not, the status is changed to Duplicate Request.

   b. The ticket owner will lead the Neuromorphological File Format Editors in discussing the issue and how to resolve it. This takes place by attaching comments in the tracking system.

   c. Editors can indicate at any time their acceptance of a proposed action or rejection. New solutions to the issue may also be proposed.

3. Resolution
^^^^^^^^^^^^^

   a. If the ticket regards a simple matter such as a formatting error, the ticket resolution does not require a majority; they can be acted upon by a single Editor and the issue closed by that Editor after they made the relevant change(s). If any other Editors disagree with the action, they can reopen the issue and call for the issue to follow the process below.

   b. In other cases, a majority consensus will eventually arise from the editors. A supermajority of 4 out of 5 editors is preferred, but some issues may become stalemated at a 3 out of 5 majority. In those cases, the MBF Representative’s opinion should be included in the discussion, and if the 2 minority-opinion Editors wish, the community may be polled via the neuromorphological file format list serve.

.. note::  If the MBF Representative or any of the Editors call for closure on an issue where consensus has not been reached, then Editors should make their opinions known within two weeks of the call for closure. If a majority opinion has not been reached by the end of two weeks, the MBF Representative’s vote may be counted as the tie-breaking vote in the event of a tie. The minority-opinion Editor(s) may still request that the community be polled on the issue.

..

   c. Once a conclusion has been reached (whether by votes or by polling the community), if the conclusion is to accept the issue and make a change, the ticket owner will change the issue’s status to Awaiting Fix. 

.. note::
   There are three versions:
   
   1. Accepted: Formatting/non-content editing: These are formatting or other issues that do not fundamentally change any textual content of the specification document.
   
   2. Accepted: Changes without conformance implications: These are issues that change the text, but do not affect software in a way that may alter their conformance with the file specification. For example, a change to some terminology in file specification would not fundamentally change the modeling formats, and therefore would not be considered a change having conformance implications.
   
   3. Accepted: Changes with conformance implications: These are changes that do affect the conformance of software reading, writing and/or processing data in neuromorphological file format.
   
      a. If MBF products will adopt the change: the issue is added to the MBF Bioscience development tracking space (Pivotal) by the MBF Representative. 
      
      b. If MBF products will skip over the change because it is not relevant or it is out of scope, this is noted on the ticket and in the specification. The editorial board’s MBF Representative is responsible for determining this. 

..

   d. On the other hand, if the conclusion is to make no change, the ticket owner will change the issue’s status to Rejected.

4. Post-resolution
^^^^^^^^^^^^^^^^^^

   a. If the reporter has selected “Keep me informed” and provided an email in the ticket, the case owner is responsible for alerting the reporter of the ticket resolution. 

   b. Following completion, the bug should be put into the next release folder so that it can be reported to the yearly change log. MBF Bioscience is responsible for creating and sharing the yearly change log to the nmf-community@mbfbioscience.com list serve.

   c. Eventually, all pending issues are handled by producing a new version release of the affected neuromorphological file format specification. 
   
