---
title: Open メソッド (ADO Record) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_Open
- _Record::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: ab79a623-88a9-40b6-a017-a658bf19b778
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97c7f1c143c83dd35ca5ff17e9776d79fb734ff9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917923"
---
# <a name="open-method-ado-record"></a>Open メソッド (ADO Record)
既存を開く[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクト、またはで表される新しい項目の作成、**レコード**ファイルやディレクトリなどです。  
  
## <a name="syntax"></a>構文  
  
```  
  
Open Source, ActiveConnection, Mode, CreateOptions, Options, UserName, Password  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**バリアント**これで表されるエンティティの URL を表すことがあります**レコード**オブジェクト、**コマンド**、開いている[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)またはもう 1 つ**レコード**オブジェクト、SQL SELECT ステートメントまたはテーブル名を含む文字列。  
  
 *ActiveConnection*  
 任意。 A**バリアント**接続文字列またはオープンを表す[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト。  
  
 *モード*  
 任意。 A [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 、結果として得られるアクセス モードを指定する値**レコード**オブジェクト。 既定値は**adModeUnknown**します。  
  
 *CreateOptions*  
 任意。 A [RecordCreateOptionsEnum](../../../ado/reference/ado-api/recordcreateoptionsenum.md)かどうか、既存のファイルまたはディレクトリを開く必要があります、または新しいファイルまたはディレクトリを作成する必要がありますを指定する値。 既定値は**adFailIfNotExists**します。 かどうか、既定値に設定して、アクセス モードがから取得した、[モード](../../../ado/reference/ado-api/mode-property-ado.md)プロパティ。 このパラメーターは無視されますと、*ソース*パラメーターに URL が含まれていません。  
  
 *[オプション]*  
 任意。 A [RecordOpenOptionsEnum](../../../ado/reference/ado-api/recordopenoptionsenum.md)開くのためのオプションを指定する値、**レコード**します。 既定値は**adOpenRecordUnspecified**します。 これらの値を組み合わせることができます。  
  
 *UserName*  
 任意。 A**文字列**、必要な場合へのアクセスを承認するユーザー ID を含む値*ソース*します。  
  
 *Password*  
 任意。 A**文字列**、必要な場合を検証するパスワードを含む値*UserName*します。  
  
## <a name="remarks"></a>Remarks  
 *ソース*可能性があります。  
  
-   URL。 URL のプロトコルが http の場合は、インターネット プロバイダーは既定で呼び出されます。 URL が実行可能スクリプトを含むノードを指すかどうか (など、します。ASP ページの場合)、**レコード**ではなく、実行されたソースを格納している内容が既定で表示します。 使用して、*オプション*この動作を変更する引数。  
  
-   A**レコード**オブジェクト。 A**レコード**別のオブジェクトを開く**レコード**元を複製**レコード**オブジェクト。  
  
-   A**コマンド**オブジェクト。 開かれている**レコード**オブジェクトが実行することによって返される単一行を表す、**コマンド**します。 結果が 1 つの行よりも多く含まれる場合は、レコードの最初の行の内容し、にエラーが追加される可能性があります、**エラー**コレクション。  
  
-   SQL SELECT ステートメント。 開かれている**レコード**オブジェクトは、文字列の内容を実行することによって返される単一行を表します。 結果が 1 つの行よりも多く含まれる場合は、レコードの最初の行の内容し、にエラーが追加される可能性があります、**エラー**コレクション。  
  
-   テーブル名です。  
  
 場合、**レコード**オブジェクトは、URL でアクセスできませんエンティティを表します (の行など、**レコード セット**データベースから派生)、両方の値、 [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md)。プロパティとフィールドを使用してアクセス、 **adRecordURL**定数が null です。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [Open メソッド (ADO Connection)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema メソッド](../../../ado/reference/ado-api/openschema-method.md)
