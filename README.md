# echo-chamber

[![Clojars Project](http://clojars.org/echo-chamber/latest-version.svg)](http://clojars.org/echo-chamber)

A minimalist SDK for setting up a handler for implementing an Echo application server.

Follows the example of the Java SDK by requiring methods for handling each request type.

## Usage

This SDK is designed to be placed in between a web server (such as Ring or Compojure) and your application, providing
simple routing and schema validation, as well as response convenience methods.

Since the functions are annotated using Prismatic schema, `with-fn-validation` can be used to validate responses. See the [schema documentation](https://github.com/Prismatic/schema) for more information.

To use the SDK, implement the IEchoApp protocol found in the echo/core namespace.
Then, get a dispatcher function by passing the app the `request-dispatcher` (also in echo/core).

This dispatcher expects to receive an EchoRequest structured map (NOT a json string). Your server or middleware
should handle deserializing that before you pass it to the dispatcher. See echo/schemas for more information on the schemas to be provided.

Finally, your app should return an EchoResponse struct. The echo/response namespace has convenience functions for creating this, the penultimate function being `respond`

For help/an example, try using the [echo-chamber-compojure template](http://github.com/blandflakes/echo-chamber-compojure)

## Future enhancements
- Potentially an intent dispatcher
- Breakout modes for common interactions - i.e. a confirm interaction could be modeled for me.
- Consider dynamically binding session so it's not part of the signature
