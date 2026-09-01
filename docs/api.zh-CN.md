# API 参考

[English](api.md) | [文档索引](README.zh-CN.md)

本清单由本仓库 package 的 `go doc -short` 生成，用于快速查看公共面。精确语义以源码和测试为准。

## 包

### `gnalloy.org/codec-ip`

包名：`ip`

```text
const Version4 = 4 ...
const ProtocolICMP = 1 ...
var ErrInvalidPacket = errors.New("gnalloy/codec/ip: invalid packet") ...
func AppendHeader(dst []byte, header Header, payloadLength int) ([]byte, error)
func Checksum(data []byte) uint16
func EncodePacket(alloc buffer.Allocator, packet Packet) (buffer.ByteBuf, error)
type Decoder struct{}
    func NewDecoder() *Decoder
type Encoder struct{}
    func NewEncoder() *Encoder
type Header struct{ ... }
    func ParseHeader(buf buffer.ByteBuf) (Header, int, error)
type Packet struct{ ... }
    func DecodePacket(buf buffer.ByteBuf) (Packet, error)
type PacketFormat uint8
    const PacketFormatPayload PacketFormat = iota ...
type ProtocolCodec struct{ ... }
    func NewProtocolCodec(cfg ProtocolCodecConfig, decoder ProtocolPayloadDecoder, ...) *ProtocolCodec
    func NewProtocolCodecFunc(cfg ProtocolCodecConfig, acceptProtocol func(int) bool, ...) *ProtocolCodec
type ProtocolCodecConfig struct{ ... }
type ProtocolPayloadDecoder interface{ ... }
type ProtocolPayloadDecoderHandler struct{ ... }
    func NewProtocolPayloadDecoder(decoder ProtocolPayloadDecoder) *ProtocolPayloadDecoderHandler
    func NewProtocolPayloadDecoderFunc(accept func(int) bool, ...) *ProtocolPayloadDecoderHandler
type ProtocolPayloadEncoder interface{ ... }
type ProtocolPayloadEncoderConfig struct{ ... }
type ProtocolPayloadEncoderHandler struct{ ... }
    func NewProtocolPayloadEncoder(cfg ProtocolPayloadEncoderConfig, encoder ProtocolPayloadEncoder) *ProtocolPayloadEncoderHandler
    func NewProtocolPayloadEncoderFunc(cfg ProtocolPayloadEncoderConfig, accept func(any) bool, ...) *ProtocolPayloadEncoderHandler
```
