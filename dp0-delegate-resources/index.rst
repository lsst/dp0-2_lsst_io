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

**"DP0 delegate"** is the term for the 300 scientists and students who will have accounts in the Rubin Science Platform (RSP) at the Interim Data Facility (IDF) during Data Preview 0 (DP0).
This term has been adopted to reflect DP0 participants’ important roles of representing the broad science community as learners, testers, and providers of feedback,
and of sharing the benefits of their DP0 participation with their communities as teachers and colleagues.

Delegates’ DP0-related activities will be supported with resources and infrastructure described on this page.
The simulated data set being used for DP0 was created by the Dark Energy Science Collaboration (DESC) as part of their second Data Challenge (DC2; `arXiv:2010.05926 <https://arxiv.org/abs/2010.05926>`_).

| **"Getting Started" Checklist**
|   1. Review the :ref:`Delegate-Homepage-Guidelines-Expectations` for delegates.
|   2. Get one of the :ref:`Delegate-Homepage-RSP-Accounts` for DP0 delegates.
|   3. Set up your account in the :ref:`Delegate-Homepage-Forum`.
|   4. Watch the recorded :ref:`Delegate-Homepage-Kickoff`.
|   5. Consider attending the :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`.
|   6. Learn about :ref:`Delegate-Homepage-Getting-Support` for DP0.


.. _Delegate-Homepage-Guidelines-Expectations:

Guidelines and expectations
===========================

**Understand the** :doc:`/data-access-analysis-tools/rsp-warnings` **of using the DP0 RSP on a shared-risk basis**.

**Abide by the** :ref:`Delegate-Homepage-Code-of-Conduct`.

**Adhere to the** :ref:`Delegate-Homepage-PubPol`.

| **Use your RSP account!**
| Delegates are invited to choose from one of these :ref:`Delegate-Homepage-Delegate-Activities`.


.. _Delegate-Homepage-RSP-Accounts:

RSP accounts
============

**Activation:**
Delegates will be contacted by Rubin Observatory staff to provide their `GitHub <http://www.github.com/>`_ username.
All delegates will be invited to join the `rubin-dp0 GitHub Organization <https://github.com/rubin-dp0>`_
and its `Delegates <https://github.com/orgs/rubin-dp0/teams/delegates/members>`_ team,
and must accept this invitation in order to log into the RSP at the Interim Data Facility (IDF; the Google Cloud).
With a browser that is logged in to GitHub, navigate to `<http://data.lsst.cloud>`_ and choose "log in" at upper right.
A pop-up window will ask to "Authorize Rubin Science Platform IDF Production Environment".
Click the green button that says "Authorize lsst-sqre".
Note that this last authorization step will need to be performed after every logout.

**Policies:**
RSP accounts are not transferable and delegates must not share their password with others.
DP0 delegates are being given access to a *shared-risk developmental version* of the RSP and the accompanying documentation.
**Everyone is responsible for their own safe usage of the RSP** and must be familiar with this list of :doc:`/data-access-analysis-tools/rsp-warnings`, and review the :ref:`Delegate-Homepage-Guidelines-Expectations` for DP0 delegates.

**Deactivation:**
Delegates who are no longer using their accounts and would like to relinquish it to make way for others should submit a GitHub issue in the ``rubin-dp0`` GitHub Organization to let us know, and then leave the ``rubin-dp0`` GitHub Organization.
(Log into GitHub, navigate to `<https://github.com/settings/organizations>`_, and click on the "Leave" button for the ``rubin-dp0`` Organization.)

**For delegates who need to get a GitHub account:** go to `<http://www.github.com>`_ and select “Sign up” in the upper-right corner.
For participation in DP0 it is not necessary to learn how to use git as a version control system, nor any of the git workflows or command line tools.
GitHub will not be used for RSP accounts during Rubin Observatory Operations, this is a DP0-specific implementation.


.. _Delegate-Homepage-Forum:

Rubin Community Forum
=====================

