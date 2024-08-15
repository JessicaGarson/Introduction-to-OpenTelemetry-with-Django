# Introduction to OpenTelemetry with Django
OpenTelemetry (OTel) is a vendor-neutral, open-source framework for observability designed to be compatible with any backend system. It offers standardized APIs, libraries, and tools for gathering telemetry data, including metrics, logs, and traces. This presentation serves as an introduction to using OpenTelemetry with Django.

## Examples
This repository contains two example applications, one showing automatic instrumentation and the other manual instrumentation using OpenTelemetry, sending the results into Elastic. Both applications are simple to-do list applications made with Django.

### Getting started
Before you can use ethier, you will need to do the following:

- Create a virtual environment.

  Mac:
  
  ```
  python -m venv venv
  source venc/bin/activate
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

### Running the example application

You can use the following command to run each example application:

```
python manage.py runserver
```

## Resources 
- [OpenTelemetry docs](https://opentelemetry.io/)
- [OpenTelemetry collectors](https://opentelemetry.io/docs/collector/) 
- [OpenTelemetry SDKs](https://opentelemetry.io/docs/languages/)
- [Django Instrumentation](https://opentelemetry-python.readthedocs.io/en/latest/examples/django/README.html)
- [elastic-otel-python](https://github.com/elastic/elastic-otel-python)
- [Elastic OpenTelemetry integration](https://www.elastic.co/guide/en/observability/current/apm-open-telemetry.html)
- [Elastic Observability Fundamentals](https://www.elastic.co/training/observability-fundamentals)

### Other talks
- [How To Monitor and Troubleshoot Applications using OpenTelemetry](https://www.youtube.com/watch?v=oTzIieqwMW0)
- [A practical guide to using OpenTelemetry in Python by Tom Eastman](https://www.youtube.com/watch?v=R8BYnL-Yp1w)
- [The State of OpenTelemetry](https://xeraa.net/talks/on-the-bleeding-edge-of-open-telemetry/)

### Other
- [APM Agent vs OpenTelemetry](https://discuss.elastic.co/t/elastic-apm-agent-vs-opentelemetry-client/332903)
- [Independence with OpenTelemetry on Elastic](https://www.elastic.co/blog/opentelemetry-observability)
- [What is OpenTelemetry?](https://www.codingblocks.net/podcast/what-is-opentelemetry/#more-40442)
