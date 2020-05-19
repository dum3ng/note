#

how to upgrade the api, and how to update the api consumer(client) ?

## client-side strategy

we can add a promt message to users using clients which version is under the
current api compatibility version.

And on the service side, add a middleware or interceptor to the routes,
check the client version in the http request, and if the version is too small
or not mainteined any more, return a response contains upgrade message.

## references

- [api-change-strategy](https://nordicapis.com/api-change-strategy/)
