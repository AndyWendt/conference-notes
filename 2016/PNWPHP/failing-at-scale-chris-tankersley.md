# Failing at Scale -- Tankersley

## Problems with distributed applications

- Configurations must be consistent
- Make sure your code gets updated everywhere
- Actually finding errors

You can't rely on physical log files with Docker.  Need to allow remote syslog connections

Look into installing a logging SaaS since it is easier to get set up.

Look into the ELK stack for logging.  ElasticSearch,  LogStash, Kibana  

Don't trust humans--automate.

Automate the build process.  

Track everything: just put it in a bash script then work towards something elegant.  


Automate code pushes.  Checklists don't save you since they can be circumvented.   Automation is the way to go.  



