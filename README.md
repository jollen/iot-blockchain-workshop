# Flowchain on MediaTek Linkt It Smart 7688

* Flowchain 是物聯網專用區塊鏈（IoT Blockchain）
* 在這次的體驗課程裡，將使用 MediaTek Linkt It Smart 7688 物聯網開發板，來驗體 IoT Blockchain 的幾個玩法

## 準備工作

* 請自備 Notebook 並安裝 Node.js v4.5 以上環境
* 能看懂基本的 JavaScript 語法 (optional)

## 安裝步驟

下載 Flowchain 系統：

```
$ git clone https://github.com/jollen/flowchain-core.git
$ npm install
$ export HOST=10.186.110.91
$ export PORT=8000
```
修改 peer.js 主程式：

```
// Start the server
server.start({
    onstart: onstart,
    onmessage: onmessage,
    onquery: onquery,
    ondata: ondata,
    join: {
        address: '192.168.0.1',
        port: '8000'
    }
});
```
教室現場會準備 2 個 peer-to-peer 的 node，請修改 ```join``` 參數，加入任一個 peer node 即可。

## 挖礦

Flowchain 具備一個專為 IoT device 重新設計的挖嚝系統，這個系統採用 Mining-based Proof-of-Stake 機制；在資料的交易過程中，可以撰寫一份 Smart contract 來改變挖礦難度。

### Smart Contracts

Flowchain 底層有一個 Lua VM；可以使用 Lua 來撰寫 Smart contract。根據 Flowchain 的技術白皮書，來調整 Probability density 的值。撰寫一份 Smart contract 來 override 機率分佈函數：

```
function distributions.norm.pdf(x, mu, sigma)
    return cephes.exp(-.5 * (x-mu)*(x-mu)/(sigma*sigma)) / math.sqrt(2.0*math.pi*sigma*sigma)
end
```

## Resources

* Flowchain, https://flowchain.io
* Top 10 Blockchain Companies to Watch in 2017, http://www.disruptordaily.com/top-10-blockchain-companies-to-watch-in-2017/
