---
title: 結果の処理 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fdc66899f7d863cbfb3ae04ad0796614717a734
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209663"
---
# <a name="processing-results"></a>結果の処理
  コマンドの実行、またはプロバイダーからの行セット オブジェクトの直接生成のいずれかによって行セット オブジェクトを作成する場合、コンシューマーはその行セット内のデータにアクセスして、データを取得する必要があります。  
  
 行セットは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーが表形式でデータを公開できるようにするための重要な機能を持つオブジェクトです。 概念的には、行セットは行の集まりを表し、各行には列データが格納されています。 行セット オブジェクトでは、**IRowset** (行セットから順番に行をフェッチするメソッドを含みます)、**IAccessor** (コンシューマーのプログラム変数に表形式のデータをバインドする方法を指定する一連の列バインドの定義を許可します)、**IColumnsInfo** (行セット内の列に関する情報を提供します)、**IRowsetInfo** (行セットに関する情報を提供します) などのインターフェイスが公開されます。  
  
 コンシューマーは、**IRowset::GetData** メソッドを呼び出して、データ行を行セットからバッファーに取得できます。 **GetData** を呼び出す前に、DBBINDING 構造体のセットを使用してバッファーを記述します。 各バインドは、行セット内の列をコンシューマーのバッファーに格納する方法を記述するもので、次の情報が含まれます。  
  
-   バインドが適用される列 (パラメーター) の序数  
  
-   バインドされる内容 (データ値、データの長さ、バインドの状態など) に関する情報  
  
-   バッファー内の各部分へのオフセットに関する情報  
  
-   コンシューマーのバッファー内でのデータ値の長さと型  
  
 プロバイダーはデータを取得するときに、各バインドの情報を使用してコンシューマーのバッファーからデータを取得する位置と方法を決定します。 また、コンシューマーのバッファーにデータを設定するときに、各バインドの情報を使用してコンシューマーのバッファー内にあるデータを返す位置と方法を決定します。  
  
 DBBINDING 構造体を指定したら、アクセサーを作成 (**IAccessor::CreateAccessor**) します。 バインドの集まりであるアクセサーは、コンシューマーのバッファー内のデータを取得または設定するときに使用します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client OLE DB プロバイダー アプリケーションの作成](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [OLE DB の使用法に関するトピック](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