The `Rubin Community Forum <http://community.lsst.org>`_ is the central hub for all virtual discussions and support.
It is the best place to post your questions about anything and everything related to DP0.
People new to the Rubin Community Forum might appreciate `this video demonstrating how to navigate and post topics to the forum <https://www.youtube.com/watch?v=d_Z5xmkR4P4&list=PLPINAcUH0dXZSx2aY6wTIjLCWiexs3dZR&index=10>`_.

**Accounts:**
Go to `<http://community.lsst.org>`_ and use the "Sign Up" button at upper-right to create an account.

**Join the DP0 Delegates Group:**
Go to `<https://community.lsst.org/groups>`_ and join "DP0 Delegates".
This will ensure you have access to the private "Support - DP0 RSP Service Issues" subcategory.

| **Find DP0-Related Content and Discussions:**
|   1. `Support - Data Preview 0 <https://community.lsst.org/c/support/dp0>`_: for all questions and discussions related to DP0. For example, use of the RSP's aspects for science, contents of the DC2 data set, delegate activities, brainstorm new investigations, show-and-tell DP0-related results, etc.
|   2. "Support - DP0 RSP Service Issues": a private subcategory for technical Q&A and discussion about potential bugs, service outages, etc.
|   3. `Topics tagged with #dp0 <https://community.lsst.org/tag/dp0>`_ across all categories.


.. _Delegate-Homepage-Kickoff:

DP0 kick-off info sessions
==========================

All delegates should view the recording if they were unable to attend live.

**Slides and Recording:** `ls.st/clo4989 <https://ls.st/clo4989>`_

| **Contents of the Kick-Off Info Sessions:**
|   -- RSP and Community Forum accounts
|   -- RSP hazards and delegate expectations
|   -- Resources and support for delegates
|   -- DP0 goals and the road to Rubin Observatory operations


.. _Delegate-Homepage-DP0-Delegate-Assemblies:

DP0 Delegate assemblies
=======================

**Connection Info (Zoom and Google Calendar Links):** `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Time:** Biweekly on Fridays from 9am to 11am US Pacific time (alternating with :ref:`DP0-Delegate-Programming-StackClub`; 4pm UTC).
See the :ref:`DP0-Delegate-Programming-Assemblies` for dates.

The Delegate Assemblies are a live, virtual seminars for DP0 delegates to learn more about DP0, the RSP, and the DC2 data set. 

**Assemblies with a formal presentation component** are split into 2 one-hour sections, and all are welcome to join for only the first or second hour, or both hours.
Everyone is welcome to attend, the assemblies are not restricted to delegates.

| **First hour: a "formal" presentation with Q&A**, such as:
|   -- hands-on demonstrations and tutorials by Rubin Observatory staff
|   -- presentations from delegates about their DP0 work
| **Second hour: breakout sessions for discussion**, such as:
|   -- "office hours" for Q&A with Rubin Observatory staff
|   -- in-depth discussion related to the first hour's contents
|   -- grassroots DP0 science working groups and collaborative projects

Everyone is welcome to propose breakout topics for the second hour.
The first five minutes of the second hour will be spent connecting people with similar interests and setting up breakout rooms.

**Assemblies without a formal presentation component** will go straight into breakout rooms.
The first five minutes of the assembly will be spent connecting people with similar interests and setting up breakout rooms.
Everyone is free to join and leave breakout rooms and to work on whatever they like.

Rubin Observatory staff will always be on hand in the main room to answer questions and provide assistance with DP0-related work during breakouts.


.. _DP0-Delegate-Programming-Assemblies:

Assemblies schedule
-------------------

Rows *in italics* are tentative topics.
Please reach out to Melissa Graham with suggestions or contributions (e.g., send her a direct message in the Community Forum).
Suggestions and contributed talks are welcome from anyone, e.g., delegates, Rubin Observatory staff.

.. include:: dp0-delegate-assemblies-schedule.inc


.. _DP0-Delegate-Programming-StackClub:

Stack Club
----------

**Connection Info (Zoom and Google Calendar Links):**  `ls.st/dp0-events <http://ls.st/dp0-events>`_

