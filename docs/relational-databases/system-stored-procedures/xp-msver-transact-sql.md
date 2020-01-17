---
title: xp_msver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 85552daa2dda14c6a7516c96f0f9fe6566f31111
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843897"
---
# <a name="xp_msver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関するバージョン情報を返します。 また**xp_msver**は、サーバーの実際のビルド番号とサーバー環境に関する情報も返します。 **Xp_msver**返される情報は、プラットフォームに依存しないコードのロジックを強化するために、[!INCLUDE[tsql](../../includes/tsql-md.md)] のステートメント、バッチ、ストアドプロシージャなどで使用できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>引数  
 *optname*  
 オプション名を指定します。次のいずれかの値を指定できます。  
  
|オプション/列名|[説明]|  
|-------------------------|-----------------|  
|**ProductName**|製品名;たとえば、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]です。|  
|**ProductVersion**|製品バージョン。|  
|**[言語]**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の言語バージョン。|  
|**プラットフォーム**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターのオペレーティングシステム名、製造元名、およびチップファミリ名。|  
|**コメント**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関するその他の情報。|  
|**仕入**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を生成する会社名たとえば、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation のようになります。|  
|**FileDescription**|オペレーティング システム。|  
|**FileVersion**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 実行可能ファイルのバージョン。|  
|**InternalName**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の [!INCLUDE[msCoName](../../includes/msconame-md.md)] 内部名です。たとえば、SQLSERVR.EXE です。|  
|**LegalCopyright**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に必要な著作権に関する法的情報。Copyright&#xA9; [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005 などです。|  
|**LegalTrademarks**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に必要な商標に関する法的情報。 たとえば、[!INCLUDE[msCoName](../../includes/msconame-md.md)] は [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation の登録商標です。|  
|**OriginalFilename**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に実行されるファイル名。Sqlservr.exe などです。|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**特殊ビルド**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**WindowsVersion**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] を実行しているコンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows のバージョン。|  
|**ProcessorCount**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターのプロセッサ数。|  
|**ProcessorActiveMask**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターに搭載されているプロセッサ。[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows により起動され、使用されます。|  
|**ProcessorType**|プロセッサの種類。 **プラットフォーム**に似ています。|  
|**PhysicalMemory**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターに搭載されている RAM の容量 (mb)。|  
|**製品 ID**|プロダクト ID (PID) 番号。 これは、インストール時に指定します。 この番号は、元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CD ケースのステッカーに記載されています。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 1 (成功)  
  
## <a name="result-sets"></a>結果セット  
 パラメーターを指定せずに**xp_msver**は、すべてのオプション値を一覧表示する4列の結果セットを返します。 **xp_msver**、任意のパラメーターについて、4列の結果セットをそのオプションの値と共に返します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [汎用拡張ストアドプロシージャ&#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION &#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
