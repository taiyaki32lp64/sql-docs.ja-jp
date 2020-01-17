---
title: ErrorValueEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ErrorValueEnum
helpviewer_keywords:
- ErrorValueEnum enumeration [ADO]
ms.assetid: 9469ba3a-5e4f-4a10-bbb8-a51a6c9660ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18117be8dccc64f7ed2583170cf062145836f337
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932874"
---
# <a name="errorvalueenum"></a>ErrorValueEnum
ADO の実行時エラーの種類を指定します。  
  
 エラー番号の 3 つのフォームが表示されます。  
  
-   正 10 進数、2 つの下位バイト 10 進数形式で完全な数。 この数は、既定の Visual Basic エラー メッセージ ダイアログ ボックスに表示されます。 たとえば、実行時エラー '3707' です。  
  
-   負の完全なエラーの数の 10 進数の 10 進数の変換。  
  
-   完全なエラー番号の 16 進数、16 進数表現。 Windows 機能のコードは 4 桁です。 ADO エラー番号の機能のコードは*A*します。以下に例を示します。0x800***A***0e7b がその例です。  
  
> [!NOTE]
>  OLE DB エラーは、ADO アプリケーションに渡すことがあります。 これらを識別しての Windows 機能のコードで通常、 *4*します。 たとえば、0x800***4***します。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**adErrBoundToCommand**|3707 -2146824581 0x800A0E7B|変更することはできません、 **ActiveConnection**のプロパティを**レコード セット**を持つオブジェクトを**コマンド**のソースとしてオブジェクト。|  
|**adErrCannotComplete**|3732 -2146824556 0x800A0E94|サーバーは、操作を完了できません。|  
|**adErrCantChangeConnection**|3748 -2146824540 0x800A0EA4|接続が拒否されました。 新しい接続を要求するには、既に使用されているものよりも異なる特性があります。|  
|**adErrCantChangeProvider**|3220 -2146825068 0X800A0C94|指定されたプロバイダーは、既に使用されているかによって異なります。|  
|**adErrCantConvertvalue**|3724 -2146824564 0x800A0E8C|符号の不一致またはデータのオーバーフロー以外の理由は、データ値を変換できません。 たとえば、変換はデータを省略しています。|  
|**adErrCantCreate**|3725 -2146824563 0x800A0E8D|データ値を設定またはフィールドのデータ型が、不明か、プロバイダーが操作を実行するリソースが不足しているために取得できません。|  
|**adErrCatalogNotSet**|3747 -2146824541 0x800A0EA3|操作が必要ですが、有効な**ParentCatalog**します。|  
|**adErrColumnNotOnThisRow**|3726 -2146824562 0x800A0E8E|レコードでは、このフィールドは含まれません。|  
|**adErrDataConversion**|3421 -2146824867 0x800A0D5D|アプリケーションでは、現在の操作が正しくない型の値を使用します。|  
|**adErrDataOverflow**|3721 -2146824567 0x800A0E89|フィールドのデータ型で表されるデータ値が大きすぎます。|  
|**adErrDelResOutOfScope**|3738 -2146824550 0x800A0E9A|削除するオブジェクトの URL は、現在のレコードの範囲外です。|  
|**adErrDenyNotSupported**|3750 -2146824538 0x800A0EA6|プロバイダーは、共有の制限をサポートしていません。|  
|**adErrDenyTypeNotSupported**|3751 -2146824537 0x800A0EA7|プロバイダーは、要求された種類の制限を共有をサポートしていません。|  
|**adErrFeatureNotAvailable**|3251 -2146825037 0x800A0CB3|オブジェクトまたはプロバイダーでは、要求された操作を実行できません。|  
|**adErrFieldsUpdateFailed**|3749 -2146824539 0x800A0EA5|フィールドを更新できませんでした。 詳細については、確認、**状態**個々 のフィールド オブジェクトのプロパティ。|  
|**adErrIllegalOperation**|3219 -2146825069 0x800A0C93|このコンテキストでは、操作は許可されません。|  
|**adErrIntegrityViolation**|3719 -2146824569 0x800A0E87|データ値、フィールドの整合性制約と競合しています。|  
|**adErrInTransaction**|3246 -2146825042 0x800A0CAE|**接続**トランザクションの実行中に、オブジェクトを明示的に閉じることができません。|  
|**adErrInvalidArgument**|3001 -2146825287 0x800A0BB9|引数型が正しくありませんは許容範囲外ですや、相互に競合します。|  
|**adErrInvalidConnection**|3709 -2146824579 0x800A0E7D|この操作を実行する接続を使用できません。 閉じているか、このコンテキストで無効になります。|  
|**adErrInvalidParamInfo**|3708 -2146824580 0x800A0E7C|**パラメーター**オブジェクトが正しく定義されていません。 一貫性のないまたは不完全な情報が提供されました。|  
|**adErrInvalidTransaction**|3714 -2146824574 0x800A0E82|トランザクションを調整するか、有効でないが開始されていません。|  
|**adErrInvalidURL**|3729 -2146824559 0x800A0E91|URL には、無効な文字が含まれています。 URL が正しく入力されていることを確認します。|  
|**adErrItemNotFound**|3265 -2146825023 0x800A0CC1|要求された名前または序数に対応するコレクション内の項目が見つかりません。|  
|**adErrNoCurrentRecord**|3021 -2146825267 0x800A0BCD|いずれか**BOF**または**EOF**が true の場合、または現在のレコードが削除されました。 要求された操作では、現在のレコードが必要です。|  
|**adErrNotExecuting**|3715 -2146824573 0x800A0E83|実行していないときに、操作を実行できません。|  
|**adErrNotReentrant**|3710 -2146824578 0x800A0E7E|イベント処理中には、操作を実行できません。|  
|**adErrObjectClosed**|3704 -2146824584 0x800A0E78|オブジェクトが閉じられたときに、操作は許可されません。|  
|**adErrObjectInCollection**|3367 -2146824921 0x800A0D27|オブジェクトのコレクションは既にです。 追加できません。|  
|**adErrObjectNotSet**|3420 -2146824868 0x800A0D5C|オブジェクトが有効ではなくなりました。|  
|**adErrObjectOpen**|3705 -2146824583 0x800A0E79|オブジェクトが開いている場合、操作は許可されません。|  
|**adErrOpeningFile**|3002 -2146825286 0x800A0BBA|ファイルを開くことができませんでした。|  
|**adErrOperationCancelled**|3712 -2146824576 0x800A0E80|操作は、ユーザーによって取り消されました。|  
|**adErrOutOfSpace**|3734 -2146824554 0x800A0E96|操作を実行できません。 プロバイダーは、記憶域容量を取得できません。|  
|**adErrPermissionDenied**|3720 -2146824568 0x800A0E88|十分なアクセス許可には、フィールドへの書き込みができないようにします。|  
|**adErrProviderFailed**|3000 -2146825288 0x800A0BB8|プロバイダーは、要求された操作を実行できませんでした。|  
|**adErrProviderNotFound**|3706 -2146824582 0x800A0E7A|プロバイダーが見つかりません。 それが正しくインストールされません。|  
|**adErrReadFile**|3003 -2146825285 0x800A0BBB|ファイルを読み取ることができませんでした。|  
|**adErrResourceExists**|3731 -2146824557 0x800A0E93|コピー操作を実行することはできません。 宛先の URL によって既にという名前のオブジェクトが存在します。 指定**adCopyOverwrite**オブジェクトに置換します。|  
|**adErrResourceLocked**|3730 -2146824558 0x800A0E92|指定した URL によって表されるオブジェクトは、他の 1 つまたは複数のプロセスによってロックされています。 プロセスが終了するまで待機し、操作をやり直してください。|  
|**adErrResourceOutOfScope**|3735 -2146824553 0x800A0E97|送信元または送信先の URL は、現在のレコードの範囲外です。|  
|**adErrSchemaViolation**|3722 -2146824566 0x800A0E8A|データ値は、データ型またはフィールドの制約と競合しています。|  
|**adErrSignMismatch**|3723 -2146824565 0x800A0E8B|データ値が署名されていて、プロバイダーで使用されるフィールドのデータ型が署名されていないので、変換ができませんでした。|  
|**adErrStillConnecting**|3713 -2146824575 0x800A0E81|非同期的に接続する際に、操作を実行できません。|  
|**adErrStillExecuting**|3711 -2146824577 0x800A0E7F|非同期的に実行中には、操作を実行できません。|  
|**adErrTreePermissionDenied**|3728 -2146824560 0x800A0E90|権限はツリーまたはサブツリーにアクセスするだけで十分ではありません。|  
|**adErrUnavailable**|3736 -2146824552 0x800A0E98|操作が完了しなかったし、状態をご利用いただけません。 フィールドを使用できないか、操作は試行されませんでした。|  
|**adErrUnsafeOperation**|3716 -2146824572 0x800A0E84|このコンピューターの安全性設定は、別のドメインのデータ ソースへのアクセスを防止します。|  
|**adErrURLDoesNotExist**|3727 -2146824561 0x800A0E8F|ソース URL またはリンク先の URL の親のいずれかが存在しません。|  
|**adErrURLNamedRowDoesNotExist**|3737 -2146824551 0x800A0E99|この URL でという名前のレコードが存在しません。|  
|**adErrVolumeNotFound**|3733 -2146824555 0x800A0E95|プロバイダーは、URL で指定されたストレージ デバイスに見つかりません。 URL が正しく入力されていることを確認します。|  
|**adErrWriteFile**|3004 -2146825284 0x800A0BBC|ファイルへ書き込めませんでした。|  
|**adWrnSecurityDialog**|3717 -2146824571 0x800A0E85|内部使用専用。 使わないでください。|  
|**adWrnSecurityDialogHeader**|3718 -2146824570 0x800A0E86|内部使用専用。 使わないでください。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
 ADO と WFC と同等の次のサブセットのみが定義されます。  
  
