Private Deployment
==================

A private deployment of Falkonry can be made into an Infrastructure-as-a-Service provider
such as Microsoft Azure or AWS. It is also possible to provide a private deployment of
Falkonry in your own data center or rack.

System requirements
-------------------

Any deployment of Falkonry should be sized appropriate to the data rate, maximum number
of signals per pipeline, and the number of pipelines. The minimum suggested hardware for
use with Falkonry is the following:

- Hardware 

  - VM and bare metal instances are supported
  - For Falkonry Enterprise

    - Tiny Deployment
      - 1 instance with 4 full cores and 16 GB RAM
      - 100 GB attached free SATA storage
    
    - Medium Deployment
      - 4 instances with 4 full cores and 64 GB RAM each
      - 256 GB attached SATA for root volumes
      - 1 TB SSD for learning buffer volumes
      - 128 GB SSD for internal database volumes

- Software 

  - `Kubernetes v1.1 <http://kubernetes.io/v1.1/gs-custom.html>`_ including 
    `kubectl <http://kubernetes.io/v1.0/docs/user-guide/kubectl/kubectl.html>`_
    The VMs can run any operating systems as long as Kubernetes is fully supported.
  
- Network
 
  - Outbound access to the Internet is required to perform installation.
  - Inbound access for Falkonry DHCS through a jump box

Preparing to Install Falkonry
-----------------------------

Make sure Kubernetes is running and a cluster has been created. Also, ensure that you can
reach the Kubernetes cluster using ``kubectl``. You can confirm this by performing the 
following steps::

  $ kubectl get services
  $ kubectl get rc

Download the Falkonry Installer from `falkonry.com/partners <http://falkonry.com/partners>`_.

Also, before executing the next step, complete the following:
  
- Obtain the following from Falkonry:

  - Software repository credentials for downloading Falkonry Enterprise.
  - Splunk HTTP Event Collector Token for deployment health monitoring.
  - Splunk credentials for application logging.

- Every instance that is part of the Kubernetes cluster will have to login to Falkonry's
  software repository using credentials from the previous step. The command will look like
  the following where the ``-u`` and ``-p`` values will be the credentials provided to you::
  
    docker login -e="." -u="falkonry+installer" \
    -p="9496DSFLGKJ49TS5MGZNW8MK5SDWZDIAKC003ZR8SM71B03UUIVAVOSC66F7S" quay.io
- Decide the configuration for the following properties:

  - Tiny vs. medium size deployment as explained earlier
  - External host name
  - External host protocol such as ``http`` or ``https``

- Create a DNS entry for your selected host name and map it to the IP address for the
  Kubernetes host.
  
- Map externally accessible ports to the Falkonry UI Server port ``30061``. You can use 
  Apache or another Web server for this purpose.

  - If you are using the ``http`` protocol in the previous step, you will need to proxy
    from port ``80`` to port ``30061``. 
  - If you are using the ``https`` protocol in the previous step, you will need to proxy
    from port ``443`` to port ``30061``. 

Executing the Falkonry Installer
--------------------------------

You can run the Falkonry installer from the downloaded `Falkonry-k8-installer.zip` file. To execute the
installer, you will need a shell environment such as `bash` or `tcsh`. Also, make sure
that you run the Falkonry installer from the environment that you can access Kubernetes
from as confirmed in the previous step.

You will run the installer in the following command from the folder where you opened the
Falkonry Installer Zip file::

  $ ./install.sh -c=tiny -h=falkonry.acme.com -p=http -k=kubernetes-token \
  -t=splunk-token -u=splunk-user -s=splunk-password
  
Note that `medium` deployment will require a multi-node Kubernetes cluster and can be 
selected by using the ``-c`` switch above.

The full usage documentation of this installer script is as follows::

  Example : install.sh -c=tiny -h=falkonry.acme.com -p=https -k=kube-secret -t=1234567890 -u=username -s=secret
    -c | --clusterType   : Cluster type - tiny or medium.
    -h | --host          : Falkonry host to be used. Example - falkonry.acme.com.
    -p | --protocol      : Host protocol to be used - http or https.
    -k | --kubeToken     : Kubernetes authentication token.
    -t | --token         : Splunk token to be used. This is provided by Falkonry.
    -u | --username      : Splunk username to be used. This is provided by Falkonry.
    -s | --password      : Splunk password to be used. This is provided by Falkonry.

Post-Installation Steps
-----------------------

If you have prepared correctly for the installation, then once the installation is 
completed, you will be able to open the URL for your host in a regular browser to bring up
Falkonry. For example, if your configured host were ``falkonry.acme.com`` and configured 
host protocol is ``http``, then just type ``http://falkonry.acme.com`` to start using
your private deployment of the Falkonry Service.

Updating Falkonry software
--------------------------

You can run the Falkonry update script from the downloaded `Falkonry-k8-installer.zip` file. To execute the
script, you will need a shell environment such as `bash` or `tcsh`. Also, make sure
that you run the script from the environment that you can access Kubernetes
from as confirmed in the previous step. Using this script, all the configurational changes released by Falkonry
will be patched to your existing installation.

You will run the update script in the following command from the folder where you opened the
Falkonry Installer Zip file::

  $ ./update.sh -c=tiny -h=falkonry.acme.com -p=http -k=kubernetes-token \
  -t=splunk-token -u=splunk-user -s=splunk-password
  
Note that `medium` deployment will require a multi-node Kubernetes cluster and can be 
selected by using the ``-c`` switch above.

The full usage documentation of this update script is as follows::

  Example : update.sh -c=tiny -h=falkonry.acme.com -p=https -k=kube-secret -t=1234567890 -u=username -s=secret
    -c | --clusterType   : Cluster type - tiny or medium.
    -h | --host          : Falkonry host to be used. Example - falkonry.acme.com.
    -p | --protocol      : Host protocol to be used - http or https.
    -k | --kubeToken     : Kubernetes authentication token.
    -t | --token         : Splunk token to be used. This is provided by Falkonry.
    -u | --username      : Splunk username to be used. This is provided by Falkonry.
    -s | --password      : Splunk password to be used. This is provided by Falkonry.

Upgrading Falkonry software
---------------------------

You can run the Falkonry upgrade script from the downloaded `Falkonry-k8-installer.zip` file. To execute the
script, you will need a shell environment such as `bash` or `tcsh`. Also, make sure
that you run the script from the environment that you can access Kubernetes
from as confirmed in the previous step.

You will run the upgrade script in the following command from the folder where you opened the
Falkonry Installer Zip file::

  $ ./upgrade.sh