**Time:** Biweekly on Fridays from 9am to 11am US Pacific time (alternating with :ref:`DP0-Delegate-Programming-Assemblies`; 4pm UTC).

`Stack Club <https://github.com/LSSTScienceCollaborations/StackClub>`_ is a group of LSST Science Collaboration members
committed to learning how to use the Rubin Observatory `LSST Science Pipelines <https://pipelines.lsst.io/>`_ (colloquially called "the Stack").
The idea is that the best way to learn something is to try and teach it, so
Stack Club members create Jupyter Notebook tutorials that feature the Stack.
Many of these notebooks were used to create the DP0 tutorial notebooks.
Sessions begin with a roundtable of what people want to do or learn that day, and then work proceeds as people stay connected via Zoom,
asking questions or having discussions in the main room or breakout rooms.

Rubin Observatory staff are always present to provide support for DP0 and the RSP.
DP0 delegates are very welcome to join the Friday Stack Club sessions,
whether it's for the full two hours or just to drop in for a few minutes and ask a question (like an office hour).
DP0 delegates do not need to formally join Stack Club unless they want to contribute specifically to the Stack Club's repository of tutorial notebooks.


.. _DP0-Delegate-Programming-ThirdThursday:

Third Thursday office hour
--------------------------

**Time:** Thursdays at 04:00 and 14:00 UTC (to serve the Asia-Pacific, APAC, and Europe, the Middle East, and Africa, EMEA, time zones respectively)

**2022 Dates:** 

Please see `this Rubin Community Forum topic <https://community.lsst.org/t/invitation-to-join-third-thursday-dp0-office-hours-for-apac-and-emea-timezones/6418>`_ for more information and connection details.

These office hour sessions are open, drop-in discussions designed to compensate
for the fact that the time of the Delegate Assemblies was only convenient for DP0 delegates in North and South America, Europe, and Africa.
Everyone is welcome to attend any of these sessions, instead of or in addition to the Delegate Assemblies and the Stack Club sessions.

There is no set agenda for these sessions, but Rubin Observatory staff are always in attendance, and topics are left open to attendees.
For example, delegates could discuss their DP0-related analysis with Rubin Observatory staff and with each other, review the DP0 RSP tutorials together,
collaborate on DP0-related science, and get support from Rubin Observatory staff as needed.

| **2021 Information:** July 15, August 19, and September 16 at 9am in Sydney Australia (Wednesday at 4pm US Pacific Daylight Time, 11pm UTC).
| These sessions were not recorded.


.. _Delegate-Homepage-Delegate-Activities:

Suggested delegate activities
=============================

All delegates are invited to take on an activity that will inform and improve development of the RSP development,
and/or extend and enhance the benefits of DP0 within the science community, beyond the limited number of DP0 participants that Rubin Observatory is able to support.

Delegate activities are envisioned to be simple and enjoyable.
They are completely voluntary and will not be tracked.
Group work is encouraged, as are delegate-designed activities.


Inform and improve the RSP
--------------------------

| - complete one or more feedback surveys for Rubin Observatory
|   -- read about `the results from the first DP0 survey <https://community.lsst.org/t/the-dp0-1-feedback-survey-action-items/6105>`_
| - submit bug reports via `GitHub issues <https://github.com/rubin-dp0/Support>`_ (see :ref:`Delegate-Homepage-Getting-Support`)
| - suggest a new RSP feature via `GitHub issues <https://github.com/rubin-dp0/Support>`_
| - post about your experiences in the `Data Preview 0 <https://community.lsst.org/c/support/dp0>`_ forum category
| - communicate directly with the Rubin RSP Users Committee
|   -- *(more information about the Users Committee is forthcoming)*

.. | - participate in calls for user acceptance testing (UAT) **(PLACEHOLDER for link to more UAT info)**
.. |   -- work through an “RSP Test Checklist” and fill out a related form **(PLACEHOLDER for link to checklist and form)**
.. |   -- test that new Notebooks run and fill out a related form **(PLACEHOLDER for link to notebooks and form)**


Extend or enhance the benefits of DP0 in the science community
--------------------------------------------------------------