|定数|  
|--------------|  
|AdoEnums.ErrorValue.BOUNDTOCOMMAND|  
|AdoEnums.ErrorValue.DATACONVERSION|  
|AdoEnums.ErrorValue.FEATURENOTAVAILABLE|  
|AdoEnums.ErrorValue.ILLEGALOPERATION|  
|AdoEnums.ErrorValue.INTRANSACTION|  
|AdoEnums.ErrorValue.INVALIDARGUMENT|  
|AdoEnums.ErrorValue.INVALIDCONNECTION|  
|AdoEnums.ErrorValue.INVALIDPARAMINFO|  
|AdoEnums.ErrorValue.ITEMNOTFOUND|  
|AdoEnums.ErrorValue.NOCURRENTRECORD|  
|AdoEnums.ErrorValue.NOTEXECUTING|  
|AdoEnums.ErrorValue.NOTREENTRANT|  
|AdoEnums.ErrorValue.OBJECTCLOSED|  
|AdoEnums.ErrorValue.OBJECTINCOLLECTION|  
|AdoEnums.ErrorValue.OBJECTNOTSET|  
|AdoEnums.ErrorValue.OBJECTOPEN|  
|AdoEnums.ErrorValue.OPERATIONCANCELLED|  
|AdoEnums.ErrorValue.PROVIDERNOTFOUND|  
|AdoEnums.ErrorValue.STILLCONNECTING|  
|AdoEnums.ErrorValue.STILLEXECUTING|  
|AdoEnums.ErrorValue.UNSAFEOPERATION|  
  
## <a name="applies-to"></a>適用対象  
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)  
  
## <a name="see-also"></a>関連項目  
 [ADO エラー コード](../../../ado/guide/appendixes/ado-error-codes.md)
