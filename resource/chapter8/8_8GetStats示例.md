## 8.8 GetStats示例

考虑用户遇到不良声音并且应用程序想要确定其原因是否是丢包的情形。可能使用以下示例代码：

```javascript
async function gatherStats() {
  try {
    const sender = pc.getSenders()[0];
    const baselineReport = await sender.getStats();
    await new Promise((resolve) => setTimeout(resolve, aBit)); // ... wait a bit
    const currentReport = await sender.getStats();

    // compare the elements from the current report with the baseline
    for (let now of currentReport.values()) {
      if (now.type != 'outbound-rtp') continue;

      // get the corresponding stats from the baseline report
      const base = baselineReport.get(now.id);

      if (base) {
        const remoteNow = currentReport.get(now.remoteId);
        const remoteBase = baselineReport.get(base.remoteId);

        const packetsSent = now.packetsSent - base.packetsSent;
        const packetsReceived = remoteNow.packetsReceived - remoteBase.packetsReceived;

        const fractionLost = (packetsSent - packetsReceived) / packetsSent;
        if (fractionLost > 0.3) {
          // if fractionLost is > 0.3, we have probably found the culprit
        }
      }
    }
  } catch (err) {
    console.error(err);
  }
}
```

