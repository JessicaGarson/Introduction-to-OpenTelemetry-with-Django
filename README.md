# Introduction to OpenTelemetry with Django
OpenTelemetry (OTel) is a vendor-neutral, open-source framework for observability designed to be compatible with any backend system. It offers standardized APIs, libraries, and tools for gathering telemetry data, including metrics, logs, and traces. This presentation serves as an introduction to using OpenTelemetry with Django.

## Slides
You can find slides to accompany this talk in the folder of this repository entitled [slides](https://github.com/JessicaGarson/Introduction-to-OpenTelemetry-with-Django/tree/main/slides).

## Examples
###  Getting telemetry data to show in your console
For telemetry to show in your terminal, your `manage.py` file should look like this:

```python
import os
import sys
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor, ConsoleSpanExporter
from opentelemetry.sdk import resources

def main():
    """Run administrative tasks."""
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "todolist_project.settings")

    resource = resources.Resource(attributes={
        resources.SERVICE_NAME: "your-service-name",
        resources.SERVICE_VERSION: "1.0.0"
    })

    trace_provider = TracerProvider(resource=resource)
    trace.set_tracer_provider(trace_provider)

    console_exporter = ConsoleSpanExporter()

    span_processor = BatchSpanProcessor(console_exporter)
    trace.get_tracer_provider().add_span_processor(span_processor)
    
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)


if __name__ == "__main__":
    main()
```

### Example applications
This repository contains two example applications, one showing [automatic instrumentation](https://github.com/JessicaGarson/Introduction-to-OpenTelemetry-with-Django/tree/main/automatic-instrumentation/todolist_project) and the other [manual instrumentation](https://github.com/JessicaGarson/Introduction-to-OpenTelemetry-with-Django/tree/main/manual-instrumentation/todolist_project) using OpenTelemetry, sending the results into Elastic. Both applications are simple to-do list applications made with Django.

#### Getting started
Before you can use either, you will need to do the following:

- Create a virtual environment.

  Mac:
  
  ```
  python -m venv venv
  source venv/bin/activate
  ```

  Windows:

  ```
  python -m venv venv
  .\venv\Scripts\activate
  ```

- Install the required packages:

  ``` 
  pip install -r requirements.txt
  ```

- Move the `env.example` into the root of whichever example you want to run. Be sure to update it with your own credentials and save it as `.env`. 

#### Running the example applications

You can use the following command to run each example application:

```
python manage.py runserver
```

#### Viewing the results in Elastic
If everything is working as intended, you should be able to see observablity data in the Services section in Elastic APM.

### Example collector
[`example_collector.yaml`](example_collector.yaml) example of a collector that sends data to Elastic.


## Resources 
- [OpenTelemetry docs](https://opentelemetry.io/)
- [OpenTelemetry collectors](https://opentelemetry.io/docs/collector/) 
- [OpenTelemetry SDKs](https://opentelemetry.io/docs/languages/)
- [Django Instrumentation](https://opentelemetry-python.readthedocs.io/en/latest/examples/django/README.html)
- [Introducing Elastic Distribution for OpenTelemetry Python](https://www.elastic.co/observability-labs/blog/elastic-opentelemetry-distribution-python)
- [elastic-otel-python](https://github.com/elastic/elastic-otel-python)
- [Elastic OpenTelemetry integration](https://www.elastic.co/guide/en/observability/current/apm-open-telemetry.html)
- [Elastic Observability Fundamentals](https://www.elastic.co/training/observability-fundamentals)
- [Automatic instrumentation with OpenTelemetry for Python applications](https://www.elastic.co/observability-labs/blog/auto-instrumentation-python-applications-opentelemetry)

### Other talks
- [How To Monitor and Troubleshoot Applications using OpenTelemetry](https://www.youtube.com/watch?v=oTzIieqwMW0)
- [A practical guide to using OpenTelemetry in Python by Tom Eastman](https://www.youtube.com/watch?v=R8BYnL-Yp1w)
- [The State of OpenTelemetry](https://xeraa.net/talks/on-the-bleeding-edge-of-open-telemetry/)

### Other
- [APM Agent vs OpenTelemetry](https://discuss.elastic.co/t/elastic-apm-agent-vs-opentelemetry-client/332903)
- [Independence with OpenTelemetry on Elastic](https://www.elastic.co/blog/opentelemetry-observability)
- [What is OpenTelemetry?](https://www.codingblocks.net/podcast/what-is-opentelemetry/#more-40442)
