This repo is to provide a minimal reproduction of an issue with OpenAPI in .NET 9.

It was generated using JetBrains Rider, the only change made was to remove the `if` statement surrounding `app.MapOpenApi();`.

Process:

- Build using provided Dockerfile
- Run resulting image
- Attempt to go to <http://localhost:8080/openapi/v1.json>
- `System.ArgumentNullException: Value cannot be null. (Parameter 'type')` is logged by the container


Versions:

- .NET (on host): 9.0.100-preview.5.24307.3
- Last tested at: 19 Jun 2024 00:12 UTC