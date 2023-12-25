# Week 2 — Distributed Tracing

Add the following Env Vars to backend-flask in docker compose:

```
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
OTEL_SERVICE_NAME: "${HONECOMB_SERVICE_NAME}"
```

You'll need to grab the API key from your honeycomb account:

```
export HONEYCOMB_API_KEY=""
export HONEYCOMB_SERVICE_NAME="Crudder"
gp env HONEYCOMB_API_KEY=""
gp env HONEYCOMB_SERVICE_NAME="Crudder"
```

### HoneyComb

When creating a new dataset in HoneyComb it will porvide all these installation instructions

We'll add the following files to our requirements.txt

```
opentelemetry-api
opentelemetry-sdk
opentelemetry-exporter-otlp-proto-http
opentelemetry-instrumentation-flask
opentelemetry-instrumentation-request
```

We'll install these dependencies

```
pip install -r requirements.txt
```

Add to the app.py

```
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry. instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

# Initialize tracing and an exporter that can send data to Honeycomb

```
provider = TracerProvider()
processor = BatchSpanProcessor (OTLPSpanExporter())
provider.add_span_processor (processor)
trace.set_tracer_provider (provider)
tracer = trace.get_tracer(__name__)
```

# Initialize automatic insturmentation with Flask
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()