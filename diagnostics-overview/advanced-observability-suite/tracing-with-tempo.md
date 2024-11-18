# Tracing with Tempo

Tempo is the tracing backend, and Alloy and Beyla are the collectors. They use eBPF technology to collect traces without requiring instrumentation.

Grafana Beyla is utilized for tracing. Beyla uses eBPF (extended Berkeley Packet Filter) to collect observability data directly from the kernel without modifying the application code.&#x20;

eBPF allows Beyla to attach to system-level events, such as network requests or function calls, and gather metrics and traces efficiently. You can fine-tune the application with OTEL SDK, receive detailed traces, and include traces in the logs.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

One can go from traces to metrics

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

