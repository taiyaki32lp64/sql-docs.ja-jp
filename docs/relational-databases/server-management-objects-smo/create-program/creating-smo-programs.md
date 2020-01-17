---
title: SMO プログラムの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b55c30746542a09a84f4b8eacde8e78f3dae8ed
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148747"
---
# <a name="creating-smo-programs"></a>SMO プログラムの作成
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) オブジェクトの一般的なプログラミングには、メソッドの実行、プロパティの設定、およびコレクションの操作など、すべてのオブジェクトが共有する共通エリアが含まれています。  
  
|トピック|説明|  
|-----------|-----------------|  
|[SQL Server のインスタンスへの接続](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスへの接続を確立する最も基本的な SMO プログラム。 Windows 認証および [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を示します。 また、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のローカル インスタンスおよびリモート インスタンスへの接続を示すサンプルも含まれています。|  
|[SQL Server のインスタンスからの切断](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスから切断する方法を示すプログラム。|  
|[メソッドの呼び出し](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|このセクションでは、メソッドを呼び出すための一般的な方法について説明します。 パラメーターの使用、および <xref:System.Data.DataTable> オブジェクトに返されるデータのテーブルを処理する方法について説明します。 また、オブジェクトコンストラクターを呼び出す方法と**Clone**メソッドを呼び出す方法の例も含まれています。|  
|[プロパティの設定 - SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|このセクションでは、プロパティのさまざまな型を設定する方法について説明します。 オブジェクト プロパティを設定および取得する方法について示します。 また、オブジェクトの作成時にオブジェクト プロパティを設定する例、およびオブジェクトのすべてのプロパティを反復処理する方法も含まれています。|  
|[コレクションの使用](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|オブジェクト コレクションと共に使用されるテクニックについて説明するさまざまなプログラム。 コレクションを使用するオブジェクトを参照する方法について説明します。 また、コレクションのメンバーを反復処理する方法の例も含まれています。|  
|[SMO イベントの処理](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|このセクションでは、SMO でイベントの設定および処理を行う方法について説明します。 イベント ハンドラーを設定する方法、およびイベント サブスクリプションを設定する方法の例が含まれています。|  
|[SMO 例外の処理](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|このセクションでは、SMO で例外をトラップする方法について説明します。 例外をキャッチする方法、および内部例外を表示する方法の例が含まれています。|  
|[データ型の処理](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|このセクションでは、さまざまな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型を操作する方法について説明します。 オブジェクト コンストラクターでの指定でデータ型を構築する方法について説明します。 また、既定のコンストラクターを使用してデータ型を作成する方法の例も含まれています。|  
|[トランザクションの使用](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|このセクションでは、SMO プログラムでトランザクション処理を実装する方法について説明します。 SMO プログラムでトランザクションを使用する方法の例が含まれています。|  
|[キャプチャ モードの使用](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|このセクションでは、SMO プログラムの出力を記録する方法について説明します。 この例では、後で実行するために [!INCLUDE[tsql](../../../includes/tsql-md.md)] のインスタンスに送信された [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ステートメントとして、SMO プログラムが記録されます。|  
  
  
