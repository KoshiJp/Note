# intra-mart / IM-Workflow

## 横配置ノード・縦配置ノードにて展開元ノードのIDを取得する

`ActvMatterNode`の`getExecNodeConfig`メソッドにて取得できる。

```js
let locale = "";
let imwSystemMatterId = "";
let imwNodeId = "";
let actvMatterNode = new ActvMatterNode(locale, imwSystemMatterId);
let config = actvMatterNode.getExecNodeConfig(imwNodeId);
if (config.resultFlag && config.data != null) {
    if (config.data.expansionOriginalNodeId != null && config.data.expansionOriginalNodeId.length > 0) {
        originalNodeId = config.data.expansionOriginalNodeId[0];
    }
}
```
