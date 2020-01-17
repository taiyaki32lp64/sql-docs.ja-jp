---
title: DELETE TAG コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 576e7e10d9d6f5c7e8616f57bde2dfed05503eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112070"
---
# <a name="delete-tag-command"></a>DELETE TAG コマンド
複合インデックス (.cdx) ファイルからのタグまたはタグを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>引数  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]] ...  
 複合インデックスのファイルから削除するタグを指定します。 削除の 1 つのタグを持つ複数のタグを削除するには、タグ名のコンマ区切りの一覧を含みます。 インデックスを開くファイルには、同じ名前の 2 つ以上のタグが存在する場合の特定のインデックス ファイルからのタグを削除 OF を含めることによって*CDXFileName*します。  
  
 すべて [OF *CDXFileName*]  
 複合インデックスのファイルからすべてのタグを削除します。 現在のテーブルに複合インデックスの構造上のファイルがある場合は、インデックス ファイルからすべてのタグが削除、インデックス ファイル、ディスクから削除されますおよび構造型の複合インデックスを関連付けられているファイルの存在を示す表のヘッダーでフラグを削除します。 すべてで使用*CDXFileName*複合インデックスの構造上のファイル以外の複合インデックスを開いているファイルからすべてのタグを削除します。  
  
## <a name="remarks"></a>コメント  
 インデックスを作成、複合インデックスのファイルには、インデックス エントリに対応するタグが含まれます。 タグの削除は、複合インデックスを開いているファイルからのタグまたはタグの削除に使用されます。 現在の作業領域で開いている複合インデックスのファイルからのタグのみを削除できます。 複合インデックスのファイルからすべてのタグを削除する場合は、ファイルがディスクから削除されます。  
  
 Visual FoxPro は、(1 つは、開いている) 場合に最初に、構造型の複合インデックス ファイル内のタグを検索します。 複合インデックスの構造上のファイルにないタグは、Visual FoxPro は、他の複合インデックスを開いているファイルにタグを検索します。  
  
## <a name="see-also"></a>関連項目  
 [INDEX コマンド](../../odbc/microsoft/index-command.md)
