# FIREWALL

### [Study link](https://www.cloudflare.com/pt-br/learning/security/what-is-a-firewall/)

## What is Firewall?

A firewall is a security system that monitors and controls network traffic based on a set of security rules. 
Firewalls often sit between a trusted network and an untrusted network; Often, the unreliable network is the Internet. 
For example, office networks often use a firewall to protect their network from online threats.
Firewalls decide whether to allow inbound and outbound traffic to pass through. They can be integrated with hardware, 
software, or a combination of both. In fact, the term "firewall" is borrowed from a practice of building walls between 
buildings or in the middle of them and designed to contain a fire. Similarly, network firewalls act to contain online threats.

## Why use a firewall?

The main justification for using a firewall is security. Firewalls can intercept incoming malicious traffic before it 
reaches the network, as well as prevent sensitive information from leaving the network. Firewalls can also be used for 
content filtering. For example, a school can set up a firewall to prevent users on its network from accessing 
adult content. Similarly, in some countries, the government uses a firewall that can prevent people within that country 
from accessing certain parts of the internet. This article will cover firewalls configured for security 
purposes and their various types.

## What are the different types of firewall?

### Proxy-based firewalls:
These are proxies* that sit between clients and servers. Clients connect to the firewall, and the firewall inspects 
the outgoing packets. It will then create a connection to the desired recipient (the web server). Similarly, when the 
web server attempts to send a response to the client, the firewall will intercept that request, inspect the packets, 
and then send that response over a separate connection between the firewall and the client. A proxy-based firewall 
effectively prevents a direct connection between the client and the server. A proxy-based firewall is a type of 
bar security. This security guard intercepts guests before they enter the bar to ensure that they are not underage, 
are not armed, or do not pose a threat to the bar and its customers. The security guard also stops customers at the 
exit to ensure they have a safe way to get home and are not planning to drink and drive. The downside of having a 
security guard at the bar is that when too many people are trying to get in or out of the bar simultaneously, 
there will be a long queue and several people will have to wait. The same is true with the firewall: a major 
disadvantage of a proxy-based firewall is that it can cause latency, especially at times of heavy traffic.
*A proxy is a computer that acts as a gateway between a local network and a larger network, such as the internet.

### Stateful firewalls:
In computer science, a "stateful" application is an application that saves data from previous events and interactions. 
A stateful firewall saves information about open connections and uses that information to analyze incoming and outgoing 
traffic, rather than inspecting each packet. Because they don't inspect all packets, stateful firewalls are faster than 
proxy-based firewalls. Stateful firewalls rely on a lot of context in decision-making. For example, if the firewall 
logs outgoing packets on a connection requesting a certain type of response, it will only allow packets to enter that 
connection if they provide the type of response requested.
Stateful firewalls can also protect ports*, keeping them all closed unless incoming packets request access to a specific port. 
This can mitigate an attack known as port scanning.
A known vulnerability associated with stateful firewalls is that they can be manipulated and trick a client into 
requesting a certain type of information. Once the client requests this response, the attacker can then send malicious 
packets that match these criteria through the firewall. For example, unsecured websites can use JavaScript code to create 
these types of forged requests from a web browser.
*A network port is a place where information is sent; it is not a physical place, but rather the endpoint of a communication.

### Next-generation firewalls (NGFW):
NGFWs are firewalls that have the capabilities of traditional firewalls, but also employ a number of additional 
capabilities to address threats in other layers of the OSI model. Some features specific to NGFW include:
- Deep Packet Inspection (DPI) - NGFWs perform much deeper packet inspection than traditional firewalls. This deep inspection can look for things like packet payloads and which application is being accessed by the packets. This allows the firewall to apply more granular filtering rules.
- Application awareness - Enabling this feature makes the firewall aware of what applications are running and what ports those applications are using. This can protect against certain types of malware that aim to terminate a running process and then take control of your port.
- Identity awareness - This feature allows a firewall to apply identity-based rules, such as which computer is being used, which user is logged on, etc.
Sandboxing - Firewalls can isolate pieces of code associated with incoming packets and run them in a "sandbox" environment to ensure they are not behaving maliciously. The results of this sandbox test can then be used as a criterion when deciding whether or not packets should enter the network.

### Web Application Firewalls (WAF)
While traditional firewalls help protect private networks from malicious web applications, WAFs help protect 
web applications from malicious users. A WAF helps secure web applications by filtering and monitoring HTTP traffic 
between a web application and the internet. They typically protect web applications from attacks such as cross-site forgery, 
cross-site-scripting (XSS), file inclusion, and SQL injection, among others.
When deploying a WAF in front of a web application, a shield is placed between the web application and the internet. 
While a proxy firewall protects the identity of the client machine with the use of an intermediary, WAF is a type of 
reverse proxy that protects the server from exposure since its clients pass through the WAF before reaching the server.
A WAF operates through a set of rules often referred to as policies. These policies aim to protect against application 
vulnerabilities by filtering malicious traffic. The value of a WAF stems in part from the speed and ease with which 
policy modification can be implemented, allowing for a faster response to diverse attack vectors; During a DDoS attack, 
rate limiting can be implemented quickly by modifying WAF policies. Commercial WAF products like Cloudflare's Web Application Firewall 
protect millions of web applications from attacks every day.

### Firewall-as-a-Service (FWaaS):
Firewall-as-a-Service (FWaaS) is a newer model for offering firewall capabilities from the cloud. This service can also 
be called a "cloud firewall". FWaaS forms a virtual barrier around cloud platforms, infrastructure, and applications, 
in the same way that traditional firewalls form a barrier around an organization's internal network. FWaaS is typically 
better suited for protecting both cloud and multicloud assets than traditional firewalls.

## What is a "network firewall"?
A "network firewall" is any firewall that defends a network. By definition, almost all security firewalls are network 
firewalls, although firewalls can also protect individual machines.
While firewalls are an important component of network security, this area also has many other aspects, including access 
control, user authentication, and DDoS mitigation.