| - join one of the eight `LSST Science Collaborations <https://www.lsstcorporation.org/science-collaborations>`_
|   -- consider participating in the Science Collaborations' `DP0 New Friends program <https://community.lsst.org/t/invitation-for-dp0-delegates-to-participate-in-the-lsst-science-collaborations-new-friends-program/5700>`_
|
| - participate in the :ref:`Delegate-Homepage-Forum` DP0-related categories
|   -- ask questions about using the RSP or the DP0 data set
|   -- respond to delegates requests for assistance when possible
|   -- "show and tell" your DP0-related work in new topics
|
| - participate in the :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`
|   -- ask questions, join the breakout discussions
|   -- volunteer to facilitate a breakout discussion during an assembly
|   -- present the results of your DP0 work in one of the :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`
|
| - lead or participate in one or more :ref:`Delegate-Homepage-Working-Groups`
|
| - contribute tutorials to the `delegates' shared repository <https://github.com/rubin-dp0/delegate-contributions-dp01>`_
|   -- create a tutorial Jupyter Notebook that uses the DC2 data set
|   -- tutorials that use the Portal, TAP, or command-line are also welcome
|
| - share your DP0-related work outside of DP0
|   -- give a seminar about Rubin Observatory and DP0 at your home institution
|   -- give a tutorial about your RSP/DP0 experience in your Science Collaboration
|   -- publish a paper on your DP0-related work


.. _Delegate-Homepage-Working-Groups:

DP0 Working Groups
==================

"DP0 Working Groups" (DP0 WGs) are any collection of DP0 delegates who want to work together on similar DP0-related science or analysis tools.
DP0 WGs are meant to be fairly informal; there are no pre-set DP0 WGs topics, and anyone can propose and coordinate a DP0 WG.
The Rubin Observatory Community Engagement Team (CET) is supporting DP0 WGs by providing Zoom breakout rooms for co-working sessions and a shared repository in the ``rubin-dp0`` GitHub Organization, as described below.
To get your DP0 WG on the list below, or request any other kind of DP0 WG support, please contact Melissa Graham.

**When would DP0 WGs meet?**
Breakout rooms during the second hour of the :ref:`Delegate-Homepage-DP0-Delegate-Assemblies`, or anytime during :ref:`DP0-Delegate-Programming-StackClub` sessions, will be created for any and all who request one.
DP0 WGs could also meet any other time they want to, for the convenience of their members.

**How would DP0 WGs collaborate?**
One way to facilitate collaborative work is to use the `delegates' shared repository <https://github.com/rubin-dp0/delegate-contributions-dp01>`_ in the ``rubin-dp0`` GitHub Organization.
As described in that repository's README file, simply create a new directory in the repository with an appropriate name (e.g., for a Transients Hosts Galaxies DP0 Working Group, could use "wg-transients-host-galaxies").
To facilitate collaboration, it is recommended to keep a README file updated with descriptions of the directory's contents.

**Can I start a DP0 WG by myself?**
Yes! In time, other delegates might join your efforts, and remember that more delegates will be joining for DP0.2 next year.

**How can I advertise a DP0 WG?**
Make a new topic in the Community Forum's Data Preview 0 category titled, e.g., "Invitation to Join the Transient Host Galaxies DP0 Working Group".
If applicable, describe some of the groups potential activities, link to the relevant folder in the shared GitHub repository, and/or say when and where the tag-ups will be.

**Current working groups and their contact info:**

.. list-table:: Active DP0 Working Groups.
   :header-rows: 1

   * - Working Group
     - Contact
   * - `Supernovae <https://community.lsst.org/t/dp0-1-supernova-science-join-the-fun/5869>`_
     - Fabio Ragosta
   * - `Large Scale Structure <https://community.lsst.org/t/invitation-to-join-dp0-lss-working-group/5694>`_
     - Bernardita Ried Guachalla


.. _Delegate-Homepage-Getting-Support:

Getting support
===============

Several venues are provided to support DP0 delegates, as described below.
There is no wrong place to post questions or requests for assistance!
Hearing about issues and receiving feedback from delegates is a key component of DP0.

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
