#seamless
(Forked from https://bitbucket.org/tebeka/seamless)

**seamless** is a TCP proxy that allow you to deploy new code then switch traffic
to it without downtime.

It does "round robin" between the list of current active backends.

Switching server is done with HTTP interface with the following API:

###### set list of backends:

        /set?backends=host:port,host:port
        
###### add a backend:

        /add?backend=host:port

###### remove a backend:

        /remove?backend=host:port

###### list backends:
        /get
        
    	return host:port,host:port

Process
=======
* Start **seamless** with list of active backends::

        seamless 8080 localhost:4444
    
* Direct all traffic to port 8080 on local machine.
* When you need to add/remove the backend, use the HTTP API on port 6777
  different port, say 4445)

        curl http://localhost:6777/add?backend=localhost:4445
        curl http://localhost:6777/remove?backend=localhost:4444

  Or

        curl http://localhost:6777/set?backends=localhost:4445
    
New traffic will be directed to new backend(s).

Installing
==========

    go get github.com/juliendsv/seamless

Contact
=======
Miki Tebeka <miki.tebeka@gmail.com> 



LICENSE
=======

https://bitbucket.org/tebeka/seamless/src/tip/LICENSE.txt
