---
title: カスタマイズされた独自のハンドラーの記述 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98e2ec3538de68bffa5b22acc94dda3d81e5c6f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921887"
---
# <a name="writing-your-own-customized-handler"></a>独自のカスタム ハンドラーの記述
RDS のサポート、既定値を希望する IIS サーバー管理者がいるかどうか、独自のハンドラーを記述したい場合がありますが、ユーザーの要求より詳細に制御し、アクセス権。  
  
 MSDFMAP します。ハンドラーの実装、 **IDataFactoryHandler**インターフェイス。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="idatafactoryhandler-interface"></a>IDataFactoryHandler インターフェイス  
 このインターフェイスは、2 つのメソッドを持って**GetRecordset**と**再接続**します。 どちらの方法では、する必要があります、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティに設定する**adUseClient**します。  
  
 どちらの方法は、最初のコンマの後に表示される引数を受け取る、"**ハンドラー =** "キーワード。 たとえば、`"Handler=progid,arg1,arg2;"`の引数の文字列を渡す`"arg1,arg2"`と`"Handler=progid"`null 引数を渡します。  
  
## <a name="getrecordset-method"></a>GetRecordset メソッド  
 このメソッドは、データ ソース クエリを実行し、新たに作成[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの指定された引数を使用します。 **Recordset**で開く必要がある**adLockBatchOptimistic**され、非同期的に開かれませんする必要があります。  
  
### <a name="arguments"></a>引数  
 ***conn***接続文字列。  
  
 ***args***ハンドラーの引数。  
  
 ***クエリ***クエリを行うためのコマンド テキスト。  
  
 ***ppRS***ポインター位置、**レコード セット**返される必要があります。  
  
## <a name="reconnect-method"></a>メソッドを再接続します。  
 このメソッドは、データ ソースを更新します。 新たに作成、[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトとの接続、指定された**レコード セット**します。  
  
### <a name="arguments"></a>引数  
 ***conn***接続文字列。  
  
 ***args***ハンドラーの引数。  
  
 ***Pr*** A **Recordset**オブジェクト。  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 これは、インターフェイス定義**IDataFactoryHandler**に表示される、 **msdfhdl.idl**ファイル。  
  
```cpp
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>関連項目  
 [カスタマイズ ファイル Connect セクション](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [カスタマイズ ファイル Logs セクション](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [カスタマイズ ファイル SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [カスタマイズ ファイル UserList セクション](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要なクライアント設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [カスタマイズ ファイルの概要](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


