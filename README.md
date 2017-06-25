Bauer et al. [1] showed that the Tor network is very vulnerable to the traffic correlation attack in the circuit creation phase. Before sending any data on the circuit, the adversary controlling the entry and the exit relays can correlate the traffic pattern on the relay cells and link the client to her destination. 

In this project we propose some approaches to hinder this attack. We borrow the techniques from the Mix networks and use them in the circuit creations in the Tor network.

In our defense, we have some parameters that should be set in torrc files to enable the defense mechanism and change its configuration.

DEFENSE parameter determines which defense mechanism you want to use.

# DEFENSE = 1:
When the relay receives the EXTEND cell, it extends the circuit (i.e. sends the CREATE cell) to the next hop after some random time between 0 and TIMEOUT_ISEC. TIMEOUT_ISEC should be set in the torrc file in milliseconds.


# DEFENSE = 2:
The relay buffers the received EXTEND cells. When it has enough number of EXTEND cells, it extends them all at once. EXTEND_CAP parameter defines the number of buffered EXTEND cell before extending. If the relay does not receive that number of EXTEND cell within TIMEOUT_ISEC milliseconds, it flushes the buffer and extends all of EXTEND cells in its buffer.

EXTEND_CAP and TIMEOUT_ISEC (in milliseconds) should be set in torrc file.

 
# DEFENSE = 3:
This case is the same as case DEFENSE = 2 but the only difference is that the relay considers separate buffers for each relay, it buffers all the EXTEND cells to a specific relay in separate buffer, and flushes them when there are EXTEND_CAP EXTEND cells for that relay within TIMEOUT_ISEC milliseconds.

# References
1-	BAUER, K., MCCOY, D., GRUNWALD, D., KOHNO, T., AND SICKER, D. Low-Resource Routing Attacks against Tor. In Proc. of Workshop on Privacy in the Electronic Society (2007). 

