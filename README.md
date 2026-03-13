# Emergent Registry

Official registry of Emergent primitives for the marketplace.

## Structure

```
emergent-registry/
├── index.toml                 # Index of all primitives
└── primitives/
    └── <name>/
        └── manifest.toml      # Detailed manifest for each primitive
```

## Available Primitives

| Name | Kind | Description |
|------|------|-------------|
| http-source | source | Generic HTTP webhook receiver |
| exec-source | source | Execute shell commands and emit output as events |
| exec-handler | handler | Pipe event payloads through any executable and publish results |
| exec-sink | sink | Pipe event payloads through any executable (fire-and-forget) |
| topology-viewer | sink | Real-time D3.js workflow visualization |

## Usage

Install primitives with the Emergent CLI:

```bash
emergent marketplace list
emergent marketplace install exec-sink
emergent marketplace info exec-handler
```

Configure the registry URL in `~/.config/emergent/marketplace.toml`:

```toml
[registry]
url = "https://raw.githubusercontent.com/Govcraft/emergent-registry/main"
```

## Registry Schema

### index.toml

```toml
[registry]
name = "emergent-official"
version = "1.0.0"
description = "Official Emergent primitives registry"

[[primitives]]
name = "example-source"
version = "0.1.0"
kind = "source"                    # source | handler | sink
description = "Brief description"
publishes = ["type.event"]         # for sources/handlers
subscribes = ["*"]                 # for handlers/sinks
tags = ["tag1", "tag2"]
```

### manifest.toml

```toml
[primitive]
name = "example-source"
version = "0.1.0"
kind = "source"
description = "Full description"
homepage = "https://github.com/..."
license = "MIT"

[messages]
publishes = ["type.event"]

[[args]]
name = "token"
long = "token"
short = "t"
env = "EXAMPLE_TOKEN"
required = true
description = "Authentication token"

[binaries]
release_url = "https://github.com/.../releases"

[binaries.checksums]
x86_64-unknown-linux-gnu = "sha256:..."

[binaries.targets]
x86_64-unknown-linux-gnu = "example-0.1.0-x86_64-unknown-linux-gnu.tar.gz"
```
