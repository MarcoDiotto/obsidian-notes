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
* **URL** (Uniform Resource Locator): identifies a resource by specifying its *location*
* **URN** (Uniform Resource Name): identifies a resource with an *unique name* $\to$ Not used!
 
  HTTP consists of  a sequence of *transactions*, composed by a *request* (client $\to$ server), followed by a *response* (server $\to$ client), formatted in an *HTTP message*
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
# Lesson 3
___
* The *scheme* specifies the protocol to use to receive the resource from the server.
* *User* and *Password* can sometimes be requested to authenticated with the server. If not specified, the default user name is **anonymous**.
* The *server address* can be a **hostname** (resolved via DNS) or an **IP address**.
* The server has a *port* on which it is listening for a connection. The port can be omitted and in this case the default value will (**Example**: HTTP default port is 80).
* The *path* specifies the local location in the server (as a file in the filesystem of the server $\to$ nowadays resources are generated on the fly). The path can be divided into multiple segments separated by /.
* *Params* allows to specify a list of "key-value" pairs. They refer to the **path**
* *Query* is again a "key-value" pair used to restrict the resources of the server. They refer to the **resources**. `&` can be used to separate "key-value" pairs.
* *frag* is used to restrict the area to a specific fragment of the page.
## Absolute and Relative URLs
* `<a href-=".hammer.html"` is a **relative** URL because it doesn't contain any *schema* nor *hostname*. We need a **base URL** to which concatenate the relative URL. Base URLs can be obtained in 2 ways:
  1) By specifying it using the tag `<base>` in the document header
  2) Using the absolute URL.
* URLs can only contain symbols from the standard **ASCII**(non-ASCII characters are supported by **IRI**)
* **Character escaping** in URLs is performed in the following way:`%`+ 2 digits that identifie the character
## HTTP Connection
HTTP works at an **application** level, so we need other protocols:
* **TCP** provides a *bidirectional data stream*:
	1) **Connection-oriented**
	2) **Reliable**
	3) **Ordered** $\to$ data arrives in the same order as they where generated
	4) **Flow control** is used to avoid congestion
	5) A **TCP connection** is uniquely identified by 4 values: `<source ip> <source port> <destination ip> <destination port>`. Multiple connections with the same IP or port are allowed.
## HTTP messages
After the **TCP connection**, the HTTP protocol expects the exchange of a list of at least **2 messages**:
* a **request**
* a **response**

A  **general message** is divided in 3 parts:
* a **start line**: string describing the message followed by a newline
* a **header**: multiple text lines to define options and properties of the message. The header section end with an empty newline
* a **body**: generic data

A **request** uses those parts as following:
* **start line**: `<method> <request-URL> <version>`
* **header** : `<name1> : <value1>  <name2> : <value2>`
* **body**: *binary*, text data or an empty line

A **response** on the other hand uses them as following:
* **start line**:
* **header**:
* **body**: