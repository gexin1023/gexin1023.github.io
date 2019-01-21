---
layout: post
title: ecrecover调用——solidity内置函数 & 固定地址调用
toc: true
---

# ecrecover调用——solidity内置函数 & 固定地址调用

在evm实现中, ecrecover是在vm/contracts.go中硬编码的固定地址合约，比如ecrecover地址为`0x1`。Solidity合约编译时，会识别`ecrecover`关键字，并编译为调用地址为`0x1`的调用字节码。

```
// PrecompiledContractsHomestead contains the default set of pre-compiled Ethereum
// contracts used in the Frontier and Homestead releases.
var PrecompiledContractsHomestead = map[common.Address]PrecompiledContract{
    common.BytesToAddress([]byte{1}): &ecrecover{},
    common.BytesToAddress([]byte{2}): &sha256hash{},
    common.BytesToAddress([]byte{3}): &ripemd160hash{},
    common.BytesToAddress([]byte{4}): &dataCopy{},
}
```

所以理论上，直接调用地址为0x1位置的合约，可以实现ecrecover。 写了一个solidity合约，验证果然如此。


```
function h() public returns( bool, bytes memory){
    address a =address( 0x1);
    bytes memory ss = new bytes(128) ;

    bytes32 msgHash = hex"1c8aff950685c2ed4bc3174f3472287b56d9517b9c948127319a09a7a36deac8";
    bytes32 s = hex"e419c9da6ff9f3877eaef35fad097873615d95d3d0200300f70927616d5531c1";
    bytes32 v = hex"0d225cf7d261b3f5445da9afa8b48d9f75cde891998d48c19ede884d508fe47a";

    for(uint8 i = 0; i<32; i++){
        ss[i]=msgHash[i];
    }
    for(uint8 i = 0; i<32; i++){
        ss[64+i]=s[i];
    }
    for(uint8 i = 0; i<32; i++){
        ss[96+i]=v[i];
        }
    ss[63]=byte(uint8(27));
    return a.call(ss);
}

function h1() public returns(address){
    bytes32 msgHash = hex"1c8aff950685c2ed4bc3174f3472287b56d9517b9c948127319a09a7a36deac8";
    bytes32 s = hex"e419c9da6ff9f3877eaef35fad097873615d95d3d0200300f70927616d5531c1";
    bytes32 v = hex"0d225cf7d261b3f5445da9afa8b48d9f75cde891998d48c19ede884d508fe47a";

    return ecrecover(msgHash,uint8(27), s,v );
}
```


