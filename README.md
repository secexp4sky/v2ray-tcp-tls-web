# VLESS / VMess / Trojan-Go
automated script for VLESS, VMess and Trojan-Go

## Usage
```sh
curl -fsSL https://raw.githubusercontent.com/phlinhng/v2ray-tcp-tls-web/vless/src/v2gun.sh -o ~/v2gun.sh && bash ~/v2gun.sh
```
To run the script again once downloaded, just use the following command:
```
bash ~/v2gun.sh
```

## Features
1. VLESS / VMess / Trojan-Go all in one
2. Higher offloading efficieny with v2ray-core as frontend
3. Support Debian9+, Ubuntu 16+ and CentOS 7+ operation systems
4. Support both IPv4 and IPv6

## Architecture
+ VLESS over TCP with [XTLS](https://github.com/XTLS/Go) powered by v2ray-core
+ VMess over WSS on Cloudflare powered by v2ray-core and Cloudflare
+ Trojan (protocol) and muxing powered by trojan-go (implementaion)
+ Trojan over WSS on Cloudflare powered by v2ray-core, trojan-go and Cloudflare
+ HTTP Website backend powered by nginx
+ Flow chart <br>
[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW0RldmljZV0gLS0-fHd3dy5leGFtcGxlLmNvbXwgQih2MnJheS1jb3JlKVxuICAgIEIgLS0-IEl7aXMgVkxFU1M_fVxuICAgIEkgLS0-fHllc3wgQiAtLT58VkxFU1N8IEVcbiAgICBJIC0tPnxub3wgQ3t3aXRoIHBhdGg_fVxuICAgIEMgLS0-fHllcywgdm1lc3MgcGF0aHwgQiAtLT58Vk1lc3N8IEVbSW50ZXJuZXRdXG4gICAgQyAtLT58eWVzLCB0cm9qYW4gcGF0aHwgRFtUcm9qYW4tR29dIC0tPiBGe2lzIHRyb2phbj99XG4gICAgQyAtLT58d3JvbmcgcGF0aCAvIG5vIHBhdGh8IERbVHJvamFuLUdvXVxuICAgIEYgLS0-fHllc3wgRCAtLT4gfFRyb2phbnwgRVxuICAgIEYgLS0-fG5vfCBEIC0tPiB8MTI3LjAuMC4xOjgwfCBHW05HSU5YXSAtLT4gfEhUVFB8IEhbRmFrZSBXZWJzaXRlXVxuICAgIEEgLS0-fHd3dy5jbG91ZGZsYXJlLmNvbXwgS1tDbG91ZGZsYXJlXS0tPnx3d3cuZXhhbXBsZS5jb218IEIiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCIsInRoZW1lVmFyaWFibGVzIjp7ImJhY2tncm91bmQiOiJ3aGl0ZSIsInByaW1hcnlDb2xvciI6IiNFQ0VDRkYiLCJzZWNvbmRhcnlDb2xvciI6IiNmZmZmZGUiLCJ0ZXJ0aWFyeUNvbG9yIjoiaHNsKDgwLCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJwcmltYXJ5Qm9yZGVyQ29sb3IiOiJoc2woMjQwLCA2MCUsIDg2LjI3NDUwOTgwMzklKSIsInNlY29uZGFyeUJvcmRlckNvbG9yIjoiaHNsKDYwLCA2MCUsIDgzLjUyOTQxMTc2NDclKSIsInRlcnRpYXJ5Qm9yZGVyQ29sb3IiOiJoc2woODAsIDYwJSwgODYuMjc0NTA5ODAzOSUpIiwicHJpbWFyeVRleHRDb2xvciI6IiMxMzEzMDAiLCJzZWNvbmRhcnlUZXh0Q29sb3IiOiIjMDAwMDIxIiwidGVydGlhcnlUZXh0Q29sb3IiOiJyZ2IoOS41MDAwMDAwMDAxLCA5LjUwMDAwMDAwMDEsIDkuNTAwMDAwMDAwMSkiLCJsaW5lQ29sb3IiOiIjMzMzMzMzIiwidGV4dENvbG9yIjoiIzMzMyIsIm1haW5Ca2ciOiIjRUNFQ0ZGIiwic2Vjb25kQmtnIjoiI2ZmZmZkZSIsImJvcmRlcjEiOiIjOTM3MERCIiwiYm9yZGVyMiI6IiNhYWFhMzMiLCJhcnJvd2hlYWRDb2xvciI6IiMzMzMzMzMiLCJmb250RmFtaWx5IjoiXCJ0cmVidWNoZXQgbXNcIiwgdmVyZGFuYSwgYXJpYWwiLCJmb250U2l6ZSI6IjE2cHgiLCJsYWJlbEJhY2tncm91bmQiOiIjZThlOGU4Iiwibm9kZUJrZyI6IiNFQ0VDRkYiLCJub2RlQm9yZGVyIjoiIzkzNzBEQiIsImNsdXN0ZXJCa2ciOiIjZmZmZmRlIiwiY2x1c3RlckJvcmRlciI6IiNhYWFhMzMiLCJkZWZhdWx0TGlua0NvbG9yIjoiIzMzMzMzMyIsInRpdGxlQ29sb3IiOiIjMzMzIiwiZWRnZUxhYmVsQmFja2dyb3VuZCI6IiNlOGU4ZTgiLCJhY3RvckJvcmRlciI6ImhzbCgyNTkuNjI2MTY4MjI0MywgNTkuNzc2NTM2MzEyOCUsIDg3LjkwMTk2MDc4NDMlKSIsImFjdG9yQmtnIjoiI0VDRUNGRiIsImFjdG9yVGV4dENvbG9yIjoiYmxhY2siLCJhY3RvckxpbmVDb2xvciI6ImdyZXkiLCJzaWduYWxDb2xvciI6IiMzMzMiLCJzaWduYWxUZXh0Q29sb3IiOiIjMzMzIiwibGFiZWxCb3hCa2dDb2xvciI6IiNFQ0VDRkYiLCJsYWJlbEJveEJvcmRlckNvbG9yIjoiaHNsKDI1OS42MjYxNjgyMjQzLCA1OS43NzY1MzYzMTI4JSwgODcuOTAxOTYwNzg0MyUpIiwibGFiZWxUZXh0Q29sb3IiOiJibGFjayIsImxvb3BUZXh0Q29sb3IiOiJibGFjayIsIm5vdGVCb3JkZXJDb2xvciI6IiNhYWFhMzMiLCJub3RlQmtnQ29sb3IiOiIjZmZmNWFkIiwibm90ZVRleHRDb2xvciI6ImJsYWNrIiwiYWN0aXZhdGlvbkJvcmRlckNvbG9yIjoiIzY2NiIsImFjdGl2YXRpb25Ca2dDb2xvciI6IiNmNGY0ZjQiLCJzZXF1ZW5jZU51bWJlckNvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IiOiJyZ2JhKDEwMiwgMTAyLCAyNTUsIDAuNDkpIiwiYWx0U2VjdGlvbkJrZ0NvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IyIjoiI2ZmZjQwMCIsInRhc2tCb3JkZXJDb2xvciI6IiM1MzRmYmMiLCJ0YXNrQmtnQ29sb3IiOiIjOGE5MGRkIiwidGFza1RleHRMaWdodENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dERhcmtDb2xvciI6ImJsYWNrIiwidGFza1RleHRPdXRzaWRlQ29sb3IiOiJibGFjayIsInRhc2tUZXh0Q2xpY2thYmxlQ29sb3IiOiIjMDAzMTYzIiwiYWN0aXZlVGFza0JvcmRlckNvbG9yIjoiIzUzNGZiYyIsImFjdGl2ZVRhc2tCa2dDb2xvciI6IiNiZmM3ZmYiLCJncmlkQ29sb3IiOiJsaWdodGdyZXkiLCJkb25lVGFza0JrZ0NvbG9yIjoibGlnaHRncmV5IiwiZG9uZVRhc2tCb3JkZXJDb2xvciI6ImdyZXkiLCJjcml0Qm9yZGVyQ29sb3IiOiIjZmY4ODg4IiwiY3JpdEJrZ0NvbG9yIjoicmVkIiwidG9kYXlMaW5lQ29sb3IiOiJyZWQiLCJsYWJlbENvbG9yIjoiYmxhY2siLCJlcnJvckJrZ0NvbG9yIjoiIzU1MjIyMiIsImVycm9yVGV4dENvbG9yIjoiIzU1MjIyMiIsImNsYXNzVGV4dCI6IiMxMzEzMDAiLCJmaWxsVHlwZTAiOiIjRUNFQ0ZGIiwiZmlsbFR5cGUxIjoiI2ZmZmZkZSIsImZpbGxUeXBlMiI6ImhzbCgzMDQsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlMyI6ImhzbCgxMjQsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSIsImZpbGxUeXBlNCI6ImhzbCgxNzYsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNSI6ImhzbCgtNCwgMTAwJSwgOTMuNTI5NDExNzY0NyUpIiwiZmlsbFR5cGU2IjoiaHNsKDgsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNyI6ImhzbCgxODgsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSJ9fSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)](https://mermaid-js.github.io/mermaid-live-editor/#/edit/eyJjb2RlIjoiZ3JhcGggTFJcbiAgICBBW0RldmljZV0gLS0-fHd3dy5leGFtcGxlLmNvbXwgQih2MnJheS1jb3JlKVxuICAgIEIgLS0-IEl7aXMgVkxFU1M_fVxuICAgIEkgLS0-fHllc3wgQiAtLT58VkxFU1N8IEVcbiAgICBJIC0tPnxub3wgQ3t3aXRoIHBhdGg_fVxuICAgIEMgLS0-fHllcywgdm1lc3MgcGF0aHwgQiAtLT58Vk1lc3N8IEVbSW50ZXJuZXRdXG4gICAgQyAtLT58eWVzLCB0cm9qYW4gcGF0aHwgRFtUcm9qYW4tR29dIC0tPiBGe2lzIHRyb2phbj99XG4gICAgQyAtLT58d3JvbmcgcGF0aCAvIG5vIHBhdGh8IERbVHJvamFuLUdvXVxuICAgIEYgLS0-fHllc3wgRCAtLT4gfFRyb2phbnwgRVxuICAgIEYgLS0-fG5vfCBEIC0tPiB8MTI3LjAuMC4xOjgwfCBHW05HSU5YXSAtLT4gfEhUVFB8IEhbRmFrZSBXZWJzaXRlXVxuICAgIEEgLS0-fHd3dy5jbG91ZGZsYXJlLmNvbXwgS1tDbG91ZGZsYXJlXS0tPnx3d3cuZXhhbXBsZS5jb218IEIiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCIsInRoZW1lVmFyaWFibGVzIjp7ImJhY2tncm91bmQiOiJ3aGl0ZSIsInByaW1hcnlDb2xvciI6IiNFQ0VDRkYiLCJzZWNvbmRhcnlDb2xvciI6IiNmZmZmZGUiLCJ0ZXJ0aWFyeUNvbG9yIjoiaHNsKDgwLCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJwcmltYXJ5Qm9yZGVyQ29sb3IiOiJoc2woMjQwLCA2MCUsIDg2LjI3NDUwOTgwMzklKSIsInNlY29uZGFyeUJvcmRlckNvbG9yIjoiaHNsKDYwLCA2MCUsIDgzLjUyOTQxMTc2NDclKSIsInRlcnRpYXJ5Qm9yZGVyQ29sb3IiOiJoc2woODAsIDYwJSwgODYuMjc0NTA5ODAzOSUpIiwicHJpbWFyeVRleHRDb2xvciI6IiMxMzEzMDAiLCJzZWNvbmRhcnlUZXh0Q29sb3IiOiIjMDAwMDIxIiwidGVydGlhcnlUZXh0Q29sb3IiOiJyZ2IoOS41MDAwMDAwMDAxLCA5LjUwMDAwMDAwMDEsIDkuNTAwMDAwMDAwMSkiLCJsaW5lQ29sb3IiOiIjMzMzMzMzIiwidGV4dENvbG9yIjoiIzMzMyIsIm1haW5Ca2ciOiIjRUNFQ0ZGIiwic2Vjb25kQmtnIjoiI2ZmZmZkZSIsImJvcmRlcjEiOiIjOTM3MERCIiwiYm9yZGVyMiI6IiNhYWFhMzMiLCJhcnJvd2hlYWRDb2xvciI6IiMzMzMzMzMiLCJmb250RmFtaWx5IjoiXCJ0cmVidWNoZXQgbXNcIiwgdmVyZGFuYSwgYXJpYWwiLCJmb250U2l6ZSI6IjE2cHgiLCJsYWJlbEJhY2tncm91bmQiOiIjZThlOGU4Iiwibm9kZUJrZyI6IiNFQ0VDRkYiLCJub2RlQm9yZGVyIjoiIzkzNzBEQiIsImNsdXN0ZXJCa2ciOiIjZmZmZmRlIiwiY2x1c3RlckJvcmRlciI6IiNhYWFhMzMiLCJkZWZhdWx0TGlua0NvbG9yIjoiIzMzMzMzMyIsInRpdGxlQ29sb3IiOiIjMzMzIiwiZWRnZUxhYmVsQmFja2dyb3VuZCI6IiNlOGU4ZTgiLCJhY3RvckJvcmRlciI6ImhzbCgyNTkuNjI2MTY4MjI0MywgNTkuNzc2NTM2MzEyOCUsIDg3LjkwMTk2MDc4NDMlKSIsImFjdG9yQmtnIjoiI0VDRUNGRiIsImFjdG9yVGV4dENvbG9yIjoiYmxhY2siLCJhY3RvckxpbmVDb2xvciI6ImdyZXkiLCJzaWduYWxDb2xvciI6IiMzMzMiLCJzaWduYWxUZXh0Q29sb3IiOiIjMzMzIiwibGFiZWxCb3hCa2dDb2xvciI6IiNFQ0VDRkYiLCJsYWJlbEJveEJvcmRlckNvbG9yIjoiaHNsKDI1OS42MjYxNjgyMjQzLCA1OS43NzY1MzYzMTI4JSwgODcuOTAxOTYwNzg0MyUpIiwibGFiZWxUZXh0Q29sb3IiOiJibGFjayIsImxvb3BUZXh0Q29sb3IiOiJibGFjayIsIm5vdGVCb3JkZXJDb2xvciI6IiNhYWFhMzMiLCJub3RlQmtnQ29sb3IiOiIjZmZmNWFkIiwibm90ZVRleHRDb2xvciI6ImJsYWNrIiwiYWN0aXZhdGlvbkJvcmRlckNvbG9yIjoiIzY2NiIsImFjdGl2YXRpb25Ca2dDb2xvciI6IiNmNGY0ZjQiLCJzZXF1ZW5jZU51bWJlckNvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IiOiJyZ2JhKDEwMiwgMTAyLCAyNTUsIDAuNDkpIiwiYWx0U2VjdGlvbkJrZ0NvbG9yIjoid2hpdGUiLCJzZWN0aW9uQmtnQ29sb3IyIjoiI2ZmZjQwMCIsInRhc2tCb3JkZXJDb2xvciI6IiM1MzRmYmMiLCJ0YXNrQmtnQ29sb3IiOiIjOGE5MGRkIiwidGFza1RleHRMaWdodENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dENvbG9yIjoid2hpdGUiLCJ0YXNrVGV4dERhcmtDb2xvciI6ImJsYWNrIiwidGFza1RleHRPdXRzaWRlQ29sb3IiOiJibGFjayIsInRhc2tUZXh0Q2xpY2thYmxlQ29sb3IiOiIjMDAzMTYzIiwiYWN0aXZlVGFza0JvcmRlckNvbG9yIjoiIzUzNGZiYyIsImFjdGl2ZVRhc2tCa2dDb2xvciI6IiNiZmM3ZmYiLCJncmlkQ29sb3IiOiJsaWdodGdyZXkiLCJkb25lVGFza0JrZ0NvbG9yIjoibGlnaHRncmV5IiwiZG9uZVRhc2tCb3JkZXJDb2xvciI6ImdyZXkiLCJjcml0Qm9yZGVyQ29sb3IiOiIjZmY4ODg4IiwiY3JpdEJrZ0NvbG9yIjoicmVkIiwidG9kYXlMaW5lQ29sb3IiOiJyZWQiLCJsYWJlbENvbG9yIjoiYmxhY2siLCJlcnJvckJrZ0NvbG9yIjoiIzU1MjIyMiIsImVycm9yVGV4dENvbG9yIjoiIzU1MjIyMiIsImNsYXNzVGV4dCI6IiMxMzEzMDAiLCJmaWxsVHlwZTAiOiIjRUNFQ0ZGIiwiZmlsbFR5cGUxIjoiI2ZmZmZkZSIsImZpbGxUeXBlMiI6ImhzbCgzMDQsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlMyI6ImhzbCgxMjQsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSIsImZpbGxUeXBlNCI6ImhzbCgxNzYsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNSI6ImhzbCgtNCwgMTAwJSwgOTMuNTI5NDExNzY0NyUpIiwiZmlsbFR5cGU2IjoiaHNsKDgsIDEwMCUsIDk2LjI3NDUwOTgwMzklKSIsImZpbGxUeXBlNyI6ImhzbCgxODgsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSJ9fSwidXBkYXRlRWRpdG9yIjpmYWxzZX0)

## Supported Protocols
| Protocol | Transport | Direct | CDN | Qv2ray | Shadowrocket | Clash | v2rayN(G) |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| VLESS | XTLS | ✅ | ❌ | ✅ | ❌ | ❌ | ✅ |
| VLESS | TLS | ✅ | ❌ | ✅ | ✅ | ❌ | ✅ |
| VLESS | TLS + Mux | ✅ | ❌ | ✅ | ✅ | ❌ | ✅ |
| VLESS | WSS | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| VLESS | WSS  + Mux | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| VMess | WSS | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| VMess | WSS + Mux | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Trojan | TLS | ✅ | ❌ | ✅ | ✅ | ✅ | ❌ |
| Trojan | TLS + Mux | ✅ | ❌ | ✅ | ✅ | ❌ | ❌ |
| Trojan | WSS | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |
| Trojan | WSS + Mux | ✅ | ✅ | ✅ | ✅ | ❌ | ❌ |

11 protocols combinations with 13 connection methods in total.

## Related work
+ [Shawdowrockets 訂閱鏈接編輯器](https://www.phlinhng.com/b64-url-editor): subscription manager
+ [v2script](https://github.com/phlinhng/v2ray-tcp-tls-web/tree/master): v1.x version

## Telegram
https://t.me/technologyshare

## Credit
+ [Project V](https://www.v2fly.org/)
+ [V2Ray 配置指南](https://toutyrater.github.io/)
+ [新 V2Ray 白话文指南](https://guide.v2fly.org/)
+ [templated.co](https://templated.co)
+ [@liberal-boy/tls-shunt-proxy](https://github.com/liberal-boy/tls-shunt-proxy)
+ [@atrandys/trojan](https://github.com/atrandys/trojan)
+ [@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat)
+ [@mack-a/v2ray-agent](https://github.com/mack-a/v2ray-agent)
+ [@chiakge/Linux-NetSpeed](https://github.com/chiakge/Linux-NetSpeed)
+ [@ylx2016/Linux-NetSpeed](https://github.com/ylx2016/Linux-NetSpeed)
+ [@LemonBench/LemonBench](https://github.com/LemonBench/LemonBench)
+ [@tindy2013/subconverter](https://github.com/tindy2013/subconverter)
+ [@9seconds/mtg](https://github.com/9seconds/mtg)
+ [@p4gefau1t/trojan-go](https://github.com/p4gefau1t/trojan-go)
+ [@rprx/v2ray-vless](https://github.com/rprx/v2ray-vless)

## Stargazers over time
[![Stargazers over time](https://starchart.cc/phlinhng/v2ray-tcp-tls-web.svg)](https://starchart.cc/phlinhng/v2ray-tcp-tls-web)