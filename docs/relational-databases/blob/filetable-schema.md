---
title: FileTable スキーマ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d5f53246717621e2482a352d25cf2a24fd24f2f3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125176"
---
# <a name="filetable-schema"></a>FileTable スキーマ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FileTable の定義済みスキーマおよび固定スキーマについて説明します。  
  
|ファイル属性の名前|型|サイズ|既定|[説明]|ファイル システムのアクセシビリティ|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|変数 (variable)|このアイテムの位置を識別する **hierarchyid** 。|階層 FileNamespace 内でのこのノードの位置。<br /><br /> テーブルの主キーです。|Windows パス値を設定することによって作成および変更できます。|  
|**stream_id**|**[一意の ID] rowguidcol**||**NEWID()** 関数によって返される値。|FILESTREAM データの一意の ID。|該当なし。|  
|**file_stream**|**varbinary(max)**<br /><br /> **ファイル ストリーム (filestream)**|変数 (variable)|NULL|FILESTREAM データが含まれています。|該当なし。|  
|**file_type**|**nvarchar (255)**|変数 (variable)|NULL。<br /><br /> ファイル システムの作成操作または名前変更操作によって、名前から取得されたファイル拡張子の値が格納されます。|ファイルの種類を表します。<br /><br /> この列は、フルテキスト インデックスの作成時に **TYPE 列** として使用できます。<br /><br /> **file_type** は、保存される計算列です。|自動的に計算されます。 設定することはできません。|  
|**[名前]**|**nvarchar (255)**|変数 (variable)|GUID 値。|ファイルまたはディレクトリの名前。|Windows API を使用して作成または変更できます。|  
|**parent_path_locator**|**hierarchyid**|変数 (variable)|このアイテムが格納されているディレクトリを識別する **hierarchyid** 。|格納されているディレクトリの **hierarchyid** 。<br /><br /> **parent_path_locator** は、保存される計算列です。|自動的に計算されます。 設定することはできません。|  
|**cached_file_size**|**bigint**|||FILESTREAM データのサイズ (バイト単位)。<br /><br /> **cached_file_size** は、保存される計算列です。|キャッシュされたファイル サイズは自動的に最新の状態に維持されますが、特殊な状況で同期がとれなくなる場合があります。 正確なサイズを計算するには、 **DATALENGTH()** 関数を使用します。|  
|**creation_time**|**datetime2(4)**<br /><br /> **NULL 以外**|8 バイト|現在の時刻|ファイルが作成された日付と時刻。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**last_write_time**|**datetime2(4)**<br /><br /> **NULL 以外**|8 バイト|現在の時刻|ファイルが最後に更新された日付と時刻。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**last_access_time**|**datetime2(4)**<br /><br /> **NULL 以外**|8 バイト|現在の時刻|ファイルが最後にアクセスされた日付と時刻。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_directory**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|行がディレクトリを表しているかどうかを示します。 この値は自動的に計算され、設定することはできません。|自動的に計算されます。 設定することはできません。|  
|**is_offline**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|オフライン ファイル属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_hidden**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|隠しファイル属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_readonly**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|読み取り専用ファイル属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_archive**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|アーカイブ属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_system**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|システム ファイル属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
|**is_temporary**|**bit**<br /><br /> **NULL 以外**|1 バイト|FALSE|一時ファイル属性。|自動的に計算されます。 Windows API を使用して設定することもできます。|  
  
## <a name="see-also"></a>参照  
 [FileTable の作成、変更、および削除](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  
