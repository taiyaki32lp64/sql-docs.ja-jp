---
title: エラー処理 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cb3213b6a4c5711ccb8d6f9243047d8361a6e37
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925421"
---
# <a name="error-handling"></a>エラー処理
ADO では、いくつかの方法を使用して、発生したエラーのアプリケーションに通知します。 このセクションでは、ADO と、アプリケーションに通知する方法を使用しているときに発生するエラーの種類について説明します。 最後にこれらのエラーを処理する方法に関する推奨事項をします。  
  
## <a name="how-does-ado-report-errors"></a>ADO がエラーを報告する方法  
 ADO では、いくつかの方法でエラーについて通知します。  
  
-   ADO エラーは、実行時エラーを生成します。 ADO エラーを使用するなどの他の実行時エラーの場合と同じ方法で処理、 **On Error** Visual Basic でのステートメント。  
  
-   プログラムでは、OLE DB からエラーを受信できます。 OLE DB エラーでは、実行時のエラーも生成されます。  
  
-   かどうか、エラーは、データ プロバイダーは、1 つまたは複数に固有**エラー**に配置されたオブジェクト、**エラー**のコレクション、**接続**データにアクセスするために使用されたオブジェクトエラーが発生したときに格納します。  
  
-   また、イベントを発生させたプロセスには、エラーが発生しました、エラー情報に置かれます。、**エラー**オブジェクトと、イベントにパラメーターとして渡されます。 参照してください[ADO イベントの処理](../../../ado/guide/data/handling-ado-events.md)イベントについての詳細。  
  
-   更新プログラムまたは関連するその他の一括操作を処理するときに発生する問題をバッチ処理、**レコード セット**によって示すことができます、**状態**のプロパティ、**レコード セット**します。 スキーマの制約違反または十分なアクセス許可を指定して、によって、**可能**値。  
  
-   特定の関連する発生する問題**フィールド**現在のレコードもで示されます、**状態**の各プロパティ**フィールド**で、**フィールド**のコレクション、**レコード**または**Recordset**します。 完了できませんでした。 更新または互換性のないデータ型を指定してなど**FieldStatusEnum**値。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ADO エラー](../../../ado/guide/data/ado-errors.md)  
  
-   [プロバイダー エラー](../../../ado/guide/data/provider-errors.md)  
  
-   [フィールドに関連するエラー情報](../../../ado/guide/data/field-related-error-information.md)  
  
-   [レコードセット関連のエラー情報](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [他の言語でエラーを処理する](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [エラーの予測](../../../ado/guide/data/anticipating-errors.md)
