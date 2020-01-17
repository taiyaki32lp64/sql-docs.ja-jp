---
title: プロジェクトの設定 (型のマッピング) (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2698fb3a-f9e6-4e04-94e0-dad289d7ed0a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d7b16bdf3717fa14f91af41663cbd65365eac52a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028660"
---
# <a name="project-settings-type-mapping-sybasetosql"></a>プロジェクトの設定 (型のマッピング) (SybaseToSQL)
[型マッピング] ページ、**プロジェクト設定** ダイアログ ボックスには、SSMA に Sybase Adaptive Server Enterprise (ASE) のデータ型に変換する方法をカスタマイズする設定が含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
型マッピング ページが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   今後のすべての SSMA プロジェクトの型マッピングの設定を指定する、**ツール**メニューの **プロジェクト設定の既定の**設定は表示に必要な移行プロジェクトの種類を選択しますまたは。変更**移行ターゲット バージョン**ドロップダウンを選択し、**型マッピングの**左側のウィンドウの下部にあります。  
  
-   現在のプロジェクトの設定を指定する、**ツール**メニューの **プロジェクト設定**、し、**型マッピングの**左側のウィンドウの下部にあります。  
  
## <a name="options"></a>および  
**変換元の型**  
マップされた ASE データ型。  
  
**ターゲットの種類**  
ターゲット[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE の指定したデータ型のデータ型。  
  
SSMA for Sybase の型マッピングの既定の次のセクションの表を参照してください。  
  
**[追加]**  
データ型をマッピングの一覧に追加する をクリックします。  
  
**[編集]**  
マッピングの一覧で選択したデータ型を編集する をクリックします。  
  
**[削除]**  
マッピングの一覧から選択したデータ型のマッピングを削除する をクリックします。  
  
**既定値にリセット**  
SSMA の既定値に型マッピングのリストをリセットする をクリックします。  
  
## <a name="default-type-mapping"></a>既定の型マッピング  
次の表に、ASE の既定の型マッピングと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
|ASE のデータ型|SQL Server データ型|  
|-----------------|------------------------|  
|**bigint**|**bigint**|  
|**[バイナリ]**|**[バイナリ]**|  
|**binary[\*..8000]**|**binary[\*]**|  
|**binary[8001..\*]**|**varbinary(max)**|  
|**bit**|**bit**|  
|**char**|**char**|  
|**char varying**|**varchar**|  
|**character varying [\*..8000]**|**varchar[\*]**|  
|**character varying [8001...\*]**|**varchar(max)**|  
|**char [\*..8000]**|**char[\*]**|  
|**char[8001..\*;]**|**varchar(max)**|  
|**character**|**char**|  
|**character varying**|**varchar**|  
|**character varying [\*..8000]**|**varchar[\*]**|  
|**character varying [8001...\*]**|**varchar(max)**|  
|**character[\*..8000]**|**char[\*]**|  
|**character[8001..\*]**|**varchar(max)**|  
|**date**|**date**|  
|**datetime**|**datetime2[3]**|  
|**dec**|**decimal**|  
|**dec[\*..\*]**|**decimal[\*]**|  
|**dec[\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**decimal**|**decimal**|  
|**decimal[\*..\*]**|**decimal[\*]**|  
|**decimal [\*..\*][\*..\*]**|**decimal[\*][\*]**|  
|**double precision**|**float[53]**|  
|**float**|**float[53]**|  
|**float[\*..15]**|**float[24]**|  
|**float [16..\*]**|**float[53]**|  
|**image**|**image**|  
|**int**|**int**|  
|**integer**|**int**|  
|**longsysname**|**nvarchar[255]**|  
|**money**|**money**|  
|**national char**|**nchar**|  
|**national char [\*..4000]**|**nchar[\*]**|  
|**varying、national char**|**nvarchar**|  
|**varying、national char [\*..4000]**|**nvarchar[\*]**|  
|**varying、national char [4001...\*]**|**nvarchar(max)**|  
|**national char [4001...\*]**|**nvarchar(max)**|  
|**national character**|**nchar**|  
|**national character [\*..4000]**|**nchar[\*]**|  
|**national character [4001...\*]**|**nvarchar(max)**|  
|**national character varying**|**nvarchar**|  
|**national character varying [\*..4000]**|**nvarchar[\*]**|  
|**national character varying [4001...\*]**|**nvarchar(max)**|  
|**national varchar**|**nvarchar**|  
|**national varchar [\*..4000]**|**nvarchar[\*]**|  
|**national varchar [4001...\*]**|**nvarchar(max)**|  
|**nchar**|**nchar**|  
|**nchar varying**|**nvarchar**|  
|**nchar varying [\*..4000]**|**nvarchar[\*]**|  
|**nchar varying [4001...\*]**|**nvarchar(max)**|  
|**nchar[\*..4000]**|**nchar[\*]**|  
|**nchar[4001..\*]**|**nvarchar(max)**|  
|**numeric**|**numeric**|  
|**numeric[\*..\*]**|**numeric[\*]**|  
|**numeric[\*..\*][\*..\*]**|**numeric[\*][\*]**|  
|**nvarchar**|**nvarchar**|  
|**nvarchar[\*..4000]**|**nvarchar[\*]**|  
|**nvarchar[4001..\*]**|**nvarchar(max)**|  
|**real**|**float[24]**|  
|**smalldatetime**|**smalldatetime**|  
|**smallint**|**smallint**|  
|**smallmoney**|**smallmoney**|  
|**sysname**|**nvarchar[128]**|  
|**sysname[\*..\*]**|**nvarchar[255]**|  
|**text**|**text**|  
|**time**|**time[3]**|  
|**timestamp**|**rowversion**|  
|**tinyint**|**tinyint**|  
|**unichar**|**nchar**|  
|**unichar varying**|**nvarchar**|  
|**unichar varying [\*..4000]**|**nvarchar[\*]**|  
|**unichar varying [4001....\*]**|**nvarchar(max)**|  
|**unichar[\*..4000]**|**nchar[\*]**|  
|**unichar[4001..\*]**|**nvarchar(max)**|  
|**unitext**|**nvarchar(max)**|  
|**univarchar**|**nvarchar**|  
|**univarchar[\*..4000]**|**nvarchar[\*]**|  
|**univarchar[4001..\*]**|**nvarchar(max)**|  
|**unsigned bigint**|**numeric[20][0]**|  
|**unsigned int**|**bigint**|  
|**unsigned smallint**|**int**|  
|**unsigned tinyint**|**tinyint**|  
|**varbinary**|**varbinary**|  
|**varbinary[\*..8000]**|**varbinary[\*]**|  
|**varbinary[8001..\*]**|**varbinary(max)**|  
|**varchar**|**varchar**|  
|**varchar[\*..8000]**|**varchar[\*]**|  
|**varchar[8001..\*]**|**varchar(max)**|  
  
