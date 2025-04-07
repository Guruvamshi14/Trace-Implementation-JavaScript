## Trace Implemnetation Java Script

Contents
- Install the GitHub Trace Application Package
- Run Jaeger Using Docker
- Install and Use Trace and Span in the Handler Function

## Install the GutHub Package 

Create package.json file

```
npm init -y 
```

Run the command in the Project folder

```
npm install github:Guruvamshi14/Trace-Implementation-JavaScript
```
Now you can see the github folder in you dependencies(package.json file)

```
"js-trace": "github:Guruvamshi14/Trace-Implementation-JavaScript"
```

Include this in Index.js at top of the file

```
require('js-trace');
```


## Run Jeager Using Docker

```
docker run --rm \
  -e COLLECTOR_ZIPKIN_HOST_PORT=:9411 \
  -p 16686:16686 \
  -p 4317:4317 \
  -p 4318:4318 \
  -p 9411:9411 \
  jaegertracing/all-in-one:latest
```
Access the Jaeger UI at: http://localhost:16686

## Intialization of Tracer

```
const tracer = trace.getTracer('Name');

```

## Intialization of Span


```
tracer.startActiveSpan('Name of the Span', (spanObject) => {});
```
First, create a parent span, then create the child spans inside the parent span so that every span gets the same trace ID.


Here is the example how of intialize the span
```
tracer.startActiveSpan('Home Route', (rootSpan) => {
        tracer.startActiveSpan('Fetching User Data', { parent: rootSpan }, (userSpan) => {
                userSpan.end();
        });

        tracer.startActiveSpan('Fetching External Info', { parent: rootSpan }, (externalInfoSpan) => {
                externalInfoSpan.end();
        });

    });

```

## Reference

If you have any doubts about initializing a trace or span, you can refer to this mini project on tracing in Go:

👉 [JS Mini Project](https://github.com/Guruvamshi14/JavaScript-Mini-project-Trace-Application
)
