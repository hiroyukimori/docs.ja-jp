---
title: "CacheMetadata を使用したデータの公開 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# CacheMetadata を使用したデータの公開
アクティビティを実行する前に、ワークフロー ランタイムは実行を維持するために必要なアクティビティに関するすべての情報を取得します。ワークフロー ランタイムは <xref:System.Activities.Activity.CacheMetadata%2A> メソッドの実行時にこの情報を取得します。このメソッドの既定の実装は、アクティビティによって公開されたすべてのパブリック引数、変数、子アクティビティを実行時にランタイムに提供します。アクティビティがランタイムにその他の情報 \(プライベート メンバーやアクティビティによってスケジュールされるアクティビティなど\) を提供する必要がある場合、このメソッドをオーバーライドして情報を提供できます。  
  
## CacheMetadata の既定の動作  
 <xref:System.Activities.NativeActivity> から派生したアクティビティの <xref:System.Activities.NativeActivity.CacheMetadata%2A> の既定の実装は、次のメソッド型を以下の方法で処理します。  
  
-   <xref:System.Activities.InArgument%601>、<xref:System.Activities.OutArgument%601>、または <xref:System.Activities.InOutArgument%601> \(ジェネリック引数\): これらの引数は公開されたプロパティと同じ名前、データ型、引数の方向、および検証データで引数としてランタイムに公開されます。  
  
-   <xref:System.Activities.Variable> またはそのサブクラス: これらのメンバーはパブリック変数としてランタイムに公開されます。  
  
-   <xref:System.Activities.Activity> またはそのサブクラス: これらのメンバーはパブリック子アクティビティとしてランタイムに公開されます。既定の動作を明示的に実装するには、子アクティビティを渡して <xref:System.Activities.ActivityMetadata.AddImportedChild%2A> を呼び出します。  
  
-   <xref:System.Activities.ActivityDelegate> またはそのサブクラス: これらのメンバーはパブリック デリゲートとしてランタイムに公開されます。  
  
-   <xref:System.Activities.Variable> 型の <xref:System.Collections.ICollection>: コレクション内のすべての要素がパブリック変数としてランタイムに公開されます。  
  
-   <xref:System.Activities.Activity> 型の <xref:System.Collections.ICollection>: コレクション内のすべての要素がパブリック子としてランタイムに公開されます。  
  
-   <xref:System.Activities.ActivityDelegate> 型の <xref:System.Collections.ICollection>: コレクション内のすべての要素がパブリック デリゲートとしてランタイムに公開されます。  
  
 <xref:System.Activities.Activity>、<xref:System.Workflow.Activities.CodeActivity>、および <xref:System.Activities.AsyncCodeActivity> から派生したアクティビティの <xref:System.Activities.Activity.CacheMetadata%2A> も次の相違点を除いて前述と同様に機能します。  
  
-   <xref:System.Activities.Activity> から派生したクラスは子アクティビティまたはデリゲートをスケジュールできないため、これらのメンバーはインポートされた子およびデリゲートとして公開されます。  
  
-   <xref:System.Activities.CodeActivity> および <xref:System.Activities.AsyncCodeActivity> から派生したクラスは変数、子、またはデリゲートをサポートしないため、引数のみが公開されます。  
  
## CacheMetadata をオーバーライドしてランタイムに情報を提供する  
 次のコード スニペットは、<xref:System.Activities.Activity.CacheMetadata%2A> メソッドの実行時にメンバーに関する情報をアクティビティのメタデータに追加する方法を示しています。メソッドの base を呼び出して、アクティビティに関するすべてのパブリック データをキャッシュしています。  
  
```  
protected override void CacheMetadata(NativeActivityMetadata metadata)  
{      
    base.CacheMetadata(metadata);  
    metadata.AddImplementationChild(this._writeLine);  
    metadata.AddVariable(this._myVariable);  
    metadata.AddImplementationVariable(this._myImplementationVariable);  
  
    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));  
    metadata.Bind(argument, this.SomeName);  
    metadata.AddArgument(argument);  
}  
  
```  
  
## CacheMetadata を使用して実装の子を公開する  
 アクティビティによってスケジュールされる子アクティビティに変数を使用してデータを渡すには、変数を実装変数として追加する必要があります。パブリック変数ではこの方法で値を設定することはできません。その理由は、アクティビティはカプセル化されたクラス \(プロパティを持つ\) としてよりも、関数 \(パラメーターを持つ\) の実装として実行することを目的としているためです。ただし、場合によっては引数を明示的に設定する必要があります。たとえば、スケジュールされたアクティビティは親アクティビティの引数に子アクティビティと同じ方法でアクセスすることはできないため、<xref:System.Activities.NativeActivityContext.ScheduleActivity%2A> を使用する場合には引数の明示的な設定が必要です。  
  
 次のコード スニペットは、<xref:System.Activities.Activity.CacheMetadata%2A> を使用してネイティブ アクティビティからスケジュールされたアクティビティに引数を渡す方法を示しています。  
  
```  
public sealed class ChildActivity : NativeActivity  
{  
    public WriteLine _writeLine;  
    public InArgument<string> Message { get; set; }  
    private Variable<string> MessageVariable { get; set; }  
    public ChildActivity()  
    {  
        MessageVariable = new Variable<string>();  
        _writeLine = new WriteLine  
        {  
            Text = new InArgument<string>(MessageVariable),  
        };  
    }  
    protected override void CacheMetadata(NativeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        metadata.AddImplementationVariable(this.MessageVariable);  
        metadata.AddImplementationChild(this._writeLine);  
    }  
    protected override void Execute(NativeActivityContext context)  
    {  
        string configuredMessage = context.GetValue(Message);  
        context.SetValue(MessageVariable, configuredMessage);  
        context.ScheduleActivity(this._writeLine);  
    }  
}  
  
```