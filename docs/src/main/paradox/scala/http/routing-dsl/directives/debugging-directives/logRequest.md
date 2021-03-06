# logRequest

## Signature

```scala
def logRequest(marker: String)(implicit log: LoggingContext): Directive0
def logRequest(marker: String, level: LogLevel)(implicit log: LoggingContext): Directive0
def logRequest(show: HttpRequest => String)(implicit log: LoggingContext): Directive0
def logRequest(show: HttpRequest => LogEntry)(implicit log: LoggingContext): Directive0
def logRequest(magnet: LoggingMagnet[HttpRequest => Unit])(implicit log: LoggingContext): Directive0
```

The signature shown is simplified, the real signature uses magnets. <a id="^1" href="#1">[1]</a>

> <a id="1" href="#^1">[1]</a> See [The Magnet Pattern](http://spray.io/blog/2012-12-13-the-magnet-pattern/) for an explanation of magnet-based overloading.

## Description

Logs the request using the supplied `LoggingMagnet[HttpRequest => Unit]`.  This `LoggingMagnet` is a wrapped
function `HttpRequest => Unit` that can be implicitly created from the different constructors shown above. These
constructors build a `LoggingMagnet` from these components:

>
 * A marker to prefix each log message with.
 * A log level.
 * A `show` function that calculates a string representation for a request.
 * An implicit `LoggingContext` that is used to emit the log message.
 * A function that creates a `LogEntry` which is a combination of the elements above.

It is also possible to use any other function `HttpRequest => Unit` for logging by wrapping it with `LoggingMagnet`.
See the examples for ways to use the `logRequest` directive.

Use `logResult` for logging the response, or `logRequestResult` for logging both.

## Example

@@snip [DebuggingDirectivesExamplesSpec.scala]($test$/scala/docs/http/scaladsl/server/directives/DebuggingDirectivesExamplesSpec.scala) { #logRequest-0 }