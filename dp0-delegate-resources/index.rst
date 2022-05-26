.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _DP0-Delegate-Resources-DP0-Delegate-Homepage:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#####################
DP0 Delegate Homepage
#####################

.. This section should provide a brief, top-level description of the page.

This page includes the guidelines, resources, and activities for DP0 Delegates.

**"DP0 delegate"** is the term for the 600 scientists and students who will have accounts in the Rubin Science Platform (RSP) at the Interim Data Facility (IDF; the Google Cloud) during Data Preview 0 (DP0).
This term has been adopted to reflect DP0 participants’ important roles of representing the broad science community as learners, testers, and providers of feedback, and of sharing the benefits of their DP0 participation with their communities as teachers and colleagues.
Delegates’ DP0-related activities will be supported with resources and infrastructure described on this page.

| **"Getting Started" Checklist**
|   1. Review the :ref:`Delegate-Homepage-Guidelines-Expectations` for DP0 participation.
|   2. Get one of the :ref:`Delegate-Homepage-RSP-Accounts` for DP0 delegates.
|   3. Set up your account in the :ref:`Delegate-Homepage-Forum`.
|   4. Attend one of the :ref:`Delegate-Homepage-Kickoff` (or watch a recording).
|   5. Consider attending the :ref:`Delegate-Homepage-DP0-Virtual-Seminars` (optional).
|   6. Learn about :ref:`Delegate-Homepage-Getting-Support` for DP0.


.. _Delegate-Homepage-Guidelines-Expectations:

Guidelines and expectations
===========================

**Rubin data rights** are required in order to hold an account in the Rubin Science Platform.
All delegates should be aware of their data rights status (please refer to the `Rubin Data Policy <https://docushare.lsst.org/docushare/dsweb/Get/RDO-013>`_).

**Understand the** :doc:`/data-access-analysis-tools/rsp-warnings` **of using the DP0 RSP on a shared-risk basis**.

**Abide by the** :ref:`Delegate-Homepage-Code-of-Conduct`.

**Adhere to the** :ref:`Delegate-Homepage-PubPol`.

| **Use your RSP account!**
| If you're not sure what to do, choose from one of our :ref:`Delegate-Homepage-Delegate-Activities`.


.. _Delegate-Homepage-RSP-Accounts:

Rubin Science Platform accounts
===============================

**Activation:**
Delegates will be contacted by Rubin Observatory staff to provide their `GitHub <http://www.github.com/>`_ username.
All delegates will be invited to join the `rubin-dp0 GitHub Organization <https://github.com/rubin-dp0>`_ and its `delegates team <https://github.com/orgs/rubin-dp0/teams/delegates/members>`_, and must accept this invitation in order to log into the RSP at the Interim Data Facility (IDF; the Google Cloud).
With a browser that is logged in to GitHub, navigate to `data.lsst.cloud <http://data.lsst.cloud>`_ and choose "log in" at upper right.
A pop-up window will ask to "Authorize Rubin Science Platform IDF Production Environment".
Click the green button that says "Authorize lsst-sqre".
Note that this last authorization step will need to be performed after every logout.

**Policies:**
RSP accounts are not transferable and delegates must not share their password with others.
DP0 delegates are being given access to a *shared-risk developmental version* of the RSP and the accompanying documentation.
**Everyone is responsible for their own safe usage of the RSP** and must be familiar with this list of :doc:`/data-access-analysis-tools/rsp-warnings`.

**Deactivation:**
Delegates who are no longer using their accounts and would like to relinquish it to make way for others should submit a GitHub issue in the ``rubin-dp0`` GitHub Organization to let us know, and then leave the ``rubin-dp0`` GitHub Organization.
(Log into GitHub, navigate to `github.com/settings/organizations <https://github.com/settings/organizations>`_, and click on the "Leave" button for the ``rubin-dp0`` Organization.)

**For delegates who need to get a GitHub account:** go to `github.com <http://www.github.com>`_ and select “Sign up” in the upper-right corner.
For participation in DP0 it is not necessary to learn how to use git as a version control system, nor any of the git workflows or command line tools.
GitHub will not be used for RSP accounts during Rubin Observatory Operations, this is a DP0-specific implementation.


.. _Delegate-Homepage-Forum:

