---
title: DataControl エラー コード |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], DataControl
- DataControl errors [ADO]
ms.assetid: 293df9d5-e1a2-406d-9107-07bf7cdc6f96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b59f0f98122d37447e2e702304a31c44073bacfa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926845"
---
# <a name="datacontrol-object-error-codes"></a>DataControl オブジェクトのエラー コードします。
次の表、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトのエラー コード。 下位 2 バイトの正の 10 進変換、完全なエラー コードと 16 進数の値の負の値の 10 進数の翻訳が表示されます。

|RDS.DataControl エラー コード|数値|説明|
|---------------------------------|------------|-----------------|
|**IDS_AsyncPending**|4107 -2146824175 0x800A1011|非同期操作が保留中に、操作を実行できません。|
|**IDS_BadInlineTablegram**|4105 -2146824183 0x800A1009|不適切なインライン tablegram します。|
|**IDS_CantConnect**|4099 -2146824189 0x800A1003|サーバーに接続することはできません。|
|**IDS_CantCreateObject**|4100 -2146824188 0x800A1004|ビジネス オブジェクトを作成できません。|
|**IDS_CantFindDataspace**|4102 -2146824186 0x800A1006|データ領域のプロパティが無効です。|
|**IDS_CantInvokeMethod**|4101 -2146824187 0x800A1005|ビジネス オブジェクトでメソッドを呼び出すことができません。|
|**IDS_CrossDomainWarning**|4112 -2146824170 0x800A1016|このページでは、別のドメイン上のデータにアクセスします。 これを許可しますか。 Internet Explorer では、このメッセージを回避するために追加できます Web サイトをセキュリティで保護された信頼済みサイト ゾーンに上、**セキュリティ**のタブ、**インターネット オプション** ダイアログ ボックス。|
|**IDS_InvalidADCClientVersion**|4106 -2146824176 0x800A1010|無効な RDS クライアントのバージョンのクライアントは、サーバーよりも新しいです。|
|**IDS_INVALIDARG**|5376 -2147019520 0x80071500|1 つ以上の引数が無効です。|
|**IDS_InvalidBindings**|4097 -2146824191 0x800A1001|プロパティのバインド エラー。|
|**IDS_InvalidParam**|4110 -2146824172 0x800A1014|1 つ以上の引数が無効です。|
|**IDS_NOINTERFACE**|5377 -2147019519 0x80071501|このようなインターフェイスがサポートされていません。|
|**IDS_NotReentrant**|4111 -2146824171 0x800A1015|イベント ハンドラーがまだ処理中に、要求を実行できません。|
|**IDS_ObjectNotSafe**|4103 -2146824185 0x800A1007|このコンピューターの安全性の設定には、ビジネス オブジェクトの作成が禁止されています。|
|**IDS_RecordsetNotOpen**|4109 -2146824173 0x800A1013|**レコード セット**が開かれていません。|
|**IDS_ResetInvalidField**|4108 -2146824174 0x800A1012|指定された列**SortColumn**または**FilterColumn**存在しません。|
|**IDS_RowsetNotUpdateable**|4104 -2146824184 0x800A1008|行セットは更新できません。|
|**IDS_UnexpectedError**|4351 -2146823937 0x800A10FF|予期しないエラーがあります。|
|**IDS_UpdatesFailed**|4098 -2146824190 0x800A1002|データベースを更新できません。|
|**IDS_URLMONNotFound**|4119 -2146824169 0x800A1017|DataControl **URL**プロパティには、システム ファイルが見つかりません、Urlmon.dll が必要です。|

## <a name="see-also"></a>関連項目
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)
