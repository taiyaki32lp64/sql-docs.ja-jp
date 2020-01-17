---
title: Open メソッド (ADO Connection) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::raw_Open
- Connection15::Open
- _Connection::Open
helpviewer_keywords:
- Open method [ADO]
ms.assetid: 663defab-5545-4973-9036-24d5882c9737
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15115313613ea8f86dd2267c6be3c231cab92503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931937"
---
# <a name="open-method-ado-connection"></a>Open メソッド (ADO Connection)
データ ソースへの接続を開きます。  
  
## <a name="syntax"></a>構文  
  
```  
  
connection.Open ConnectionString, UserID, Password, Options  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ConnectionString*  
 任意。 A**文字列**接続情報を表す値です。 参照してください、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティの詳細については、有効な設定をします。  
  
 *UserID*  
 任意。 A**文字列**接続を確立するときに使用するユーザー名を含む値。  
  
 *Password*  
 任意。 A**文字列**接続を確立するときに使用するパスワードを表す値です。  
  
 *[オプション]*  
 任意。 A [ConnectOptionEnum](../../../ado/reference/ado-api/connectoptionenum.md)後に、このメソッドを返す必要があるかどうかを決定する値 (同期) (非同期)、接続が確立される前に、または。  
  
## <a name="remarks"></a>コメント  
 使用して、**オープン**メソッドを[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトは、データ ソースへの物理接続を確立します。 このメソッドが正常に完了したら、接続はライブとに対してコマンドを発行し、結果を処理することができます。  
  
 オプションを使用して、 *ConnectionString*一連を含む接続文字列を指定する引数*引数* *値 =* ステートメントをセミコロンで区切られた、またはURL で識別されるファイルまたはディレクトリのリソース。 **ConnectionString**プロパティで使用される値を自動的に継承する、 *ConnectionString*引数。 そのため、いずれかに設定できます、 **ConnectionString**のプロパティ、**接続**、開く前にオブジェクトまたはを使用して、 *ConnectionString*引数を設定またはオーバーライドするには現在の接続パラメーター中に、**オープン**メソッドの呼び出し。  
  
 ユーザー名とパスワード両方の情報を渡す場合、 *ConnectionString*引数と省略可能な*UserID*と*パスワード*、引数、 *UserID*と*パスワード*引数で指定された値をオーバーライドは*ConnectionString*します。  
  
 開いている操作が完了すると**接続**を使用して、[閉じる](../../../ado/reference/ado-api/close-method-ado.md)メモリを解放するメソッドには、システム リソースが関連付けられています。 オブジェクトを閉じるは削除されません。 メモリからそのプロパティの設定を変更して使用できます、**開く**メソッドを後でもう一度開きます。 メモリからオブジェクトを完全に排除するに、オブジェクト変数を設定します。 *Nothing*します。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**接続**オブジェクト、**オープン**メソッドまで、サーバーへの接続を確立実際には、[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)で開かれた、**接続**オブジェクト。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open および Close メソッドの例 (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Open および Close メソッドの例 (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Open および Close メソッドの例 (vc++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open メソッド (ADO Record)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [OpenSchema メソッド](../../../ado/reference/ado-api/openschema-method.md)
