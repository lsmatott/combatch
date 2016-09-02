=============================================================================
combatch - COMSOL Server Batch Automation
=============================================================================

combatch is an automation script for running COMSOL server applications on 
distributed computing clusters. It is currently configured for users of 
`SLURM <http://slurm.schedmd.com/>`_. 

-------------
INSTALL
-------------

- To install combatch download the `latest release <https://github.com/lsmatott/combatch/releases>`_::

  $ tar xvf combatch-0.x.x.tar.gz
  $ cd combatch-0.x.x

- Copy the sample config file and edit to taste::

  $ cp conf/combatch.sample conf/combatch
  $ vim conf/combatch

----------------------------------
Summary of combatch commands
----------------------------------

- *combatch*

  The primary application of this repository. It does the following:

(1) request compute nodes on the cluster (based on a set of command line arguments that specify number of nodes, memory, etc.)

(2) wait for compute nodes to be allocated by the SLURM scheduler

(3) login to the head compute node

(4) launch comsol server on the head compute node

(5) launch firefox web browser on the head compute node and connect to localhost:port to initiate the CSL app session

(6) within firefox session the user uploads and/or selects desired app --- this should include an interface for setting up cluster computing if the computation is to be spread across more than one node

(7) when user hits the COMSOL compute button (i.e. "=" icon) the cluster compute job is launched on the assigned compute nodes. An example .mph file (examples/simpleEnvReader.mph) illustrates how a bit of java code can populate the COMSOL cluster compute settings to match them with what is assigned by the scheduler (e.g. node list and paths to .mph files)

(8) the combatch script also writes a "reconnect" script that can be used to reattach to the job. This way, once a compute job starts running the user can close the firefox browser session and reconnect later when the job is completed.


- *comsniff*

  A bash one-liner that tries to determine the name of the .mph file that a user has selected in a browser session.

----------
License
----------

combatch is released under the GNU General Public License ("GPL") Version 3.0. See the LICENSE file.
