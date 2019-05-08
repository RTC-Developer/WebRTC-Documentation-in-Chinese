## 6.4垃圾收集

`RTCDataChannel`对象必须不能被垃圾回收如果它的

- [ReadyState]插槽为`connecting`并且至少一个事件听众以`open`，`message`，`error`，`close`事件登记。
- [ReadyState]插槽为`open`并且至少一个事件听众以`message`，`error`，`close`事件登记。
- [ReadyState]插槽为`closing`并且至少一个事件听众以`error`，`close`事件登记。
- 底层数据传输被建立，并且数据已经排序准备传输。
