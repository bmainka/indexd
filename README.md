indexd - Index-Based Search Daemon
==================================

The indexd (Index Daemon) is a background process which receives new fingerprints from featureX over sockets and performs a quick search in all previous fingerprints.

Therefore the fingerprints are stored and maintained in an index-like structure with the feature classes in the dictionary and tuples of call identifier and position of occurrence in the postings lists.
These postings list are also called inverted files or inverted list and the search method basically intersects these list with some fault-tolerance mechanisms.

###Usage

Since indexd is a background daemon an easy way to start it is to run on the command line the following:

	./indexd
	
You can pass the configuration file as argument. Otherwise indexd expects the configuration file to be _/etc/viat/indexd.conf_.

	./indexd indexd.conf

###Configuration

Here is an example for a configuration file with all configurable parameters:

	######################################################################
	########## Configuration file for index-based search daemon ##########
	######################################################################
	
	# Specify directory to run daemon and for logging output
	LOG_DIR                         = /var/log/viat/
	PID_DIR                         = /var/run/viat/
	
	# Port to receive new fingerprints
	SOCKET_PORT                     = 3000
	
	# Connection string for database 
	# (connection string has to be between quotes e.g. "dbname=viat"!)
	CONNINFO                        = "host=139.6.237.43 dbname=viat user=viat"
	
	# Fuzzy search (no: 0, yes: other)
	FUZZY                           = 0
	# Number of matches
	N                               = 20
	# Maximal time shift in samples (>= 0)
	MAX_OFFSET                      = 127
	
	# Maximal number of elements per query (position, feature) (query, memory allocation)
	NUMELEMOFEACHQUERY              = 500
	
	# Logging level 
	# 1: FATAL
	# 2: ERROR
	# 3: WARNING
	# 4: INFO
	# 5: DEBUG (search)
	# 6: TRACE (search algorithm output)
	LOG_LEVEL                       = 4

###Logging

The logging output is in the configured directory, e.g. _/var/log/viat/indexd.log_. You can follow the output by using tail.

	tail -f /var/log/viat/indexd.log

###Process Identifier (PID)

To quit the daemon is very easy using the pid. For example type:

	kill `cat /var/run/viat/indexd.pid`

and press enter.