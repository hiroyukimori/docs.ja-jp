---
title: "トランザクション キュー | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b1b011dd-5e0b-482c-9bb0-9d8727038f14
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# トランザクション キュー
このサンプルでは、キューとトランザクションを [!INCLUDE[wf](../../../../includes/wf-md.md)] に統合し、信頼性があり、拡張性の高いサービスを作成する方法を示します。<xref:System.Activities.TransactionScope> は、<xref:System.ServiceModel.NetMsmqBinding> を使用してトランザクション内でキューにメッセージを送信するためにクライアント ワークフローで使用されます。<xref:System.ServiceModel.Activities.TransactedReceiveScope> は、キューからメッセージを受信して同じトランザクション内でワークフローの状態を更新するためにサーバーで使用されます。  
  
## 使用例  
 <xref:System.Activities.Statements.TransactionScope>、<xref:System.ServiceModel.Activities.TransactedReceiveScope>、<xref:System.ServiceModel.NetMsmqBinding>、<xref:System.ServiceModel.Activities.Receive>、およびコンテンツ ベースの相関関係。  
  
## 説明  
 このサンプルで取り上げる機能について説明するために、特定のアカウント用に取得されて使用されるポイントを追跡する `RewardsPoints` ワークフロー サービスが作成されます。クライアントは、<xref:System.Activities.WorkflowInvoker> を使用してキューへのさまざまな要求の送信をシミュレートします。トランザクション内でキューにメッセージを送信するために、<xref:System.ServiceModel.Activities.Send> アクティビティを <xref:System.Activities.Statements.TransactionScope> の <xref:System.Activities.Statements.TransactionScope.Body%2A> 内に配置できます。このサンプルでは、キューに置かれたメッセージがクライアント アプリケーションとサーバー アプリケーションを切り離す方法について説明するために、最初にクライアントが実行され、次にサーバーが実行されます。  
  
 クライアントが完了したら、サービスが構成されてホストされます。サービスが開くとすぐに、既にキューに置かれているメッセージの処理が開始されます。各メッセージが同じサーバー トランザクション内で受信および処理されます。このサンプルでは、最初に受信するメッセージは、要求メッセージの一部として渡されるアカウント名に基づいてインスタンスを作成してコンテンツ ベースの相関関係を初期化する `CreateAccount` 要求です。実際に必要となる可能性のある種類のサービスをモデル化するために、`AddPoints` メッセージと `UsePoints` メッセージを処理する次の 2 つの <xref:System.ServiceModel.Activities.TransactedReceiveScope> アクティビティが `while` ループ内の並行分岐に配置されており、これらのメッセージを任意の順序で繰り返し処理できるようになっています。  
  
 <xref:System.Activities.Statements.TransactionScope> および <xref:System.ServiceModel.Activities.TransactedReceiveScope> は、それぞれスコープの末尾に暗黙的な永続化ポイントを持つので、これらのアクティビティをキューと組み合わせて [!INCLUDE[wf1](../../../../includes/wf1-md.md)] で使用すると、メッセージが失われないようにしながら、ワークフローを一貫性のある状態から次の一貫性のある状態に確実に移行できます。  
  
#### サンプルを設定、ビルド、および実行するには  
  
1.  MSMQ をインストールして構成します。詳細については、「[メッセージ キュー \(MSMQ\) のインストール](http://go.microsoft.com/fwlink/?LinkId=178526)」を参照してください。  
  
2.  コマンド ラインで次のコマンドを実行して、MSDTC を確実に実行します。`net start msdtc`  
  
3.  プロジェクトをコンパイルして実行可能ファイルを開くか、[!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] でプロジェクトを開いてデバッグ メニューから開始オプションを選択します。最初にキューが作成され、次にクライアントが実行されてキューにメッセージが送信され、最後にサービスが開始されてメッセージが処理されます。プログラムを終了するには、Enter キーを押します。  
  
> [!IMPORTANT]
>  サンプルは、既にコンピューターにインストールされている場合があります。続行する前に、次の \(既定の\) ディレクトリを確認してください。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  このディレクトリが存在しない場合は、「[.NET Framework 4 向けの Windows Communication Foundation \(WCF\) および Windows Workflow Foundation \(WF\) のサンプル](http://go.microsoft.com/fwlink/?LinkId=150780)」にアクセスして、[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] および [!INCLUDE[wf1](../../../../includes/wf1-md.md)] のサンプルをすべてダウンロードしてください。このサンプルは、次のディレクトリに格納されます。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Transactions\TransactedQueues`