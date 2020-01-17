---
title: ハンドラーのプロパティ (RDS) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a7423879b8263d87575d913c4863143faf3573e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964007"
---
# <a name="handler-property-rds"></a>Handler プロパティ (RDS)
機能を拡張するプログラム (ハンドラー) のサーバー側のカスタマイズの名前を示す、 [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)とで使用されるパラメーター、*ハンドラー*します。  
  
 **適用対象します。** [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *String*  
 A**文字列**コンマ区切りのすべてのハンドラーと、パラメーター名を含む値 (たとえば、 `"handlerName,parm1,parm2,...,parm` *N*`"`)。  
  
## <a name="remarks"></a>コメント  
 このプロパティはサポート[カスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)、設定を必要とする機能、 [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**します。  
  
 ハンドラーとそのパラメーターの名前は、存在する場合、コンマで区切られます (「,」)。 予期しない動作は発生する場合は、セミコロン (「;」) 内で任意の場所が表示されます。*文字列*します。 独自のハンドラーを記述するには、サポート提供される、 **IDataFactoryHandler**インターフェイス。  
  
 既定のハンドラーの名前は**MSDFMAP します。ハンドラー**、という名前のカスタマイズ ファイルをその既定のパラメーターは、 **MSDFMAP します。INI**します。 このプロパティを使用して、サーバー管理者によって作成された別のカスタマイズ ファイルを呼び出します。  
  
 設定する代わりに、**ハンドラー**プロパティが、ハンドラーと内のパラメーターを指定するには、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティですつまり、"**ハンドラー =**  _。handlerName、parameter1、parameter2 など、います。_ ".  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [Handler プロパティの例 (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [DataFactory オブジェクト (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


