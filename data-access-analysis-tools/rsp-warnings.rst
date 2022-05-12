.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name"  -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-RSP-Warnings:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the link check process.

#####################
RSP Risks and Caveats
#####################

.. This section should provide a brief, top-level description of the page.

We are excited to be offering limited early access to a preview of RSP capabilities. DP0 is a *shared-risk activity* as it predates not only the end of construction development, but even the telescope's first light.

.. Important::
    During DP0, everyone is responsible for their own safe usage of the shared-risk,
    in-development version of the RSP and other capabilities of the Rubin Interim Data Facility (IDF).
    Some controls to prevent anti-social or damaging actions do not exist yet; many important features are not available yet.
    Read on to understand more about both of these.

.. Important::
    **Do not share your passwords or RSP account access with others.**

When in doubt whether something is okay or to ask information about planned future functionality,
post questions in `the "Support -- Data Preview 0" subcategory <https://community.lsst.org/c/support/dp0/49>`__ in the Community Forum.

If you believe you have found a bug or wish to request a feature, please `open a GitHub Issue <https://github.com/rubin-dp0/Support/issues/new/choose>`_ instead.

User data: No parachutes!
-------------------------

When you access the RSP Notebook aspect, you have a home space you can use to store your notebooks, scripts, extra python modules and small files.
Other users cannot see the contents of your home space, but you have no expectation of privacy from observatory staff monitoring the systems.
If we experience an incident, we will attempt to restore the contents of your homespace.
The contents of your homespace will not be deleted without attempting to notify you.

Data in ``/scratch`` is not backed up.

Data in ``/projects`` is available for use in the situation where you wish to share files with other RSP users.
For this data preview, any files in you put in ``/projects`` are readable and writeable by all users.
Take care you do not delete other people's files.

For this data preview there are no file quotas applied, however usage will be monitored and users may be asked to reduce their footprint, either in their home space or shared data spaces.

For this data preview, there are no write/delete restrictions on the shared user data Butler repository (butler-us-central1-dp01).
That means you could delete your data and other user's data.
User data stored in our Butler repositories is not backed up, and may not be retained past the Data Preview 0.2 period.
Be very careful when using the Butler prune collection feature and in particular don't use wildcards with that command.

You can reduce the risk of accidents by following the convention documented in `DMTN-167 <https://dmtn-167.lsst.io/>`__ and only write to your own ``u/<user>/*`` collections.

You should only access our Butler repositories using standard Butler APIs provided in the Rubin Stack.
This is both to prevent accidents but also to fulfill your role in helping us evaluate our software.

RSP/IDF missing features
------------------------

Many more features are on our roadmap for the RSP and its related services (Qserv, Butler, etc.) and we have requirements to deliver them by the start of the survey.
Some major ones to look forward in the future are:

- Notebooks: We are planning on providing a filespace that you can access from your personal device (e.g., laptop) so you can use your favorite editor/IDE to write code in your local environment and save it in a way that makes it visible in your RSP notebook environment
- Batch: Opportunities for parallelized/batch/non-interactive computation are not currently available
- Qserv: User tables are not yet available
- Qserv: TAP/ADQL Queries using some keywords (AREA, BOX, COORDSYS, COORD1, COORD2 and INTERSECTS) are not yet supported
- Portal: Many improvements are planned, including the ability to start a query in the portal and access it from your notebook
- Authentication and Authorization: You will be able to create and manage groups to allow you to share data with specific RSP users
- API: Virtual Observatory image services are not yet available
- API: VOSpace service is not yet available
- ConsolidatedDB: Access to observatory metadata is not yet available
- Bulk Download Service: Not offered

Warnings and admonishments
---------------------------

Our `Acceptable Use Policy <https://data-dev.lsst.cloud/terms>`_ applies: We’re giving you access to Rubin Observatory systems so you can do science with the data we provide or otherwise further the mission of the observatory.
You can lose your access if you misuse our resources, interfere with other users, or otherwise do anything that would bring the observatory into disrepute.

One of the main goals of the Data Preview program is to allow us to assess user interactions with our services.
Bypassing use of our services (such as attempting to bulk download data or trying to defeat the Butler APIs) violate the spirit of the exercise.
