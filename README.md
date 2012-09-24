indexd - Index-Based Search Daemon
==================================

The indexd (Index Daemon) is a background process which receives new fingerprints from featureX over sockets and performs a quick search in all previous fingerprints.

Therefore the fingerprints are stored and maintained in an index-like structure with the feature classes in the dictionary and tuples of call identifier and position of occurrence in the postings lists.
These postings list are also called inverted files or inverted list and the search method basically intersects these list with some fault-tolerance mechanisms.

###Usage

Since indexd is a background daemon an easy way to start it is to run on the command line the following.
 
Example:
	./indexd
