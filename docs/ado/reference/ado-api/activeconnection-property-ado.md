---
title: ActiveConnection プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::ActiveConnection
- Recordset15::get_ActiveConnection
- _Record::ActiveConnection
helpviewer_keywords:
- ActiveConnection property [ADO]
ms.assetid: 52d0a96c-14fb-4ad9-b004-4d821bc0a6db
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dabf974e36b1f6beaff36f3a4888c128d7dfe1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921514"
---
# <a name="activeconnection-property-ado"></a>ActiveConnection プロパティ (ADO)
先を示します[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの指定した[コマンド](../../../ado/reference/ado-api/command-object-ado.md)、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)、または[レコード](../../../ado/reference/ado-api/record-object-ado.md)オブジェクトが現在属しています。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 設定または取得を**文字列**場合は、接続を終了すると、接続の定義を含む値**バリアント**現在を含む**接続**オブジェクトの場合、接続は開いています。 既定では、null オブジェクト参照です。 参照してください、 [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティ。  
  
## <a name="remarks"></a>コメント  
 使用して、 **ActiveConnection**プロパティの**接続**オブジェクトを指定した**コマンド**オブジェクトが実行されますか、指定された**レコード セット**が開きます。  
  
## <a name="command"></a>コマンド  
 **コマンド**、オブジェクト、 **ActiveConnection**読み取り/書き込みプロパティです。  
  
 呼び出すしようとした場合、 [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)メソッドを**コマンド**、オープンにこのプロパティを設定する前にオブジェクト**接続**オブジェクトか、有効な接続文字列、エラーが発生します。  
  
 場合、**接続**に割り当てられているオブジェクト、 **ActiveConnection**プロパティ、オブジェクトを開く必要があります。 閉じた接続オブジェクトを割り当てると、エラーが発生します。  
  
### <a name="note"></a>注意  
 **Microsoft Visual Basic**設定、 **ActiveConnection**プロパティを*Nothing*の関連付けを解除、**コマンド**オブジェクトから現在**接続**と、データ ソースに関連付けられているリソースを解放するプロバイダー。 関連付けることができますし、**コマンド**同一または別のオブジェクト**接続**オブジェクト。 一部のプロバイダーでは、いずれかから、プロパティの設定を変更できます。**接続**を最初に、プロパティを設定することなく別*Nothing*します。  
  
 場合、[パラメーター](../../../ado/reference/ado-api/parameters-collection-ado.md)のコレクション、**コマンド**オブジェクトには、プロバイダーによって指定されたパラメーターが含まれています、設定した場合、コレクションの消去、 **ActiveConnection**プロパティを*Nothing*または別**接続**オブジェクト。 手動で作成する場合[パラメーター](../../../ado/reference/ado-api/parameter-object.md)オブジェクトし、入力して、**パラメーター**のコレクション、**コマンド**オブジェクト、設定、 **ActiveConnection**プロパティを*Nothing*または別**接続**リーフ オブジェクト、**パラメーター**コレクションをそのまま残ります。  
  
 閉じる、**接続**オブジェクトを**コマンド**オブジェクトが関連付けられているセット、 **ActiveConnection**プロパティを*Nothing*します。 このプロパティの設定を閉じている**接続**オブジェクト、エラーが発生します。  
  
## <a name="recordset"></a>レコードセット  
 オープンの**レコード セット**オブジェクトまたは**レコード セット**オブジェクト[ソース](../../../ado/reference/ado-api/source-property-ado-recordset.md)プロパティが有効な**コマンド**オブジェクト、 **ActiveConnection**プロパティは読み取り専用です。 それ以外の場合、読み取り/書き込みになります。  
  
 このプロパティを設定するには有効な**接続**オブジェクトまたは有効な接続文字列にします。 この場合、プロバイダーを作成、新しい**接続**オブジェクトのこの定義を使用して、接続が開かれます。 さらに、プロバイダーはこのプロパティの新しいに設定が**接続**にアクセスする方法を提供するオブジェクト、**接続**オブジェクトの拡張エラー情報またはその他のコマンドを実行します。  
  
 使用する場合、 *ActiveConnection*の引数、[開く](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドを開き、**レコード セット**オブジェクト、 **ActiveConnection**プロパティは引数の値を継承します。  
  
 設定した場合、**ソース**のプロパティ、**レコード セット**を有効なオブジェクト**コマンド**オブジェクト変数を**ActiveConnection**のプロパティ**Recordset**の設定を継承、**コマンド**オブジェクトの**ActiveConnection**プロパティ。  
  
> [!NOTE]
>  **リモート データ サービスの使用状況**クライアント側で使用すると**Recordset**オブジェクト、または (Microsoft Visual Basic または Visual Basic Scripting Edition) で接続文字列にのみ、このプロパティを設定できます*Nothing*.  
  
## <a name="record"></a>レコード  
 このプロパティは読み取り/書き込み時に、**レコード**オブジェクトが閉じられるし、接続文字列または開いているへの参照を含めることができます**接続**オブジェクト。 このプロパティは読み取り専用ときに、**レコード**オブジェクトを開くと、および開いているへの参照が含まれています**接続**オブジェクト。  
  
 A**接続**オブジェクトが暗黙的に作成されるときに、**レコード**オブジェクトは、URL から開きます。 開く、**レコード**開き、既存の**接続**オブジェクトを割り当てることによって、**接続**オブジェクトをこのプロパティは、またはを使用して、 **の接続**オブジェクト内のパラメーターとして、[オープン](../../../ado/reference/ado-api/open-method-ado-record.md)メソッドの呼び出し。 場合、**レコード**を既存の開いた**レコード**または[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)が自動的に関連付けられている**レコード**または**レコード セット**オブジェクトの**接続**オブジェクト。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
  
||||  
|-|-|-|  
|[Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (vc++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、サイズ、および方向プロパティの例 (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [ConnectionString プロパティ (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md)
