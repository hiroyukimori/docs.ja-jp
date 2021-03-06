---
title: "&lt;peerTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1a5013a-9dd4-4a27-b114-795b8b323177
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# &lt;peerTransport&gt;
カスタム バインディングのピア トランスポートを定義します。  
  
## 構文  
  
```  
  
<peerTransport   
    listenIpAddress="String"  
    maxBufferPoolSize="Integer"  
    maxReceivedMessageSize="Integer"  
    port="Integer"  
        <security>  
    </security>  
/>  
```  
  
## 属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### 属性  
  
|属性|説明|  
|--------|--------|  
|listenIpAddress|ピア ノードが TCP メッセージをリッスンする IP アドレスを指定する文字列です。  既定値は、`null` です。|  
|maxBufferPoolSize|バッファー プールの最大サイズを指定する正の整数です。  既定値は 524288 です。<br /><br /> WCF の多くの部分でバッファーが使用されます。  使用するたびに毎回バッファーを作成および破壊すると負荷が高くなります。バッファーのガベージ コレクションも同様です。  バッファー プールを使用すると、バッファーをプールから取得して使用し、作業が終わったらプールに戻すことができます。  これで、バッファーの作成と破棄のオーバーヘッドを回避できます。|  
|maxReceivedMessageSize|ヘッダーなどのメッセージの最大サイズ \(バイト単位\) を定義する正の整数。  受信側にとってメッセージが大きすぎると、メッセージの送信側は SOAP エラーを受け取ります。  メッセージは受信者によって破棄され、トレース ログにこのイベントのエントリが作成されます。  既定値は 65536 です。|  
|ポート|このバインディングがピア チャネルの TCP メッセージを処理するネットワーク インターフェイス ポートを指定する整数です。  この値の有効値の範囲は <xref:System.Net.IPEndPoint.MinPort> ～ <xref:System.Net.IPEndPoint.MaxPort> です。  既定値は 0 です。|  
  
### 子要素  
  
|要素|説明|  
|--------|--------|  
|[\<security\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-peertransport.md)|このトランスポートのセキュリティ設定を定義します。  この要素は <xref:System.ServiceModel.Configuration.PeerSecurityElement> 型です。|  
  
### 親要素  
  
|要素|説明|  
|--------|--------|  
|[\<binding\>](../../../../../docs/framework/misc/binding.md)|カスタム バインドのすべてのバインド機能を定義します。|  
  
## 解説  
 このトランスポートは、要求\/応答操作を含むコントラクトと共に使用することはできません。  
  
## 参照  
 <xref:System.ServiceModel.Configuration.PeerTransportElement>   
 <xref:System.ServiceModel.Channels.PeerTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [トランスポート](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [トランスポートの選択](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [バインディング](../../../../../docs/framework/wcf/bindings.md)   
 [バインディングの拡張](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [カスタム バインディング](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)