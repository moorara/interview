# Web Backend

## Web Development

  * Cookie
  * Session


## Frameworks

  * **Go**
    * Go Kit
    * Gorilla
    * Echo
  * **Node.js**
    * Express.js
  * **Ruby**
    * Ruby on Rails
    * Sinatra


## API Paradigms

  * REST
  * [GraphQL](https://graphql.org)
  * RPC
    - [gRPC](https://grpc.io)
    - [JSON-RPC](https://www.jsonrpc.org)


### REST API

  * **REpresentational State Transfer**
  * REST is **resource-based** or noun-based instead of action-based or verb-based (versus RPC/SOAP).
  * Each resource has its own URI, and multiple URIs may refer to same resource.

  * Architectural Constraints:
    * **Client-Server**
      * A uniform interface separates clients from servers.
      * The separation of concerns improves the portability of clients and scalability of servers.
      * Servers and clients may also be replaced and developed independently, as long as the interface between them is not altered.
    * **Stateless**
      * No client context is stored on the server between requests.
      * Each request from any client contains all the information needed to service the request, and session state is held in the client.
      * The session state can be transferred to a database for maintaining a persistent state and allowing authentication.
    * **Cacheable**
      * Well-managed caching partially or completely eliminates some client–server interactions and improves scalability and performance.
      * Responses must implicitly or explicitly define themselves as cacheable or not to prevent clients from reusing stale or inappropriate data.
    * **Layered System**
      * A client cannot assume whether it is connected directly to the end server or to an intermediary along the way.
      * Intermediary servers improve system scalability by enabling load balancing and by providing shared caches.
    * **Code on Demand**
      * Servers can temporarily extend or customize the functionality of a client by transferring executable logic.
      * "Code on demand" is the only optional constraint of the REST architecture.
    * **Uniform Interface**
      * Resource-Based (Identification of Resources):
        * Individual resources are identified in requests using URIs as resource identifiers.
        * The resources themselves are conceptually separate from the representations that are returned to the client.
      * Manipulation of Resources through Representations:
        * A client holding representation of a resource, has enough info to modify or delete the resource, provided it has permission to do so.
      * Self-Descriptive Messages:
        * Each message includes enough information to describe how to process the message.
        * Responses also explicitly indicate their cacheability.
      * Hypermedia as the Engine of Application State (**HATEOAS**):
        * Clients deliver state via body contents, query-string parameters, request headers and the requested URI.
        * Servers deliver state to clients via body content, response codes, and response headers.
        * Links are contained in the returned body or headers to supply the URIs needed for the object itself or related objects.


  * Resource names should be nouns (use HTTP methods for specifying the verb portion of requests).
  * Resources are viewed hierarchically via their URI names. Leverage the hierarchical nature of the URL to imply structure.
  * Use identifiers in your URLs instead of in the query-string.
  * Use plurals in URL segments to keep your API URIs consistent.
  * Use lower-case in URL segments, separating words with underscores.
  * Keep URLs as short as possible, with as few segments as makes sense.


  * Use HTTP verbs for CRUD operations:
    * **POST**: Create a new resource.
    * **GET**: Read a specific resource by an identifier or a collection of resources.
    * **PUT**: Update a specific resource by an identifier or a collection of resources.
    * **DELETE**: Delete a specific resource by an identifier.


  * Use HTTP response codes to indicate status:
    * `200`: OK, general success status code.
    * `204`: CREATED, successful creation occurred. Set the Location header to contain a link to the newly-created resource.
    * `400`: BAD REQUEST, general error for when fulfilling the request would cause an invalid state.
    * `401`: UNAUTHORIZED, error code response for missing or invalid authentication token.
    * `403`: FORBIDDEN, error code for when the user is not authorized to perform the operation or the resource is unavailable for some reason.
    * `404`: NOT FOUND, the requested resource doesn't exist or there was a 401 or 403 error, for security reasons, the service wants to mask.
    * `409`: CONFLICT, a resource conflict would be caused by fulfilling the request.


  * Create fine-grained resources, start with small and easily defined resources, and provide CRUD functionality on those.
  * APIs become more self-descriptive and discoverable when links are returned in the response.
  * A self link reference informs clients how the data was or can be retrieved.
  * Utilize the HTTP Location header to contain a link on resource creation via POST or PUT.


  * The **GET** method is a **safe** method (nullipotent), meaning that calling it produces no side-effects.
  * The **PUT** and DELETE methods are **idempotent**, meaning that the operation will produce the same result no matter how many times it is repeated.
  * The **POST** method is **not idempotent** and recommended for non-idempotent resource requests.

