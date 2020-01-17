---
title: テーブル値パラメーターの行セットの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 11acec127d354688aa81e8e50006c0b80c14347d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761649"
---
# <a name="table-valued-parameter-rowset-creation"></a>テーブル値パラメーターの行セットの作成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  コンシューマーはテーブル値パラメーターに任意の行セット オブジェクトを使用できますが、通常の行セット オブジェクトはバックエンドのデータ ストアに対して実装されるため、パフォーマンスが制限されます。 このため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、コンシューマーがメモリ内データの上位に特殊な行セット オブジェクトを作成できます。 この特別なメモリ内の行セットオブジェクトは、テーブル値パラメーターの行セットと呼ばれる新しい COM オブジェクトです。 このオブジェクトには、パラメーター セットと同様の機能が用意されています。  
  
 テーブル値パラメーターの行セット オブジェクトは、コンシューマーが、複数のセッション レベルのインターフェイスを使用して、入力パラメーターに対して明示的に作成します。 テーブル値パラメーターの行セット オブジェクトは、テーブル値パラメーターごとに 1 つのインスタンスがあります。 コンシューマーは、既知のメタデータ情報を指定するか (静的なシナリオ)、プロバイダー インターフェイスを使用してメタデータ情報を検出する (動的なシナリオ) ことにより、テーブル値パラメーターの行セット オブジェクトを作成できます。 この後の各セクションで、これらの 2 つのシナリオについて説明します。  
  
## <a name="static-scenario"></a>静的なシナリオ  
 型情報がわかっている場合、コンシューマーは ITableDefinitionWithConstraints:: CreateTableWithConstraints を使用して、テーブル値パラメーターに対応するテーブル値パラメーターの行セットオブジェクトをインスタンス化します。  
  
 *Guid*フィールド (*ptableid*パラメーター) には、特別な guid (CLSID_ROWSET_TVP) が含まれています。 *pwszName* メンバーには、コンシューマーがインスタンスを作成するテーブル値パラメーターの型の名前を含めます。 *eKind* フィールドは、DBKIND_GUID_NAME に設定されます。 この名前は、ステートメントがアドホック SQL の場合に必要です。プロシージャ呼び出しの場合、名前は省略可能です。  
  
 集計の場合、コンシューマーは制御 IUnknown に*pUnkOuter*パラメーターを渡します。  
  
 テーブル値パラメーターの行セットオブジェクトのプロパティは読み取り専用であるため、コンシューマーは*rgPropertySets*のプロパティを設定する必要はありません。  
  
 各 DBCOLUMNDESC 構造体の *rgPropertySets* メンバーの場合、コンシューマーは列ごとに追加のプロパティを指定できます。 これらのプロパティは、DBPROPSET_SQLSERVERCOLUMN プロパティ セットに属しています。 これらのプロパティによって、列ごとに計算の設定と既定の設定を指定できます。 また、NULL 値の許容や ID など、列の既存のプロパティもサポートされます。  
  
 コンシューマーでは、テーブル値パラメーターの行セット オブジェクトから対応する情報を取得するために、IRowsetInfo::GetProperties を使用します。  
  
 各列の null、一意、計算、および更新の各状態に関する情報を取得するには、コンシューマーが IColumnsRowset:: GetColumnsRowset または IColumnsInfo:: GetColumnInfo を使用します。 これらのメソッドでは、各テーブル値パラメーターの行セットの列に関する詳細情報が取得できます。  
  
 コンシューマーは、テーブル値パラメーターの列ごとに型を指定します。 この方法は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテーブルを作成する際に列を指定する方法と似ています。 コンシューマーは、 *ppRowset* output パラメーターを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーからテーブル値パラメーターの行セットオブジェクトを取得します。  
  
## <a name="dynamic-scenario"></a>動的なシナリオ  
 コンシューマーが型情報を持っていない場合は、IOpenRowset:: OpenRowset を使用してテーブル値パラメーターの行セットオブジェクトをインスタンス化する必要があります。 すべてのコンシューマーは、プロバイダーに型名を知らせる必要があります。  
  
 このシナリオでは、プロバイダーがコンシューマーに代わって、テーブル値パラメーターの行セット オブジェクトに関する型情報をサーバーから取得します。  
  
 *Ptableid*パラメーターと*pUnkOuter*パラメーターは、静的なシナリオのように設定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、サーバーから型情報 (列情報と制約) を取得し、 *ppRowset*パラメーターを使用してテーブル値パラメーターの行セットオブジェクトを返します。 この操作にはサーバーとの通信が必要であるため、静的なシナリオと同様に実行されません。 動的なシナリオは、パラメーター化されたプロシージャ呼び出しでのみ動作します。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
