---
title: SQL Server カーソルでデータを更新します。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5c0b188d8fd45c1177cab77501bdf80fc550987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63242922"
---
# <a name="updating-data-in-sql-server-cursors"></a>SQL Server カーソルでのデータ更新
  フェッチとを使用してデータを更新するとき[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]カールでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーのコンシューマー アプリケーションが同じ考慮事項とその他のクライアント アプリケーションに適用される制約をバインドします。  
  
 同時実行データアクセス制御に関係するのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カーソル内の行だけです。 コンシューマーから変更可能な行セットが要求されるときは、コンカレンシー制御が DBPROP_LOCKMODE によって制御されます。 同時実行アクセス制御のレベルを変更するには、コンシューマーで行セットを開く前に DBPROP_LOCKMODE プロパティを設定します。  
  
 クライアント アプリケーションのデザインにより、トランザクションが長時間開かれたままの状態になる場合、トランザクション分離レベルが原因で行の位置指定が大幅に遅れる可能性があります。 既定で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、DBPROPVAL_TI_READCOMMITTED によって指定される read committed 分離レベルを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーは、行セットの同時実行が読み取り専用にすると、ダーティ リード分離をサポートしています。 そのため、コンシューマーは変更可能な行セットで、より高い分離レベルを要求できますが、より低い分離レベルは要求できません。  
  
## <a name="immediate-and-delayed-update-modes"></a>即時更新モードと遅延更新モード  
 即時更新モードでは、**IRowsetChange::SetData** を呼び出すたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との間にラウンドトリップが発生します。 コンシューマーが 1 つの行に複数の変更を加える場合は、**SetData** を 1 回呼び出してすべての変更を実行する方が効率が高くなります。  
  
 遅延更新モードでは、**IRowsetUpdate::Update** の *cRows* パラメーターと *rghRows* パラメーターに示される行ごとに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との間にラウンドトリップが発生します。  
  
 どちらのモードでも、行セットに対してトランザクション オブジェクトが開いていないときは、1 つのラウンドトリップが個別のトランザクションを表します。  
  
 使用する場合は**IRowsetUpdate::Update**、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーは指定された各行を処理しようとしています。 任意の行で停止しないために、無効なデータ、長さ、またはステータスの値があるため発生しているエラー[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーを処理します。 更新に関係する他のすべての行が変更されることも、そのような行がまったく変更されないこともあります。 コンシューマーは、返された調べる必要があります*prgRowStatus*配列は、特定のエラーを確認するときに行、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは DB_S_ERRORSOCCURRED を返します。  
  
 コンシューマーでは、特定の順序で行が処理されることを想定しないでください。 1 行以上の行に対してデータ変更を順序付けて処理することが必要な場合、アプリケーション ロジックで順序を確立し、トランザクションを開いてそのロジックをトランザクション内に含める必要があります。  
  
## <a name="see-also"></a>参照  
 [行セット内のデータの更新](updating-data-in-rowsets.md)  
  
  
