___
## Internet

* The internet is the $\color{green}global\  system$ of interconnected computer networks that uses the $\color{green}Internet\ Protocol\ Suite$ (TCP/IP) to link devices worldwide.
* Every device is identified by an $\color{green}address$ and is generally referred to as an $\color{green}host$. Two hosts may communicate even if they have no direct connection.

### Protocols

* A communication protocol is a $\color{green}set\ of\ rules$ for exchanging information over a network.
* Protocols are usually layered in a $\color{green} stack$.
* Specifies how data should be $\color{green} packetized,\ adressed,\ transmitted,\ routed$ and $\color{green}received$.
* $\color{red}Physical\ Layer$: transceiver that drives the signal on the network.
* $\color{red} Data\ Link\ Layer\ (MAC)$: creates the frames that move across the network.
* $\color{red}Network\ Layer$: creates the pakets that move across the network.
* $\color{red}Transport\ Layer\ (TCP/UDP)$: established connection between devices.
* $\color{red}Application\ Layer$: final layer.


## World Wide Web

The world Wide Web is an $\color{green} Information\ System$ in which the items of interests ($\color{green}resources$) are referred to as Uniform Resource Locators($\color{green}URL$)

Resources can be linked by $\color{green}hypertext$ and are accessible over the $\color{green}Internet$. Resources may be accessed by a $\color{green}Web\ Browser$.

### Architectural bases of the WWW

* $\color{red}URLs$ are used to identify resources
* $\color{red}Web\ agents$ communicates using $\color{green}Standardized\ protocols$ that enable interaction through the exchange of messages that adhere to a defined syntax and semantycs.
* $\color{red}Resources$ have a specific $\color{green}representation$ that can be interpreted (and visualized) by $\color{green}web\ browser$. 
		Resource $\neq$ representation. `http://www.../cat.jpg` $\rightarrow$ jpg doesn't mean anything for the web browser.
### Browsing the web

We start with a resource: `http://www.example.org/home.html`

* http is the name of the protocol used to ask for the resource
* `www.example.org` is the destination name (resolved into an IP address by the DNS (Domain Name System))
* using the HTTP protocol, the browser askes for the resource `home.html`
* The resource is downloaded by the TCP connection.
* The resource has an associated representation($\color{green} mime-type$).