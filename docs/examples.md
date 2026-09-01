# Examples

[简体中文](examples.zh-CN.md) | [Docs Index](README.md)

## Example 1: Add the Module to an Application

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/codec-ip@dev
go doc gnalloy.org/codec-ip
```

## Example 2: Inspect Current Packages

The current source tree exposes these package import paths:
- `gnalloy.org/codec-ip`

Use `go doc` against the package that matches the behavior you need:

```bash
go doc gnalloy.org/codec-ip
```

Selected current exported entry points:
- `const Version4 = 4 ...`
- `const ProtocolICMP = 1 ...`
- `var ErrInvalidPacket = errors.New("gnalloy/codec/ip: invalid packet") ...`
- `func AppendHeader(dst []byte, header Header, payloadLength int) ([]byte, error)`
- `func Checksum(data []byte) uint16`
- `func EncodePacket(alloc buffer.Allocator, packet Packet) (buffer.ByteBuf, error)`

## Example 3: Use Executable Tests as Behavioral Examples

Repository tests are executable examples of supported behavior. Start with the selected names below, then read the matching `_test.go` files for complete setup and assertions. See [Testing and Performance](testing.md) for the complete discovered list.

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

Selected current test, benchmark, fuzz, and example entry points:
- `BenchmarkEncodeDecodeIPv4Packet`
- `TestDecodeIPv4PacketFragmentedHeader`
- `TestEncodeDecodeIPv4PacketZeroCopyPayload`
- `TestEncodeDecodeIPv6Packet`
- `TestPipelineDecodeEncodeRawAddressed`
- `TestProtocolCodecIPPacketFormatReadsAndWritesFullIPPackets`
- `TestProtocolCodecPayloadFormatReadsAndWritesRawPackets`
- `TestProtocolPayloadDecoderDispatchesCustomProtocol`
- `TestProtocolPayloadEncoderBuildsRawIPPackedPayload`

## Example 4: Cross-Module Assembly

Direct Gnalloy dependencies for this module:
- `gnalloy.org/gnalloy`
- `gnalloy.org/transport-raw`

Assembly guidance:
- Use this codec above a byte-oriented or datagram transport and below application handlers.
- The codec converts bytes or Gnalloy messages into protocol objects and converts outbound protocol objects back to bytes.
- It does not open sockets, own EventLoops, or define application lifecycle.

## Example 5: Pressure-Test Harness

For sustained load, wire this module into a scenario under `gnalloy.org/benchmarks` or a runnable client under `gnalloy.org/examples` when the module participates in network traffic. Record host, OS, CPU, Go version, protocol, payload, concurrency, warmup, repetitions, throughput, and p99 latency in the report.
