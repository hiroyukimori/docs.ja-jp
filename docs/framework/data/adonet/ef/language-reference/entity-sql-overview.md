---
title: "Entity SQL の概要 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: f0bb8120-e709-40a3-ac1e-5520dc47477d
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Entity SQL の概要
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] は、[!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] 内の概念モデルに対するクエリの実行に使用できる SQL に似た言語です。  概念モデルは、データをエンティティおよびリレーションシップとして表します。[!INCLUDE[esql](../../../../../../includes/esql-md.md)] を使用すると、SQL を使用したことのあるユーザーが慣れている形式でそれらのエンティティおよびリレーションシップに対してクエリを実行できます。  
  
 [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] は、ストレージ固有のデータ プロバイダーと連携し、汎用的な [!INCLUDE[esql](../../../../../../includes/esql-md.md)] をストレージ固有のクエリに変換します。  EntityClient プロバイダーには、エンティティ モデルに対して [!INCLUDE[esql](../../../../../../includes/esql-md.md)] コマンドを実行し、スカラー結果、結果セット、オブジェクト グラフなど、さまざまなデータ型を返すための手段が用意されています。  <xref:System.Data.EntityClient.EntityCommand> オブジェクトを構築する場合は、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] のクエリ文字列を <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=fullName> プロパティに割り当てることで、ストアド プロシージャの名前またはクエリのテキストを指定できます。  EDM に対する <xref:System.Data.EntityClient.EntityCommand> の実行結果は、<xref:System.Data.EntityClient.EntityDataReader> によって公開されます。  <xref:System.Data.EntityClient.EntityDataReader> を返すコマンドを実行するには、<xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A> を呼び出します。  
  
 EntityClient プロバイダーだけでなく [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] でも、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] を使用して概念モデルに対するクエリを実行し、エンティティ型のインスタンスである厳密に型指定された CLR オブジェクトとしてデータを返すことができます。  詳細については、「[オブジェクトの使用](../../../../../../docs/framework/data/adonet/ef/working-with-objects.md)」を参照してください。  
  
 ここでは、[!INCLUDE[esql](../../../../../../includes/esql-md.md)] の概念について説明します。  
  
## このセクションの内容  
 [Entity SQL と Transact\-SQL の相違点](../../../../../../docs/framework/data/adonet/ef/language-reference/how-entity-sql-differs-from-transact-sql.md)  
  
 [Entity SQL クイック リファレンス](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-quick-reference.md)  
  
 [型システム](../../../../../../docs/framework/data/adonet/ef/language-reference/type-system-entity-sql.md)  
  
 [型定義](../../../../../../docs/framework/data/adonet/ef/language-reference/type-definitions-entity-sql.md)  
  
 [コンストラクター](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md)  
  
 [クエリ プランのキャッシュ](../../../../../../docs/framework/data/adonet/ef/language-reference/query-plan-caching-entity-sql.md)  
  
 [名前空間](../../../../../../docs/framework/data/adonet/ef/language-reference/namespaces-entity-sql.md)  
  
 [識別子](../../../../../../docs/framework/data/adonet/ef/language-reference/identifiers-entity-sql.md)  
  
 [パラメーター](../../../../../../docs/framework/data/adonet/ef/language-reference/parameters-entity-sql.md)  
  
 [変数](../../../../../../docs/framework/data/adonet/ef/language-reference/variables-entity-sql.md)  
  
 [サポートされていない式](../../../../../../docs/framework/data/adonet/ef/language-reference/unsupported-expressions-entity-sql.md)  
  
 [リテラル](../../../../../../docs/framework/data/adonet/ef/language-reference/literals-entity-sql.md)  
  
 [NULL リテラルと型推論](../../../../../../docs/framework/data/adonet/ef/language-reference/null-literals-and-type-inference-entity-sql.md)  
  
 [入力文字セット](../../../../../../docs/framework/data/adonet/ef/language-reference/input-character-set-entity-sql.md)  
  
 [クエリ式](../../../../../../docs/framework/data/adonet/ef/language-reference/query-expressions-entity-sql.md)  
  
 [関数](../../../../../../docs/framework/data/adonet/ef/language-reference/functions-entity-sql.md)  
  
 [演算子の優先順位](../../../../../../docs/framework/data/adonet/ef/language-reference/operator-precedence-entity-sql.md)  
  
 [ページング](../../../../../../docs/framework/data/adonet/ef/language-reference/paging-entity-sql.md)  
  
 [比較セマンティクス](../../../../../../docs/framework/data/adonet/ef/language-reference/comparison-semantics-entity-sql.md)  
  
 [入れ子になった Entity SQL クエリの作成](../../../../../../docs/framework/data/adonet/ef/language-reference/composing-nested-entity-sql-queries.md)  
  
 [NULL 値が許容される構造化型](../../../../../../docs/framework/data/adonet/ef/language-reference/nullable-structured-types-entity-sql.md)  
  
## 参照  
 [Entity SQL リファレンス](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Entity SQL 言語](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)   
 [CSDL、SSDL、および MSL 仕様](../../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)