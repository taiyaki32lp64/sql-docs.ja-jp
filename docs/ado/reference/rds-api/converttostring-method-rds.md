---
title: ConvertToString メソッド (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71e50c4f611342c8e06687c47ab1c45fb60974ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964572"
---
# <a name="converttostring-method-rds"></a>ConvertToString メソッド (RDS)
変換を[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)レコード セットのデータを表す MIME 文字列にします。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataFactory*  
 オブジェクト変数を表す、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクト。  
  
 *レコード セット*  
 オブジェクト変数を表す、 **Recordset**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 .Asp ファイルを使用して**ConvertToString**を埋め込む、**レコード セット**にクライアント コンピューターに転送のためにサーバーで生成された HTML ページ。  
  
 **ConvertToString**が初めて読み込まれる、 **Recordset**カーソル サービスにテーブル、および MIME 形式でストリームを生成します。  
  
 クライアントでは、リモート データ サービスは、すべての機能に MIME 文字列を変換できます**Recordset**します。 400 より少ない行以上の行ごとの 1024 バイト幅でのデータの処理に適してします。 BLOB データをストリーミングするのに使用することはできませんし、大きな結果が HTTP 経由で設定します。 送信中の圧縮は行われません、文字列でとても大きなデータ セットは時間がかかるトランスポートを定義およびネイティブ トランスポート プロトコルとしてリモート データ サービスによってデプロイ tablegram の送信中に最適化された形式と比較した場合、HTTP 経由で。  
  
> [!NOTE]
>  クライアントの HTML ページに、結果として得られる MIME 文字列を埋め込むには、Active Server Pages を使用する場合が VBScript のバージョンより前のバージョン 2.0 が 32 K に文字列のサイズを制限することに注意してください。 この制限を超えると、エラーが返されます。 クエリ スコープ比較的小さく保つ .asp ファイルを使用して MIME の埋め込みを使用する場合。 これを解決するには、Microsoft Windows スクリプト テクノロジ Web サイトから VBScript の最新バージョンをダウンロードします。  
  
## <a name="applies-to"></a>適用対象  
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>関連項目  
 [ConvertToString メソッドの例 (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [ConvertToString メソッドの例 (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


