---
title: 結果の処理 |Microsoft Docs
description: 結果の処理
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 9d29e75f75332f207c64a7b502e60300e9aae3d5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994974"
---
# <a name="processing-results"></a>結果の処理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  コマンドの実行、またはプロバイダーからの行セット オブジェクトの直接生成のいずれかによって行セット オブジェクトを作成する場合、コンシューマーはその行セット内のデータにアクセスして、データを取得する必要があります。  
  
 行セットは、SQL Server の OLE DB ドライバーが表形式でデータを公開できるようにする中心的なオブジェクトです。 概念的には、行セットは行の集まりを表し、各行には列データが格納されています。 行セット オブジェクトでは、**IRowset** (行セットから順番に行をフェッチするメソッドを含みます)、**IAccessor** (コンシューマーのプログラム変数に表形式のデータをバインドする方法を指定する一連の列バインドの定義を許可します)、**IColumnsInfo** (行セット内の列に関する情報を提供します)、**IRowsetInfo** (行セットに関する情報を提供します) などのインターフェイスが公開されます。  
  
 コンシューマーは、**IRowset::GetData** メソッドを呼び出して、データ行を行セットからバッファーに取得できます。 **GetData** を呼び出す前に、DBBINDING 構造体のセットを使用してバッファーを記述します。 各バインドは、行セット内の列をコンシューマーのバッファーに格納する方法を記述するもので、次の情報が含まれます。  
  
-   バインドが適用される列 (パラメーター) の序数  
  
-   バインドされる内容 (データ値、データの長さ、バインドの状態など) に関する情報  
  
-   バッファー内の各部分へのオフセットに関する情報  
  
-   コンシューマーのバッファー内でのデータ値の長さと型  
  
 プロバイダーはデータを取得するときに、各バインドの情報を使用してコンシューマーのバッファーからデータを取得する位置と方法を決定します。 また、コンシューマーのバッファーにデータを設定するときに、各バインドの情報を使用してコンシューマーのバッファー内にあるデータを返す位置と方法を決定します。  
  
 DBBINDING 構造体を指定したら、アクセサーを作成 (**IAccessor::CreateAccessor**) します。 バインドの集まりであるアクセサーは、コンシューマーのバッファー内のデータを取得または設定するときに使用します。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のアプリケーションの作成](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [OLE DB の使用法に関するトピック](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
