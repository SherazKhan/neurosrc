# chantimeremoval

This submodule contains a function (chanTimeReject.m) and associated function dependencies
that can be applied in a script (example: chanTimeRejectDemo.m) in order to mark bad
channels and time periods in multi-channel electrophysiology recordings. Specifically, 
this function was written to detect bad channels in 96-channel Neuroport recordings. Below 
is an outline of how the algorithm rejects times and channels.

	1. Each channel’s voltage time series is normalized by mapping voltage to zscore.
	2. For each channel, the time points at which the voltage exceeds some user-defined absolute z-score (Zhigh, default = 6), are marked as bad time points for that channel.
	3. For each of the bad time points identified, the time point is marked as a bad time point in general if a certain number of other channels (nChanForBadTime, default = 10) exceed a lower z-score threshold (Zlow, default = 4) within a certain time period (dtForBadTime, default = 1 second).
	4. These general bad time points were then extended to general bad time periods by marking any time point within a user-defined period (dtReject, default = 1 second) as a bad time point.
	5. Time periods bad for individual channels are identified. These are defined similar to the general bad time periods except using the time points for which the nChanForBadTime criteria was not met.
	6. Bad channels are identified as having a large number of non-general time periods (nBadtoRejectChan, default = 10).
