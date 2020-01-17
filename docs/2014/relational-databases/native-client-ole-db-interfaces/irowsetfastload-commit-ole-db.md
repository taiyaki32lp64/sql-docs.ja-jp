---
title: IRowsetFastLoad::Commit (OLE DB)。マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- IRowsetFastLoad::Commit (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Commit method
ms.assetid: 19de9128-b91a-4626-847f-af721edaa24e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e6983eaccf1a934a318c69e72ebdfebf17d2ad9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224725"
---
# <a name="irowsetfastloadcommit-ole-db"></a>IRowsetFastLoad::Commit (OLE DB)
  挿入される行のバッチの終わりをマークし、挿入された行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルに書き込みます。 サンプルについてを参照してください[一括コピー データを使用して IRowsetFastLoad &#40;OLE DB&#41; ](irowsetfastload-ole-db.md)と[SQL サーバーを使用して IROWSETFASTLOAD および ISEQUENTIALSTREAM の BLOB データの送信&#40;OLE DB&#41;](../native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)。  
  
## <a name="syntax"></a>構文  
  
```  
  
HRESULT Commit(  
BOOL   
fDone  
);  
  
```  
  
## <a name="arguments"></a>引数  
 *fDone*[in]  
 FALSE の場合、行セットは有効なまま保持され、コンシューマーはこの行セットを使用してさらに行を挿入できます。 TRUE の場合、行セットは無効になり、コンシューマーはこれ以上行を挿入できません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 S_OK  
 メソッドが成功し、挿入されたすべてのデータが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込まれました。  
  
 E_FAIL  
 プロバイダー固有のエラーが発生しました。 特定のエラー テキストのエラー情報をプロバイダーから取得してください。  
  
 E_UNEXPECTED  
 既に **IRowsetFastLoad::Commit** メソッドによって無効になっている一括コピー行セットに対して呼び出されました。  
  
## <a name="remarks"></a>コメント  
 A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ネイティブ クライアント OLE DB プロバイダーの一括コピー行セットは、遅延更新モードの行セットとして動作します。 ユーザーが行セットを使用して行データを挿入すると、挿入された行は、**IRowsetUpdate** をサポートする行セットでの保留中の挿入と同様の形式で扱われます。  
  
 コンシューマーは、**IRowsetUpdate::Update** メソッドを使用して保留中の行を SQL Server のインスタンスに送信するのと同様に、一括コピー行セットに対して **Commit** メソッドを呼び出して、挿入された行を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込む必要があります。  
  
 コンシューマーが **Commit** メソッドを呼び出さないで一括コピー行セットの参照を解放すると、挿入されてもそれ以前に書き込まれていない行はすべて失われます。  
  
 コンシューマーは、*fDone* 引数を FALSE に設定して **Commit** メソッドを呼び出すことにより、挿入される行をバッチ処理できます。 *fDone* を TRUE に設定すると、その行セットは無効になります。 無効な一括コピー行セットでは、**ISupportErrorInfo** インターフェイスと **IRowsetFastLoad::Release** メソッドのみがサポートされます。  
  
## <a name="see-also"></a>参照  
 [IRowsetFastLoad &#40;OLE DB&#41;](irowsetfastload-ole-db.md)  
  
  
