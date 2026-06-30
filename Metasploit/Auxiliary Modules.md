Auxiliary modules are used to scanning, discovering and fuzzing. As we can use Auxiliary modules to perform both TCP and UDP port scanning as well as enumerating information from services like FTP,SSH,HTTP etc.

Auxiliary Modules is used during the information gathering phase of a penetration test as well as the post exploitation phase.

service postgresql start && msfconsole
workspace -a port scanning
search portscan
