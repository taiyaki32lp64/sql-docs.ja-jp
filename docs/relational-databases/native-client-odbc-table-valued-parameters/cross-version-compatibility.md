---
title: バージョン間の互換性 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 196c99bebaf0255f095055bef6c9c6a64c41908b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73776279"
---
# <a name="cross-version-compatibility"></a>複数バージョン間の互換性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  バージョン間の競合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] より前のバージョンの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のクライアント インスタンスまたはサーバー インスタンスでテーブル値パラメーターを処理する必要がある場合に発生することがあります。  
  
 一般に、テーブル値パラメーターの機能を使用できるのは、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (以降) のサーバーに接続されている [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のクライアント (SQL Server Native Client 10.0 を使用) だけです。 カタログ関数の結果セットの新しい列は、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (またはそれ以降) のサーバーに接続されている場合にのみ存在します。  
  
 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でコンパイルされたクライアント アプリケーションで、テーブル値パラメーターが必要なステートメントを実行すると、サーバーではデータ変換エラーからこの状態が検出され、ODBC によって、これが "データ型の属性に関する制限に違反しました" というメッセージの SQLSTATE 07006 として返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 以降を使用してコンパイルされたクライアントアプリケーションが [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]より前のサーバーインスタンスに接続したときにテーブル値パラメーターを使用しようとした場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client はこれを検出し、SQLBindCol、SQLBindParameter、SQLSetDescFields と SQLSetDescRec の呼び出しは、SQLSTATE 07006 で失敗し、"データ型の属性が制限されています (この接続のバージョン SQL Server はテーブル値パラメーターをサポートしていません)" というメッセージが表示されます。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;の ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
