---
title: テーブル値パラメーター行セットの作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de130ef821551383ada1a6df3574404cd3518e88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046517"
---
# <a name="table-valued-parameter-rowset-creation"></a>テーブル値パラメーターの行セットの作成
  コンシューマーはテーブル値パラメーターに任意の行セット オブジェクトを使用できますが、通常の行セット オブジェクトはバックエンドのデータ ストアに対して実装されるため、パフォーマンスが制限されます。 このため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーでは、コンシューマーがメモリ内データの上位に特殊な行セット オブジェクトを作成できます。 この特別なメモリ内の行セット オブジェクトは、テーブル値パラメーター行セットと呼ばれる新しい COM オブジェクトです。 このオブジェクトには、パラメーター セットと同様の機能が用意されています。  
  
 テーブル値パラメーターの行セット オブジェクトは、コンシューマーが、複数のセッション レベルのインターフェイスを使用して、入力パラメーターに対して明示的に作成します。 テーブル値パラメーターの行セット オブジェクトは、テーブル値パラメーターごとに 1 つのインスタンスがあります。 コンシューマーは、既知のメタデータ情報を指定するか (静的なシナリオ)、プロバイダー インターフェイスを使用してメタデータ情報を検出する (動的なシナリオ) ことにより、テーブル値パラメーターの行セット オブジェクトを作成できます。 この後の各セクションで、これらの 2 つのシナリオについて説明します。  
  
## <a name="static-scenario"></a>静的なシナリオ  
 型情報がわかっている場合、コンシューマーは、テーブル値パラメーターに対応するテーブル値パラメーター行セット オブジェクトをインスタンス化するのに ITableDefinitionWithConstraints::CreateTableWithConstraints を使用します。  
  
 *Guid*フィールド (*pTableID*パラメーター) 特殊な GUID (CLSID_ROWSET_TVP) が含まれています。 *pwszName* メンバーには、コンシューマーがインスタンスを作成するテーブル値パラメーターの型の名前を含めます。 *eKind* フィールドは、DBKIND_GUID_NAME に設定されます。 この名前は、ステートメントがアドホック SQL の場合に必要です。プロシージャ呼び出しの場合、名前は省略可能です。  
  
 コンシューマーでは、集計、 *pUnkOuter* controlling IUnknown のパラメーター。  
  
 テーブル値パラメーター行セット オブジェクトのプロパティは読み取り専用に、コンシューマーは、プロパティを設定する必要はありません*rgPropertySets*します。  
  
 各 DBCOLUMNDESC 構造体の *rgPropertySets* メンバーの場合、コンシューマーは列ごとに追加のプロパティを指定できます。 これらのプロパティは、DBPROPSET_SQLSERVERCOLUMN プロパティ セットに属しています。 これらのプロパティによって、列ごとに計算の設定と既定の設定を指定できます。 また、NULL 値の許容や ID など、列の既存のプロパティもサポートされます。  
  
 コンシューマーでは、テーブル値パラメーターの行セット オブジェクトから対応する情報を取得するために、IRowsetInfo::GetProperties を使用します。  
  
 計算するには、null、一意、に関する情報を取得し、各列のステータスの更新、コンシューマーは、icolumnsrowset::getcolumnsrowset または icolumnsinfo::getcolumninfo を使用します。 これらのメソッドでは、各テーブル値パラメーターの行セットの列に関する詳細情報が取得できます。  
  
 コンシューマーは、テーブル値パラメーターの列ごとに型を指定します。 この方法は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でテーブルを作成する際に列を指定する方法と似ています。 コンシューマーからテーブル値パラメーター行セット オブジェクトを取得する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーを介して、 *ppRowset*出力パラメーター。  
  
## <a name="dynamic-scenario"></a>動的なシナリオ  
 コンシューマーが型情報を持っていない場合に、テーブル値パラメーター行セット オブジェクトをインスタンス化するのに iopenrowset::openrowset を使用してください。 すべてのコンシューマーは、プロバイダーに型名を知らせる必要があります。  
  
 このシナリオでは、プロバイダーがコンシューマーに代わって、テーブル値パラメーターの行セット オブジェクトに関する型情報をサーバーから取得します。  
  
 *PTableID*と*pUnkOuter*パラメーターは、静的なシナリオのように設定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、サーバーから型情報 (列情報と制約) を取得しをテーブル値パラメーター行セット オブジェクトを返す、 *ppRowset*パラメーター。 この操作は、サーバーとの通信が必要ですし、そのため、静的なシナリオとは実行されません。 動的なシナリオは、パラメーター化されたプロシージャ呼び出しでのみ動作します。  
  
## <a name="see-also"></a>参照  
 [テーブル値パラメーター &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [テーブル値パラメーターの使用 &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
