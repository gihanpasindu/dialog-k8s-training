### Loadbalancing
### NOTE: done in Destination Rule
ROUND_ROBIN -  evenly distributes the load,in order
RANDOM -evenly distributes the load across the endpoints in the load-balancing pool but without any order.
LEAST_CONN - picks two random hosts from the load

### Timeouts 
### NOTE: Done in Virtual Service

### Retries
### NOTE: Done in Virtual Service