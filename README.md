# 期刊域名规则集
本项目收集了期刊论文出版商的域名，
Clash 均使用以下格式：
```yaml
- DOMAIN-SUFFIX,cnki.net
```
QuantumultX 均使用以下格式：
```yaml
HOST-SUFFIX,cnki.net,Clash_paper
```
# 使用方法
Clash 规则集借鉴[FantasticMao](https://github.com/fantasticmao/clash-rules/blob/main/README.md)
的规则集使用方法，感谢！

以下是复制 FantasticMao 的使用方法，在 rule-providers 中添加了 paper 规则集，rules 添加 paper 规则集指向直连策略组
```yaml
proxies:
  - name: proxy01
    type: ss
    server: server
    port: 443
    cipher: chacha20-ietf-poly1305
    password: password
  - name: proxy02
    type: vmess
    server: server
    port: 443
    uuid: uuid
    alterId: 32
    cipher: auto

proxy-groups:
  - name: PROXY
    type: url-test
    proxies:
      - proxy01
      - proxy02
    url: http://www.gstatic.com/generate_204
    interval: 300

# Premium only
rule-providers:
  common:
    type: http
    behavior: classical
    url: https://gh-proxy.com/https://raw.githubusercontent.com/fantasticmao/clash-rules/main/common.yaml
    interval: 3600
    path: ./ruleset/common.yaml
  telegramcidr:
    type: http
    behavior: classical
    url: https://gh-proxy.com/https://raw.githubusercontent.com/fantasticmao/clash-rules/main/telegramcidr.yaml
    interval: 3600
    path: ./ruleset/telegramcidr.yaml
  #添加 paper 规则集
  paper:
    type: http
    behavior: classical
    url: https://gh-proxy.com/https://raw.githubusercontent.com/fantasticmao/clash-rules/main/common.yaml
    interval: 3600
    path: ./ruleset/paper.yaml
rules:
  - RULE-SET,common,PROXY
  - RULE-SET,telegramcidr,PROXY
  #添加 paper 规则集到直连策略组
  - RULE-SET,paper,DIRECT
  # Others
  - GEOIP,CN,DIRECT
  - MATCH,DIRECT
```

# 目的
因个人原因，需要经常查阅文献，使用 Clash 过程中发现开源的规则集并没有收录
期刊出版商的域名规则。相当长时间查阅文献时需要手动开关 Clash 很不优雅。遂
自定义 Clash 配置文件，手动添加遇到的出版商域名，最近一次发现已经积攒了相
当一部分规则，于是决定维护期刊出版商规则。