Rubin Community Forum
=====================

The `Rubin Community Forum <http://community.lsst.org>`_ is the central hub for all virtual discussions and support.
It is the best place to post your questions about anything and everything related to DP0.
People new to the Rubin Community Forum might appreciate `this video demonstrating how to navigate and post topics to the forum <https://www.youtube.com/watch?v=d_Z5xmkR4P4&list=PLPINAcUH0dXZSx2aY6wTIjLCWiexs3dZR&index=10>`_.

**Accounts:**
Go to `community.lsst.org <http://community.lsst.org>`_ and use the "Sign Up" button at upper-right to create an account.

**Join the DP0 Delegates Group:**
Go to `community.lsst.org/groups <https://community.lsst.org/groups>`_ and join "DP0 Delegates".
This will ensure you have access to the private "Support - DP0 RSP Service Issues" subcategory.
DP0-related news and events are shared as direct messages to this group.
If you want email notifications, set your Community Forum user profile preference for "Email me when I am sent a personal message" to "Always".

| **Find DP0-Related Content and Discussions:**
| - `Support - Data Preview 0 <https://community.lsst.org/c/support/dp0>`_: for all questions and discussions related to DP0. For example, use of the RSP's aspects for science, contents of the DC2 data set, delegate activities, brainstorm new investigations, show-and-tell DP0-related results, etc.
| - "Support - DP0 RSP Service Issues": a private subcategory for technical Q&A and discussion about potential bugs, service outages, etc.
| - `Topics tagged with #dp0 <https://community.lsst.org/tag/dp0>`_ across all categories.


.. _Delegate-Homepage-Kickoff:

DP0 kick-off info sessions
==========================

All **new** delegates in 2022 should plan to attend one of the three live virtual kick-off info sessions, or view the recording.

Delegates who joined DP0 in 2021 do not need to attend a kick-off info session in 2022.

**Connection Info:** `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Recording:** (link to be added here)

| **Schedule:**
| - Session 1: Fri Jul 1 2022 at 09:00 US Pacific, Fri Jul 1 2022 at 16:00 UTC
| - Session 2: Tue Jul 5 2022 at 21:00 US Pacific, Wed Jul 6 2022 at 04:00 UTC
| - Session 3: Wed Jul 6 2022 at 07:00 US Pacific, Wed Jul 6 2022 at 14:00 UTC

Note that the first kick-off info session, on Fri Jul 1 2022 at 09:00 US Pacific, takes place during the first hour of the first of the :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`.

| **Every session will be 1 hour and will cover:**
| - RSP and Community Forum accounts
| - RSP hazards and delegate expectations
| - resources and support for delegates
| - DP0 goals and the road to Rubin Observatory operations


.. _Delegate-Homepage-DP0-Virtual-Seminars:

DP0 virtual seminars
====================

Attendance at any of the following virtual seminars is optional for DP0 delegates.


.. _Delegate-Homepage-DP0-Delegate-Assemblies:

DP0 Delegate assemblies
-----------------------

