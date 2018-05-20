Real time view must support random write? what's the difference between support random write or not?

* The speed layer data is at most a few hours old and is vastly smaller than the master dataset
* The speed layer producing views by running a function over all of the recent data



Two facets of the speed layer:

* storing the realtime views
* Processing the incoming data stream and update those views



The incremental algorithms in speed layer:



