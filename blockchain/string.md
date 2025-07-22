# String
## keccak256
EVM 内置的加密哈希函数，输入任意长度 bytes，输出固定 32 字节 bytes32（也叫 Keccak-256 / SHA-3 变体）;
使用 keccak256思路
`先将文字转换为字节-> 计算256位哈希 -> 比较哈希是否一致`
+ 确定性： 同一输入永远得到同一输出
+ 固定长度： 无论原字符多长，hash都是32字节，比较开销固定且便宜
+ 极低碰撞率：找到两端不同数据却相同哈希的难度极低，基本不可能

``` solidity
// 把字符串打包成 btyes
bytes memory packed = abi.encodePacked('A');
bytes memory packedBLT = abi.encodePacked("BLT");

// 分别取keccak-256 HASH ,结果是  bytes32
bytes32 h1 = keccak256(packed);
bytes32 h2 = keccak256(packedBLT);

// ③ 比较哈希
if (h1 == h2) { eat(); }

```



## abi.encodePacked()
把若干参数紧凑打包成 bytes，常用来给哈希函数做输入