**Connection Info:** `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Time:** Biweekly on Fridays from 9am to 11am US Pacific (alternating with :ref:`DP0-Delegate-Programming-StackClub`).

The Delegate Assemblies are a live, virtual seminars for DP0 delegates to learn more about DP0, the RSP, and the DC2 data set.
Attendance is optional and all are welcome.

Typically, the first hour contains a presentation or hands-on tutorial, and the second hour is spent in breakout rooms for discussion or co-working on topics suggested by delegates.

Rubin Observatory staff are always available in the main room to answer questions and provide assistance with DP0-related work during breakouts.

Contributed presentations, tutorials, or advance suggestions for breakouts are encouraged from DP0 delegates and Rubin Observatory staff (contact Melissa Graham).

**Schedule:** 

| Fri Jul 1 2022: Special DP0.2 Assembly
| - first hour: :ref:`Delegate-Homepage-Kickoff`
|   -- for *new* DP0 delegates only
| - second hour: "Introduction to the DP0.2 Time-Domain Data Products"
|   -- for experienced DP0 delegates

| Fri Jul 15 2022: TBD
| - first hour:
| - second hour:

| Fri Jul 29 2022: TBD
| - first hour:
| - second hour:

| Fri Aug 26 2022: TBD
| - first hour: 
| - second hour: 


.. _DP0-Delegate-Programming-StackClub:

Stack Club
----------

**Connection Info:**  `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Time:** Biweekly on Fridays from 9am to 11am US Pacific time (alternating with :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`).

`Stack Club <https://github.com/LSSTScienceCollaborations/StackClub>`_ is an open drop-in session for working with the DP0 data set and/or the Rubin Observatory `LSST Science Pipelines <https://pipelines.lsst.io/>`_ (colloquially called "the Stack").
Stack Club sessions begin with a roundtable of what people want to do or learn that day, and then work proceeds as people stay connected via Zoom,
asking questions or having discussions in the main room or breakout rooms as need arises.
Rubin Observatory staff are always present to provide support for DP0 and the RSP.
Everyone is welcome to attend for the full two hours, or just to drop in for a few minutes and ask a question (like an office hour).


.. _DP0-Delegate-Programming-ThirdThursday:

Third Thursday office hour
--------------------------

**Connection Info:**  `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Time:** The third Thursday of every month at 04:00 and 14:00 UTC.

These two time slots serve the Asia-Pacific (APAC) and Europe, the Middle East, and Africa (EMEA) time zones, respectively.
Note that in the western Americas (AMER) time zone, the first slot at 04:00 UTC is actually on Wednesday evening.

**Dates:** Thu Jul 21 2022 (additional dates TBD)

These office hour sessions are open, drop-in discussions designed to compensate for the fact that the time of the Delegate Assemblies was only convenient for DP0 delegates in North and South America, Europe, and Africa.
Everyone is welcome to attend any of these sessions, instead of or in addition to the Delegate Assemblies and the Stack Club sessions.

There is no set agenda for these sessions, but Rubin Observatory staff are always in attendance, and topics are left open to attendees.
For example, delegates could discuss their DP0-related analysis with Rubin Observatory staff and with each other, review the DP0 RSP tutorials together,
collaborate on DP0-related science, and get support from Rubin Observatory staff as needed.

Please see `this Rubin Community Forum topic <https://community.lsst.org/t/invitation-to-join-third-thursday-dp0-office-hours-for-apac-and-emea-timezones/6418>`_ for more information about the Third Thursdays.


.. _Delegate-Homepage-Delegate-Activities:

Suggested delegate activities
=============================

**Learn to use the Rubin Science Platform.**
All delegates are encouraged to use the documentation, instructions, and tutorials to learn how to use the Rubin Science Platform, and its various tools for accessing and analyzing LSST data.

**Prepare to do science with the Data Previews.**
In the coming years, *real commissioning data* from Rubin Observatory will be released as Data Preview 1 and 2.
Use the simulated LSST-like DP0 data set to prepare your custom analysis software, so that you're ready to do early science.

Beyond these two main activities, all delegates are invited to take on an activity that will inform and improve development of the RSP development,
and/or extend and enhance the benefits of DP0 within the science community beyond the limited number of DP0 participants that Rubin Observatory is able to support.

Delegate activities are envisioned to be simple and enjoyable.
They are completely voluntary and will not be tracked.
Group work is encouraged, as are delegate-designed activities.
Have fun!


Inform and improve the RSP
--------------------------

**Participate in feedback surveys.**
When requested, complete the DP0 delegate feedback surveys for Rubin Observatory.
Read about `the results from the first DP0 survey <https://community.lsst.org/t/the-dp0-1-feedback-survey-action-items/6105>`_.

**Submit bug reports.**
Help with RSP improvements by submitting bug reports via `GitHub issues <https://github.com/rubin-dp0/Support>`_ (see :ref:`Delegate-Homepage-Getting-Support`).

**Suggest new features.**
Help with RSP development by suggesting new RSP features via `GitHub issues <https://github.com/rubin-dp0/Support>`_, or by communicating directly with the Rubin `Users Committee <https://www.lsst.org/scientists/users-committee>`_ to advocate for the tools that you need for your LSST science goals.

**Share your experiences with Rubin Observatory staff.**
Post about your DP0 investigations in the `Data Preview 0 <https://community.lsst.org/c/support/dp0>`_ category of the Community Forum, so Rubin Observatory staff can see how users are doing science with the RSP.


Extend the benefits of DP0 in the science community
---------------------------------------------------

**Join an LSST Science Collaboration.** 
There are eight `LSST Science Collaborations <https://www.lsstcorporation.org/science-collaborations>`_, and new members are always welcome.

**Participate in the Rubin Community Forum.**
Ask questions about DP0, or "show and tell" your DP0-related investigations in the `Data Preview 0 <https://community.lsst.org/c/support/dp0>`_ category of the Community Forum.
Respond to questions or discussion topics raised by other DP0 delegates.
This helps to build a global self-supporting network of scientists engaged in LSST reasearch.

**Participate in the DP0 virtual seminars.**
Attend the delegate assemblies, Stack Club, or Third Thursday sessions described above.
Ask questions and join the breakout discussions.
All are welcome to volunteer to facilitate a breakout room or to give a presentation (contact Melissa Graham).

**Contribute tutorial notebooks.**
All delegates are welcome to share their own Jupyter Notebooks using the `delegates' shared repo <https://github.com/rubin-dp0/delegate-contributions-dp02>`_.
Step-by-step tutorials that use the Portal, TAP, or command-line are also welcome.

**Share your DP0-related work outside of DP0.**
For example, give a seminar about Rubin Observatory and DP0 at your home institution, give a tutorial about your RSP/DP0 experience in your Science Collaboration, or publish a paper on your DP0-related work.
Be sure to refer to the :ref:`Delegate-Homepage-PubPol`.


.. _Delegate-Homepage-Getting-Support:

Getting support
===============

Several venues are provided to support DP0 delegates, as described below.
There is no wrong place to post questions or requests for assistance!
Hearing about issues and receiving feedback from delegates is a key component of DP0 for Rubin Observatory staff.

Scientific support via the Community Forum
------------------------------------------

The `Support – Data Preview 0 subcategory <https://community.lsst.org/c/support/dp0/49>`_ is the best place for DP0 delegates to post topics related to scientific support.

Scientific support includes questions about the DC2 simulated data set, the DP0 data products, and/or the application of the LSST Science Pipelines to the DP0 data set, as well as general discussion about DP0-related scientific analyses, or DP0 policies and guidelines.

This subcategory will be monitored by the Rubin Observatory `Community Engagement Team (CET) <https://community.lsst.org/t/about-the-community-engagement-team/4526>`_.
DP0 delegates are especially encouraged to post new topics and reply to others' posts in this subcategory.

Technical assistance via GitHub issues
--------------------------------------

Bug reports, persistent technical issues, and requests for assistance from Rubin Observatory staff should be submitted by DP0 delegates as GitHub issues in the `rubin-dp0 GitHub Organization's Support repository <https://github.com/rubin-dp0/Support>`_.
Requests for new features or for global installations of commonly used software packages are also welcome via GitHub issues.

In the horizontal menu bar at the top of that page, click on the “Issues” option (with the circled dot icon), then choose the green “New Issue” button at right.
Next to either “Bug report” or "Feature request" choose “Get started” (as appropriate for your case), and fill in the title and contents of your issue.
In the right side-menu, do adjust the labels as appropriate, but leave the other options.
Click “Submit new issue” when you’re ready.
These issues will be addressed by Rubin Observatory staff.

Minor or ambiguous RSP service and access issues
------------------------------------------------

Please feel free post even small questions as new topics in the "Support - DP0 RSP Service Issues" private subcategory of the Community Forum.

This subcategory enables DP0 delegates to determine if others are experiencing the same issue (e.g., *"is this local or general network outage?"*, *"my query is taking a long time, is this a real problem or did I do it wrong?"*),
crowd-source solutions to technical issues from each other when possible, and have a non-public venue for DP0-related questions.
Updates about commonly experienced access issues or planned service outages will be posted by Rubin Observatory staff in this category.

Since the "DP0 RSP Service Issues" subcategory is not public, it cannot be linked to directly, but anyone who is logged in to the Community Forum can access it via the main landing page at `community.lsst.org <https://community.lsst.org>`_.

Read more in the Community Forum about `Scientific Support and Technical Assistance for DP0 Delegates <https://community.lsst.org/t/scientific-support-and-technical-assistance-for-dp0-delegates/5485>`_.

Live support
------------

Bring your questions to the Delegate Assemblies, third Thursday office hours, or Stack Club meetings.
Rubin Observatory staff members will usually be in attendance and able to assist you.


.. _Delegate-Homepage-Code-of-Conduct:

Code of conduct
===============

Please review the Rubin Code of Conduct (CoC) at `ls.st/comms-coc <http://ls.st/comms-coc>`_.

| To summarize the CoC:
| - Bullying and harassment will not be tolerated.
| - Research inclusion and collaborative work must not be impeded by poor behavior.
| - Discussion should be constructive and civil at all times.

If you experience or witness a violation of the CoC in the Community Forum, please `flag the post <https://community.lsst.org/t/how-and-why-to-flag-a-post>`_.
Forum moderators will handle the issue from there.
Please note that there are a few reasons why posts get flagged, and CoC violations are only one of them.
Here are some guidelines on `how to react if your post is flagged <https://community.lsst.org/t/how-to-react-if-your-post-is-flagged>`_.

If you experience or witness a violation of the CoC in another venue, please reach out to Sandrine Thomas, one of the `Rubin Observatory Workplace Culture Advocates <https://project.lsst.org/workplace-culture-advocate>`_ who has agreed to be the contact person for DP0 Delegates.
Please also feel free to reach out to any Community Engagement Team member at any time: Melissa Graham, Jeff Carlin, Greg Madejski, Jim Annis, Alex Drlica-Wagner, or Tina Adair.
All can be contacted by email or via direct message in the Community Forum.


.. _Delegate-Homepage-PubPol:

Policies for acknowledgments, citations, and publications
=========================================================

**Cite the DESC’s publications for the DC2 simulated data set**, which is being used for DP0.
If you publish work based on the DP0 data set, you must cite “CosmoDC2: A Synthetic Sky Catalog for Dark Energy Science with LSST”
(`Korytov et al 2019 <https://ui.adsabs.harvard.edu/abs/2019ApJS..245...26K/abstract>`_), “The LSST DESC DC2 Simulated Sky Survey” (`arXiv:2010.05926 <https://arxiv.org/abs/2010.05926>`_),
and potentially “DESC DC2 Data Release Note” (`arXiv:2101.04855 <https://arxiv.org/abs/2101.04855>`_) if you used the Object or Truth-Match tables, which are presented in that release note.

**Consider extending co-authorship or acknowledgments to DP0 delegates whose work you used, or who have helped you, as appropriate.**
Delegates are encouraged to openly share their DP0-related work and/or code during :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`, via the `Community Forum <https://community.lsst.org/>`_,
within :ref:`Delegate-Homepage-Working-Groups`, and in the shared GitHub repository `delegate-contributions-dp01 <https://github.com/rubin-dp0/delegate-contributions-dp01>`_.
This is intended to facilitate collaboration, which requires proper acknowledgments.
For example, if you use another delegate’s Jupyter Notebook as a starting point for your Notebook, give credit to that person at the top of your Notebook.
If another delegate’s work contributed to your DP0-related publication, consider including an acknowledgment, citing their relevant publications, and/or extending co-authorship, as appropriate.

**Be aware that DP0-related work done by Science Collaboration (SC) members might be subject to the publication policies of their Science Collaborations.**
Significant overlap between the DP0 working groups and SC working groups, committees, or task forces is to be expected, because the science goals of DP0 and the SCs overlap (i.e., preparing for LSST).
Each SC has their own policies regarding collaboration, co-authorship, and publications and delegates are responsible for following the policies of their SCs, if and when they pertain to their DP0-related work.
If cases of real or perceived conflict between the general open nature of DP0 collaboration and any SC policies arise, delegates are expected to understand and abide by their SC’s policies.
In other words, the fact that work is DP0-related does not nullify any SC policies that might apply to a delegate’s work.
Example scenarios might include sharing SC-developed software with delegates who are not members of that SC, or using code or analysis results collaboratively by delegates in a SC publication.

Note that the `Rubin Observatory Publication Policy <https://docushare.lsst.org/docushare/dsweb/Get/LPM-162>`_ does not apply to publications by delegates that are based on their DP0 work.
