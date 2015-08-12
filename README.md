# Getting-started-with-sendwithus
-------------------------------
Getting started with sendwithus 
===============================
-------------------------------

### About sendwithus ###

Sendwithus is an API to send emails to your customers. Your application, product, or service triggers an API call to sendwithus. Your email is then rendered by sendwithus for delivery, and is then delivered to your ESP and your email gets sent. Our API integrates with your email service provider. You simply set up your email template, connect your ESP, and our API takes care of the rest.


### REST API ###

Sendwithus is a Representational State Transfer application program interface (REST API) for SendGrid, Mandrill, and MailGun. REST is resource based versus action based, and a REST-ful API refers to things or resources instead of actions. Representations are how resources get manipulated, and are usually in JSON or XML format, and sendwithus uses JSON. Resources are transferred between client and server as part of the resource state. The REST architectural style describes 6 constraints that are applied to the architecture, which are as follows:

- Uniform Interface: defines the interface between client and server, simplifies and decouples the architecture 
- Stateless: the server does not contain a client state, each request has enough context to process the message
- Cacheable: server responses must be cacheable 
- Client-Server: is a disconnected system, may not have a direct connection to a database
- Layered System: client cannot tell if connected directly to an end or intermediary server (improves scalability) 
- Code on demand: an optional constraint where server can temporarily extend client

### HTTP ###

The Hypertext Transfer Protocol (HTTP) is a protocol for information systems. It is the foundation of data communication for the internet. It is structured text that uses hyperlinks between nodes containing text. Some of the main HTTP request methods used in sendwithus are as follows: 

- PUT: puts a resource at a specific uniform resource identifier (URI). If there is an existing resource, PUT will replace that resource. If the URI does not point to an existing resource, then the server can create the resource with that URI.
- POST: sends data to a URI and then the resource at that URI handles the request, then the server determines what to do with the data.
- GET: requests data from a specific resource. It only retrieves data, and has no other effect.
- HEAD: asks for the same response as a GET request, but without the response body.

### JSON ###

JSON is used by sendwithus as opposed to other technologies such as XML for several reasons. XML is ill-suited to data-interchange, as it carries a lot of baggage, and it does not match the data model of many programming languages. JSON is better suited to data-interchange. JSON is simpler than XML, easier to read and write for humans and machines, and maps better onto the data structures in programming languages. Since JSON's structure is simpler, it is processed more easily. JSON is data-oriented instead of document-oriented, and can be mapped more easily to object-oriented systems. JSON is ultimately more efficient. The following is an example of JSON versus XML formatting:

###### JSON ######
	
	{
    "glossary": {
        "title": "example glossary",
		"GlossDiv": {
            "title": "S",
			"GlossList": {
                "GlossEntry": {
                    "ID": "SGML",
					"SortAs": "SGML",
					"GlossTerm": "Standard Generalized Markup Language",
					"Acronym": "SGML",
					"Abbrev": "ISO 8879:1986",
					"GlossDef": {
                        "para": "A meta-markup language, used to create markup languages.",
						"GlossSeeAlso": ["GML", "XML"]
                    },
					"GlossSee": "markup"
                }
            }
        }
    }

###### XML ######

	<!DOCTYPE glossary PUBLIC "-//OASIS//DTD DocBook V3.1//EN">
 	<glossary><title>example glossary</title>
	  <GlossDiv><title>S</title>
   	<GlossList>
   	 <GlossEntry ID="SGML" SortAs="SGML">
    	 <GlossTerm>Standard Generalized Markup Language</GlossTerm>
    	 <Acronym>SGML</Acronym>
    	 <Abbrev>ISO 8879:1986</Abbrev>
    	 <GlossDef>
     	 <para>A meta-markup language, used to create markup
	languages such as DocBook.</para>
      	<GlossSeeAlso OtherTerm="GML">
    	  <GlossSeeAlso OtherTerm="XML">
   		  </GlossDef>
   	  	<GlossSee OtherTerm="markup">
   	 	</GlossEntry>
  	 	</GlossList>
 	 </GlossDiv>
 	</glossary>

### Authentication ###

Basic access authentication is used by a HTTP user agent to provide a password and user name when making a request. It does not require cookies or a session identifier, and is therefore the most simple method for enforcing access controls to web resources. Instead, it uses static and standard fields in the HTTP header, which bypasses the process of handshaking. An API key is a code passed to identify the calling program, or its developer or user. They are used to track how the API is used. For example, when calling an API that does not access private user data, an API key can be used by authenticating the application for accounting purposes.

To use an API key, the a relevant script example is as follows:

	service = build('books', 'v1', developerKey = "api_key")


### Error Handling ###

Sendwithus' HTTP codes return if there is an error, such as 4XX and 5XX errors. A HTTP 5XX error is when the server failed to fulfill a request. The '5' indicates that the server is aware that is has encountered an error, but cannot perform the request. HTTP 500 is a generic internal server error, and if a user receives one, you know the application is the problem. To debug such an error, take the following steps:

- check the integrity of the web server, the web server plugin, the application server, the application
- verify that the application server is started, then that the application is started
- application must start up without exceptions thrown in SystemOut

As another example, a 404 error indicates  that the client was able to communicate with the server, but the resource that was requested was not found. For debugging, you can usually narrow down the problem to one of two types, based on the symptoms that users report:

- The first error may be a JSP/JSF error. To debug, take the following steps:

	- verify that the web server plug-in is functioning properly and that the URL is specified properly
	- verify that the web server is responding, and that the application is running

- The second most likely error is that the WebGroup/virtual host is not defined. To debug:
	
	- verify that the configuration of the virtual host is correct, and that the URL is specified properly
	- verify that the application is running

### Sending your first email ###

The following is an example of a cURL command which can be used to send an email, taken from the sendwithus website:
	
	curl\
		-X POST\
		-u swu_key_582cc75cc64f6d7ea0db:\
		-d '{
			"template": "swu_email_emWvGb6pH",
			"recipient": {
				"address": "john@example.com"
			},
			"template_data": {
				"first_name": "John Doe",
				"link_url": "https://www.sendwithus.com",
				"items": ["an array item", "another item"]
			}
		}'\
		https://api.sendwithus.com/api/v1/send

The API takes the "first\_name", "link\_url", and "items" information entered, and passes it into the corresponding email template. The "-u" option allows the user to pass their credentials to view the website content. The "-x" option allows the user to specify cURL to use proxy to do a specific operation, such as POST. Lastly, the "-d" option sends data in a POST request to the HTTP server.

###### References ######

[1] Roy Fielding. (2000). *Representational State Transfer*. Available: http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm.

[2] Wikipedia. (2015). *Basic access authentication*. Available: https://en.wikipedia.org/wiki/Basic\_access\_authentication.

[3] Wikipedia. (2015). *Hypertext Transfer Protocol*. Available: https://en.wikipedia.org/wiki/Hypertext\_Transfer\_Protocol
