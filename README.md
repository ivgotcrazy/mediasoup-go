# Mediasoup-Go

A Go library for [mediasoup](https://github.com/versatica/mediasoup) that enables WebRTC Selective Forwarding Unit (SFU) functionality without Node.js dependencies.

> **Note**: v2.x.x tag only supports mediasoup v3.14.0 and above. For mediasoup v3.13.0 below, please use v1.x.x tag.

## Features
- Full mediasoup v3 API support in Go
- Consistent API design with the original Node.js version
- Uses `Cmd.ExtraFiles` for worker communication (not compatible with Windows)
- Supports multi-core processing via `PipeTransport`

## Prerequisites
- Download the prebuilt mediasoup worker from [mediasoup releases](https://github.com/versatica/mediasoup/releases)
- Linux or macOS (Windows not supported)

## Installation
```go
import "github.com/jiyeyuran/mediasoup-go/v2"
```

## Documentation
- [Go API Documentation](https://pkg.go.dev/github.com/jiyeyuran/mediasoup-go/v2)
- [Official mediasoup Documentation](https://mediasoup.org/documentation/v3/mediasoup/api/)

## Example Usage
See [mediasoup-go-demo](https://github.com/jiyeyuran/mediasoup-go/v2-demo) for a complete example application.

<details>
<summary>Click to see code example</summary>

```go
package main

import (
    "github.com/jiyeyuran/mediasoup-go/v2"
    // ... other imports
)

func main() {
    // Create worker
    worker, err := mediasoup.NewWorker("path/to/mediasoup-worker")
    if err != nil {
        panic(err)
    }

    // Create router
    router, err := worker.CreateRouter(&mediasoup.RouterOptions{
        // Configure media codecs
    })

    // Create WebRTC transport
    transport, err := router.CreateWebRtcTransport(&mediasoup.WebRtcTransportOptions{
        ListenInfos: []mediasoup.TransportListenInfo{
            {IP: "0.0.0.0", AnnouncedAddress: "your.public.ip"},
        },
    })

    // Use the transport to produce/consume media
    // ...
}
```
</details>

## License
[ISC](/LICENSE)

