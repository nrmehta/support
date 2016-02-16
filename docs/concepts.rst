Basic Concepts
==============

Here's a quick overview of the basic elements of the Falkonry Service and concepts that
are referenced elsewhere in the documentation.

.. image:: images/operations.png

Things
------

Things are what they sound like - anything (e.g. an appliance, a device, a vehicle, a 
machine) that produce a stream of data through its operation.

Operational View
----------------

In the condition prediction context, there is an Operational View where a locus of 
information about the set of Things is managed.  It is from this view that the state of 
the Things is monitored and in some cases controlled.  

Falkonry Pipeline
-----------------

A Falkonry Condition Pipeline is what a user interacts with when using the Falkonry 
Service for condition prediction. The Pipeline augments the Operational View, by 
providing a stream of condition predictions in exchange for a stream of source signal data
from Things.

.. image:: images/pipeline.png
   :height: 223
   :width: 240
   
Source Signals
--------------

The source signals provide to the Pipeline a stream of values over time, that can be 
indexed by the Thing identity.  At a given time, then, the Pipeline receives a set of 
signals (e.g. representing a set of sensor readings), and it can receive sets of signals 
for many individual Things.  The signals can be of three types:  numerical, categorical, 
and vector (a sequence of numerical values associated with one time point).

Condition Predictions
---------------------

Condition predictions are what the Pipeline produces.  Like the source signals, each 
condition prediction output (called an Assessment)  is a stream of values over time that 
is indexed by the Thing identity.  The value type of an Assessment is categorial, where 
each potential value is a ‘Condition’ associated with that Thing.  There can be multiple 
Assessments associated with one type of Thing, e.g. a Health Assessment and an Operating 
Mode Assessment.

Verified Condition Examples
---------------------------

A Falkonry Pipeline learns by example, i.e. as verified condition states for Things are 
supplied, the Pipeline’s machine learning capabilities improve its condition predictions.  
These verified condition examples can come from periodic inspection reports, incident 
reports, or other forms of data collection.  The Pipeline can use verified conditions from 
individual Things to improve predictions across the entire set.