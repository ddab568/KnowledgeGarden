
A note describing some of the different API architectures/protocols, namely RPC, REST and GraphQL.

## RPC - Remote Procedure Call

Earliest API architecture. Remote Procedure Call (RPC), as the name implies, calls a remote "[procedure](programming-paradigms#procedural-programming,1:#*)" or a function e.g. from a client application to the API on a server.

How the procedure/function is invoked on the server depends on the framework and choice of technology adopted. RPC is just a concept, and in a simple scenario, the method called could be determined by simply parsing query parameters from the url coming from the client and performing a string comparison, matching the method from the client to the server.

A contrived example where a client invokes the API to perform mathematical operations on two numbers 'a' and 'b' and return the result:

```Javascript
/** Server API **/
const express = require('express')
const app = express()
const port = 3000

app.get('/',(req, res) => {
  // extract the method being called from the query params
  // URL is in the format http(s)://<host>/method=<methodName>&b=<b>&c=<c>
  const { method } = req.query;
  const a = parseInt(req.query.a);
  const b = parseInt(req.query.b);

  let methodResponse = "";

  // call the method requested - here we do a simple string comparison
  // so that it appears the FE and BE "share" procedures
  switch(method) {
     case "add":
     	methodResponse = add(a,b);
        break;
     case "multiply":
     	methodResponse = multiply(a,b);
        break;
     case "minus":
     	methodResponse = minus(a,b);
	break;
     default:
        methodResponse = "method doesn't exist";

  }

  res.send({ result: methodResponse });
})

function add(a, b) {
  return a + b;
}

function multiply(a, b) {
  return a * b;
}

function minus(a, b) {
  return a - b;
}
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
})

```

A client can communicate to the above API application as follows:

```bash
GET http://localhost:3000/?method=multiply&a=4&b=2
{output: 8} #response recieved

```

### Disadvantages

**Tight coupling** - RPCs client and server are tightly coupled since function calls need to match.

**Leaking internal implementation** - It may be considered a flaw that the inner workings of the API are somewhat revealed to the client as the backend method names may be "telling".

**Extensibility of methods is difficult** - it's often the case that in RPC API's, a procedure may not perform the exact functionality and hence another method that does something slightly different is added. In this case, there is an overload of similar functions which can be messy:

```javascript
function multiply() {
  // does something
}

function multiplyV2() {
  // does something similar to multiply() but different
}

function multiplyV3() {
  // etc
}
```

### Advantages

**Lightweight** - RPC APIs are expected not to return a lot of meta data and the most popular frameworks such as gRPC are built in such a way that allows them to be more performant than their REST counterpart.

**Action-oriented** - RPCs are good for action oriented applications where we are calling 'commands' rather than focusing on resources.

### gRPC

One of the most notable examples of RPC frameworks in modern day is [gRPC](https://grpc.io/). gRPC is an open-source Google framework used for high performance microservice architecture styles. It's supported by multiple languages/frameworks such as Go, Node, Rust Python and more. It's used by many well known tech companies such as Square, Netlfix and [Cloudflare](https://blog.cloudflare.com/road-to-grpc/).

gRPC is considered highly performant due to:

- Using HTTP/2 for transport
- Allowing both clients and servers to stream data as opposed to polling (_Note: I believe this is available due to HTTP/2_)
- Encouraging **Protobuf** as the messaging format

Protobuf (protocol buffers) are a message format that allow for serialization of structured data in a language neutral way. They are an alternative messaging format to others such as JSON or XML and are considered more compact to achieve low latency.

Example of a Protobuf message:

```Protobuf
// Person.proto
message Person {
  required string name = 1;
  required int32 age = 2;
  optional string email = 3;
}
```

Protobufs are encoded in such a way that makes them lightweight and performant.

![](/assets/images/2022-03-03-10-51-00.png)

<caption>Source: https://developers.google.com/protocol-buffers/docs/overview#work</caption>
<br>
<br>

gRPC can be implemented using a variety of languages or frameworks, however it seems performance varies - multiple language performance tests are [performed often](https://grpc.io/docs/guides/benchmarking/) on the code base. Note that the [performance dashboard](https://grafana-dot-grpc-testing.appspot.com/?kiosk=tv) is missing Node however, it has been [benchmarked by 3rd parties](https://www.nexthink.com/blog/comparing-grpc-performance/) and _appears_ to be less performant than alternatives such as Go.

gRPC currently cannot natively communicate with the web via HTML/2. Browsers do not support protobuf payloads and hence, grpc-web was introduced in order to act as a proxy to serialize web payload and give developers the ability to use protobufs across the full stack:

![https://grpc.io/blog/state-of-grpc-web/](/assets/images/2022-03-03-10-13-17.png)

<caption>Source: https://grpc.io/blog/state-of-grpc-web/</caption>

</br>
</br>
Prior to this, developers would likely use REST APIs with HTTP to communicate with the gRPC backend.

## REST

**Re**presentational **s**tate **t**ransfer (REST) API is an architectural style created by Roy Fielding, described famously in his [dissertation](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm).

REST is commonly not adhered to when implemented as many APIs do not tick the architectural constraints that make an API "RESTful". There are **6 constraints** which make a web service truly RESTful:

1. **Uniform Interface**

What distinguishes REST is uniform interface whereby the client and server are decoupled in such a way that allows them tfcv o evolve independently. Having this interface provides the client with enough information to retrieve the relevant data without having to understand the underlying implementation. This concept is achieved through these four principles:

- **Identification of resources** - where RPCs are command or action oriented, REST APIs are modeled around resources. For example, users in a rest API are handled via the URI `/user`

- **Manipulation of resources through representations** - When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource on the server. This makes REST APIs **discoverable** in that from the root of the API, the client has enough information to perform any available action on the available resources.

- **self-descriptive messages** - Each message includes enough information to describe how to process the message. For example, by using standard [MIME Types](https://en.wikipedia.org/wiki/Media_type#cite_note-10) e.g. `application/json`, . Responses also explicitly indicate their cache-ability. e.g. `Cache-Control: max-age=31536000`

- **hypermedia as the engine of application state (HATEOAS)** - allows the client to dynamically navigate to the appropriate resources by traversing the hypermedia links. For example, a call to `GET http://localhost:8080/users` could return:

```JSON


```

#### References

1. https://blog.jscrambler.com/rpc-style-vs-rest-web-apis
2. https://grpc.io/
3. https://www.restapitutorial.com/lessons/whatisrest.html#
