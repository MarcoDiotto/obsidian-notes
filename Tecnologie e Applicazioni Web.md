# Lesson 1
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
* using the HTTP protocol, the browser asks for the resource `home.html`
* The resource is downloaded by the TCP connection.
* The resource has an associated representation($\color{green} mime-type$).
# Lesson 2
___
**HTTP**: 
* A *protocol* is a set of rules. 
* It is called *hypertext* because it was once used to transmit only texts 
* It is used to *transfer* data
* It's a *request-response* protocol with a *client-server* model 
  ```mermaid
  flowchart LR
  A[[CLIENT]] --HTPP REQUEST --> B[[SERVER]]
  B -- HTTP RESPONSE --> A
  B -- HOSTS --> C(Resources)
  D(Static) --> C
  E(Generated on-demands) --> C
  ```
  Every *resource* has an associated type, called **MIME**, which is simply a *string* formatted as: `<type>/<subtype>`. 
  **Examples**:
  * the mime type of an HTML document is `text/plain`
  * the mime type of a JPEG image is `image/jpeg`
  * the mime type of JSON strings in `application/json`
Every resource has a name, called **URI** (Uniform Resource Identifier):
* **URL** (Uniform Resource Locator): identifies a resource by specifiyng its *location*
* **URN** (Uniform Resource Name): identifies a resource with an *unique name* $\to$ Not used!
 
  HTTP consists of  a sequence of *trnasactions*, composed by a *request* (client $\to$ server), followed by a *response* (server $\to$ client), formatted in an *HTTP message*
  The commands for asking a server to do something are called *HTTP  methods*, the six most common ones are:
  * GET
  * PUT
  * DELETE
  * POST
  * HEAD
  * PATCH
Every *server response* must contain a *status code*, the most popular ones are:
* 200 (Success)
* 302 (Redirect required)
* 404 (The resource does not exists)