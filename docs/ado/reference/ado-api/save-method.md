---
title: Save メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ec1601749b6537484cead17c50492de131932ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931172"
---
# <a name="save-method"></a>Save メソッド
保存、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)ファイルまたは[Stream](../../../ado/reference/ado-api/stream-object-ado.md)オブジェクト。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Destination (公開先)*  
 任意。 A**バリアント**ファイルの完全なパス名を表す場所、 **Recordset**を保存するまたはへの参照、 **Stream**オブジェクト。  
  
 *PersistFormat*  
 任意。 A [PersistFormatEnum](../../../ado/reference/ado-api/persistformatenum.md)形式を指定する値、 **Recordset** (XML または adtg 形式) に保存します。 既定値は**adPersistADTG**します。  
  
## <a name="remarks"></a>コメント  
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)メソッドは、オープンでのみ呼び出すこと**Recordset**します。 使用して、 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)後で復元する方法、**レコード セット**から*先*します。  
  
 場合、[フィルター プロパティ](../../../ado/reference/ado-api/filter-property.md)プロパティはに対して有効で、**レコード セット**フィルターでアクセス可能な行のみが保存されます。 場合、**レコード セット**は階層構造を持つ現在の子、**レコード セット**と親を含む、その子が保存**レコード セット**します。 場合、子の Save メソッド**レコード セット**は子とそのすべての子を保存すると、呼び出されるが、親はありません。  
  
 初めて保存するとき、**レコード セット**を指定する省略可能*先*します。 省略した場合*先*の Source プロパティの値に設定の名前を持つ新しいファイルを作成するが、**レコード セット**。  
  
 省略*先*関数を呼び出すと**保存**後、最初の保存または実行時エラーが発生します。 後で呼び出す場合**保存**を新しい*先*、**レコード セット**新しい変換先に保存されます。 ただし、新しい変換先および元の送信先両方開かれます。  
  
 **保存**が閉じない、**レコード セット**または*先*で作業を続行することができますので、**レコード セット**して最新の変更を保存します。 *移行先*されるまで開いたまま、 **Recordset**が閉じられました。  
  
 セキュリティ上の理由から、**保存**メソッドは、Microsoft Internet Explorer によって実行されるスクリプトから低、カスタムのセキュリティ設定の使用のみを許可します。  
  
 場合、**保存**中に、非同期メソッドが呼び出される**レコード セット**フェッチ、実行、または更新し、操作が進行中は**保存**まで非同期の操作の待機完了しました。  
  
 最初の行で始まるレコードの保存、 **Recordset**します。 ときに、**保存**メソッドが終了したらの最初の行に現在の行位置を移動、**レコード セット**します。  
  
 最適な結果を設定、 [CursorLocation プロパティ (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**で**保存**します。 かどうか、プロバイダーがサポートしないすべての機能を保存するために必要な**レコード セット**オブジェクトの場合、カーソル サービスが機能を提供します。  
  
 ときに、**レコード セット**に保存されて、 **CursorLocation**プロパティに設定**adUseServer**、更新プログラムの機能、 **Recordset**は制限されています。 通常、のみ単一テーブルの更新、挿入、および削除が (プロバイダーの機能に依存する) を使用できます。 [メソッドの再同期](../../../ado/reference/ado-api/resync-method.md)メソッドもこの構成では使用できません。  
  
> [!NOTE]
>  保存、**レコード セット**で**フィールド**型の**adVariant**、**追加**、または**しようとする**はADO でサポートされずに、予期しない結果が発生することができます。  
  
 のみがフィルター条件文字列の形式で (例: OrderDate > ' 12/31/1999 ')、永続化の内容に影響を与える**レコード セット**します。 配列が作成されたフィルター**ブックマーク**またはからの値を使用して、 [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) 、永続化の内容には影響しません**Recordset**します。 これらの規則を適用する**Recordset**クライアント側またはサーバー側のカーソルで作成されました。  
  
 *先*パラメーターは、OLE DB IStream インターフェイスをサポートする任意のオブジェクトを受け入れることができます、保存することができます、**レコード セット**ASP 応答オブジェクトに直接します。 詳細についてを参照してください、 **XML レコード セットの保持シナ リオ**します。  
  
 保存することも、 **Recordset** MSXML の DOM オブジェクトのインスタンスには、XML の形式で次の Visual Basic コードに示すようには。  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  階層レコード セット (データ図形) を XML 形式で保存するときに、2 つの制限が適用されます。 場合は、XML に保存することはできません、階層**レコード セット**保留中の更新プログラムが含まれています。 パラメーター化されたを保存することはできませんと階層**レコード セット**します。  
  
 A **Recordset**保存 utf-8 形式を使用して XML の形式が保存されます。 このようなファイルが、ADO Stream に読み込まれると、Stream オブジェクトが開こうとしていない、**レコード セット**ストリームからストリームの文字セット プロパティが utf-8 形式の適切な値に設定されていない限り。  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Stream オブジェクト (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>関連項目  
 [Save および Open メソッドの例 (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [保存および開く方法の例 (vc++)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [SaveToFile メソッド](../../../ado/reference/ado-api/savetofile-method.md)
