---
title: プロジェクトの設定 (型のマッピング) (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access data types
- data types, default mappings
- default data type mappings
- Project Settings dialog box, Type Mapping
- SQL Server data types
- Type Mapping settings
ms.assetid: b87b9683-abed-4677-8c50-18bdba704655
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 01154cf477435e9dc5335606d0c11a05aecc492b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066658"
---
# <a name="project-settings-type-mapping-accesstosql"></a>プロジェクトの設定 (型のマッピング) (AccessToSQL)
プロジェクトの型マッピングの設定では、SSMA プロジェクトの既定の型マッピングを設定できます。 個々 のデータベース オブジェクトの型のマッピングを指定することもできます。 詳細については、次を参照してください。[マッピング ソースとターゲットのデータ型](mapping-source-and-target-data-types-accesstosql.md)します。  
  
型のマッピングが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   使用して、**プロジェクト設定**ダイアログ ボックスを現在のプロジェクトの構成オプションを設定します。 型マッピングの設定にアクセスする、**ツール**メニューの **プロジェクト設定**、順にクリックします**型マッピング**左側のウィンドウでします。  
  
-   使用して、**プロジェクト設定の既定の**ダイアログ ボックスをすべてのプロジェクトの構成オプションを設定します。 型マッピングの設定にアクセスする、**ツール**メニューの **プロジェクト設定の既定の**、設定は、表示/から変更する必要を移行プロジェクトの種類を選択します **。移行のターゲット バージョン**ドロップダウンをクリックし、**型マッピングの**左側のウィンドウでします。  
  
## <a name="options"></a>および  
**変換元の型**  
Access データ型にマップします。  
  
**ターゲットの種類**  
ターゲット[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または指定したアクセスのデータ型の SQL Azure のデータ型。  
  
次の表では、ソースとターゲットのデータ型の既定のマッピングを示します。  
  
|Access データ型|SQL Server データ型|  
|--------------------|------------------------|  
|**binary[\*..\*]**|**varbinary[\*]**|  
|**boolean**|**bit**|  
|**byte**|**tinyint**|  
|**currency**|**money**|  
|**date**|**datetime**|  
|**decimal**|**float**|  
|**double**|**float**|  
|**guid**|**uniqueidentifier**|  
|**整数 (integer)**|**smallint**|  
|**long**|**int**|  
|**longbinary**|**varbinary(max)**|  
|**memo**|**nvarchar(max)**|  
|**メモ**- Access 97|**varchar(max)**|  
|**single**|**real**|  
|**text[\*..\*]**|**nvarchar[\*]**|  
|**テキスト [\*..\*]** - Access 97|**varchar[\*]**|  
  
**[追加]**  
データ型をマッピングの一覧に追加する をクリックします。  
  
**[編集]**  
データ型マッピングのリストを編集する をクリックします。  
  
**[削除]**  
マッピングの一覧から選択したデータ型のマッピングを削除する をクリックします。  
  
**既定値にリセット**  
すべてのデータ型マッピングを SSMA の既定値にリセットする をクリックします。  
  
## <a name="see-also"></a>参照  
[ソースとターゲットのデータ型のマッピング](mapping-source-and-target-data-types-accesstosql.md)  
[ユーザー インターフェイスの Reference(Access)](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
