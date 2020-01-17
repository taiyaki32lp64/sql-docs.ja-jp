---
title: CopyRecord メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aaabb32234cefe2e3c3727ce5a18dd2d98549a77
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933417"
---
# <a name="copyrecord-method-ado"></a>CopyRecord メソッド (ADO)
によって表されるエンティティのコピーを[レコード](../../../ado/reference/ado-api/record-object-ado.md)別の場所にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Source*  
 任意。 A**文字列**URL を含むエンティティを指定するコピーする (たとえば、ファイルまたはディレクトリ) の値。 場合*ソース*を省略するか、空の文字列、ファイルまたはディレクトリが現在によって表される指定[レコード](../../../ado/reference/ado-api/record-object-ado.md)がコピーされます。  
  
 *変換先*  
 任意。 A**文字列**場所を指定する URL を含む値、*ソース*がコピーされます。  
  
 *UserName*  
 任意。 A**文字列**値が必要な場合へのアクセスを承認するユーザー ID を含む*先*します。  
  
 *Password*  
 任意。 A**文字列**値が必要な場合を検証するパスワードを含む*UserName*します。  
  
 *[オプション]*  
 任意。 A [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md)の既定値を持つ値**adCopyUnspecified**します。 このメソッドの動作を指定します。  
  
 *Async*  
 任意。 A**ブール**値と**True**、この操作を非同期にすることを指定します。  
  
## <a name="return-value"></a>戻り値  
 A**文字列**を通常の値を返す値*先*します。 ただし、返される正確な値は、プロバイダーによって異なります。  
  
## <a name="remarks"></a>コメント  
 値*ソース*と*先*することはできませんと同じです。 それ以外の場合、実行時エラーが発生します。 少なくとも 1 つのサーバー、パス、またはリソースの名前が異なる必要があります。  
  
 すべての子 (たとえば、サブディレクトリ)*ソース*はないと、コピーされた再帰的に**adCopyNonRecursive**を指定します。 再帰的な操作で*先*のサブディレクトリではない必要があります*ソース*。 それ以外の操作を完了できません。  
  
 このメソッドは失敗*先*しない限り (たとえば、ファイルまたはディレクトリ)、既存のエンティティを識別する**adCopyOverWrite**が指定されて。  
  
> [!IMPORTANT]
>  使用して、 **adCopyOverWrite**慎重オプションします。 など、ファイルをディレクトリにコピーするときに、このオプションを指定する*削除*ディレクトリ、ファイルに置き換えます。  
  
> [!NOTE]
>  Http スキームを使用して Url が自動的に呼び出さ、 [Microsoft OLE DB Provider for Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)します。 詳細については、次を参照してください。[絶対と相対 Url](../../../ado/guide/data/absolute-and-relative-urls.md)します。  
  
## <a name="applies-to"></a>適用対象  
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
