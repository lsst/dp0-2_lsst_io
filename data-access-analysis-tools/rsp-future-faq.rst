.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-RSP-Future-FAQ:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the link check process.


############################
RSP Future Functionality FAQ
############################

This page contains answers to frequently asked questions (FAQ) about the future full functionality of the Rubin Science Platform (RSP).



Will batch resources be available?
----------------------------------

Yes.

As described in Section 4.3 of `LSE-319 <https://ls.st/lse-319>`_,
the future RSP will provide a shared computing cluster for users to perform analysis through its Portal, Notebook, and Web API Aspects.
The cluster will be managed by a workload management system based on predetermined policies to allocate resources to individual users or groups.
RSP users will have an initial allocation of batch CPU time, with the possibility of applying for additional quota through a Resource Allocation Committee.
The size of the batch computing resource is determined by the requirement to provide 10% of the total LSST computing and storage resources to users.
Users will be able to launch jobs primarily through the APIs exposed in Notebook and Web API Aspects, and the Portal may potentially use the batch computing cluster too.

References:
 * `LSE-319 <https://ls.st/lse-319>`_: Science Platform Vision Document

See also:
 * `DMTN-202 <https://dmtn-202.lsst.io/>`_: Use cases and science requirements on a user batch facility
 * `DMTN-223 <https://dmtn-223.lsst.io/>`_: User batch - possibilities and plans



Will users be able to install custom software?
----------------------------------------------

Yes.

In fact, in the current DP0 era of the RSP, users are already able to install custom software into their own homespace.
In addition, during the operations-era RSP there will be a process for users to request certain popular packages to be added to the 
common environment for use by all.

References:
 * `How do I install packages in my user environment <https://dp0-2.lsst.io/data-access-analysis-tools/nb-intro.html#how-do-i-install-packages-in-my-user-environment>`_



Will GPUs be available in addition to CPUs?
-------------------------------------------

No plan at this time.

As of 2023, there are no plans to include GPUs as part of the resources made available on-project (including "bring-your-own" resources).
At this time, although there are early discussions about providing a mechanism for users to "bring their own" Google resources to the RSP,
including GPU virtual machines, users interested in GPUs should contact the Independect Data Access Centers program
(see, e.g., `Contributed  Computing Resources <https://www.lsst.org/scientists/in-kind-program/cec>`_).

Definitions:
 * GPU: graphics processing unit
 * CPU: central processing unit



Will users be able to download data?
------------------------------------

Yes, for limited subsets of the data.

However, it will be impossible (and impractical) to download the full amount of data that the LSST will produce.
The RSP, in particular its Notebook Aspect, are designed to provide the users with resources at the LSST Data Access Centers 
such that computation and analyses can be performed "next to the data".



Will users be able to work offline?
-----------------------------------

No.

The full functionality of the RSP Aspects will require an online connection in order to access the LSST data and perform analyses on them.



Will use of IDEs be enabled?
----------------------------

IDEs such as VSCode support connections to a JupyterLab server.
However, this currently doesn't work with the Notebook Aspect of the Rubin Science Platform.
Unfortunately, it's challenging to make this work in our environment at the moment, and this feature is not currenyly a priority in the current RSP developement.

Definitions:
 * IDE: integrated development environment (e.g., VSCode, DataSpell)



OTHER
-----

**Q: Will it be possible to prove that algorithms can scale using the DP0-era RSP?**

**A**: No access to user batch or parallelization are available in DP0.
Resources provided as part of DP0.2 are limited and meaningful scalability testing of algorithms is not practical.

Addition references: 
* `FAQ: Technical Aspects of Rubin Science Platform Accounts for DP0 <https://community.lsst.org/t/faq-technical-aspects-of-rubin-science-platform-accounts-for-dp0/4791>`_

To ask additional questions, please use the "Support -- Rubin Science Platform" category in the Rubin Observatory `Community Forum <https://community.lsst.org/c/support/lsp/39>`_


**Q: What are the main technical differences between the DP0-era RSP and the operations-era RSP as described in the RSP Vision Document?**

**A**: A description of the operations-era RSP for future users is provided in the `RSP Vision Document <https://docushare.lsst.org/docushare/dsweb/Get/LSE-319>`_.
The DP0-era RSP will have limited features in many respects, as it is still under active development.
Some of the more notable differences of the DP0-era RSP are:

* Authentication will be performed using Github as the identity provider.
  DP0 delegates will have to create a GitHub account if they do not already have one.
  During operations, authentication will be done with, e.g., US university (InCommon) identity.

* Some major usability features will not be available, such as support for user database tables; support for parallelized or batch computation; the ability to sync files between RSP accounts and personal devices; and the ability to manage the sharing of data within private groups.

* For the Notebook aspect, only python notebooks and the terminal interface are supported, and RSP users will not be able to access their Portal queries from the Notebook aspect for DP0.2.

* For the API aspect, only the Table Access Protocol (TAP) will be available for DP0 (i.e., catalog queries).

* For the Portal Aspect, only catalog queries will be available. 
  Note that the Portal Aspect has not been under active development recently and it is expected to evolve significantly before the first LSST annual data release (DR1).

* A number of safeguards for avoiding uptime or temporary data loss will not be present – the resources are still in “trusted user” mode.

* DP0 delegates will be provided with guidelines that they must follow for safe usage of the RSP during DP0.

* Performance during DP0 may not reflect the performance of the final system, and the resources made available to DP0 delegates may not reflect the final user quotas of the operations-era RSP.

