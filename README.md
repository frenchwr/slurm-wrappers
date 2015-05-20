# SLURM Wrappers 

These are Python wrappers for parsing SLURM commands. Specifically, **qSummary** lists active and pending cores/jobs organized by group and user, while **showLimits** lists account limits for CPU, memory, and CPU time usage.

Both scripts work for Python 2.7 and above. You may need to change the shebang line from:

	#!/usr/local/bin/python

to

	#!/usr/bin/env python

if you do not have a Python 2.7+ interpreter living in /usr/local/bin.

qSummary
--------

Usage:

	[jill@vmps15 ~]$ qSummary
	GROUP      USER        ACTIVE_JOBS  ACTIVE_CORES  PENDING_JOBS  PENDING_CORES
	-----------------------------------------------------------------------------
	science                    18            34             5             7
			   jack             5             5             4             4
			   jill            13            29             1             3
	-----------------------------------------------------------------------------
	economics                  88           200           100           100
			   emily           88           200           100           100
	-----------------------------------------------------------------------------
	Totals:                   106           234           105           107

Notes:

- Before 14.11.6 there was a SLURM bug in reporting pending job arrays where the user limited
the number of concurrently running job array elements with the % symbol. This may cause
inaccurate reporting for pending job arrays running SLURM prior to version 14.11.6.

showLimits
----------

Usage:

	[jill@vmps15 ~]$ showLimits -g science_account
	ACCOUNT         GROUP       FAIRSHARE   MAXCPUS   MAXMEM(GB)  MAXCPUTIME(HRS)
	-----------------------------------------------------------------------------
	science_account                12        3600       2400           23040
				   biology          1        2400       1800               -
				   chemistry        1         800        600               -
				   physics          1         600        600            8640
				   science          1           -       2200           20000
	-----------------------------------------------------------------------------

Notes:

- On Vanderbilt University's ACCRE cluster we only enforce limits on CPU cores, 
memory, and CPU time. If your cluster imposes additional limits this script will
need to be modified/extended.