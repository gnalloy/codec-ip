# 案例

[English](examples.md) | [文档索引](README.zh-CN.md)

## 案例 1：将模块加入应用

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/codec-ip@dev
go doc gnalloy.org/codec-ip
```

## 案例 2：查看当前包

当前源码树暴露这些 package 导入路径：
- `gnalloy.org/codec-ip`

按需要的行为对对应 package 执行 `go doc`：

```bash
go doc gnalloy.org/codec-ip
```

精选当前导出入口：
- `const Version4 = 4 ...`
- `const ProtocolICMP = 1 ...`
- `var ErrInvalidPacket = errors.New("gnalloy/codec/ip: invalid packet") ...`
- `func AppendHeader(dst []byte, header Header, payloadLength int) ([]byte, error)`
- `func Checksum(data []byte) uint16`
- `func EncodePacket(alloc buffer.Allocator, packet Packet) (buffer.ByteBuf, error)`

## 案例 3：将可执行测试作为行为示例

仓库测试是受支持行为的可执行示例。先从下面的精选名称开始，再阅读对应 `_test.go` 文件中的完整 setup 和断言。完整发现列表见 [测试与性能](testing.zh-CN.md)。

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

精选当前 test、benchmark、fuzz 与 example 入口：
- `BenchmarkEncodeDecodeIPv4Packet`
- `TestDecodeIPv4PacketFragmentedHeader`
- `TestEncodeDecodeIPv4PacketZeroCopyPayload`
- `TestEncodeDecodeIPv6Packet`
- `TestPipelineDecodeEncodeRawAddressed`
- `TestProtocolCodecIPPacketFormatReadsAndWritesFullIPPackets`
- `TestProtocolCodecPayloadFormatReadsAndWritesRawPackets`
- `TestProtocolPayloadDecoderDispatchesCustomProtocol`
- `TestProtocolPayloadEncoderBuildsRawIPPackedPayload`

## 案例 4：跨模块装配

本模块的直接 Gnalloy 依赖：
- `gnalloy.org/gnalloy`
- `gnalloy.org/transport-raw`

装配说明：
- codec 位于面向字节或 datagram 的 transport 之上、应用 handler 之下。
- 它负责把字节或 Gnalloy 消息转换成协议对象，并把出站协议对象转换回字节。
- 它不打开 socket，不拥有 EventLoop，也不定义应用生命周期。

## 案例 5：压测 Harness

持续负载测试时，如果该模块参与网络流量路径，将它接入 `gnalloy.org/benchmarks` 的场景，或接入 `gnalloy.org/examples` 的可运行客户端。报告中记录 host、OS、CPU、Go version、protocol、payload、concurrency、warmup、repetitions、throughput 和 p99 latency。
