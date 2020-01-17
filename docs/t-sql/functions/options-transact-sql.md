---
title: '@@OPTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e33ca6d8afdb7aa9245bbdc6b0ad225dcd00dade
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982470"
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;OPTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在の SET オプションに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>戻り値の型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 オプションは、**SET** コマンドの使用または **sp_configure ユーザー オプション**値からのものです。 **SET** コマンドで構成されているセッション値は、**sp_configure** オプションをオーバーライドします。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] などの多数のツールによって SET オプションは自動的に構成されます。 各ユーザーには、構成を表す @@OPTIONS 関数が用意されます。  
  
 SET ステートメントを使用することにより、特定のユーザー セッションの言語とクエリ処理オプションを変更できます。 **\@\@OPTIONS** では、ON または OFF に設定されたオプションのみを検出できます。  
  
 **\@\@OPTIONS** 関数によって、10 進数の整数に変換された、オプションのビットマップが返されます。 ビット設定は、「[user options サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)」トピックで説明されている場所に格納されます。  
  
 **\@\@OPTIONS** 値をデコードするには、 **\@\@OPTIONS** によって返された整数をバイナリに変換し、その値を「[user options サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)」の表で検索します。 たとえば、`SELECT @@OPTIONS;` によって値 `5496` が返された場合、Windows のプログラマ電卓 (**calc.exe**) を使用して、10 進数の `5496` をバイナリに変換します。 結果は `1010101111000`です。 右端の文字 (バイナリ 1、2、および 4) は 0 で、テーブル内の最初の 3 つの項目がオフであることを示します。 表を見ると、これらは **DISABLE_DEF_CNST_CHK**、**IMPLICIT_TRANSACTIONS**、**CURSOR_CLOSE_ON_COMMIT** であることがわかります。 次の項目 (`1000` 位置の **ANSI_WARNINGS**) はオンです。 ビットマップを左へ、オプションの一覧を下へ見ていきます。 左端のオプションが 0 の場合、これらは型変換によって切り捨てられています。 ビットマップ `1010101111000` は実際は `001010101111000` であり、全部で 15 個のオプションを表しています。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 変更が動作に与える影響の例  
 次の例では、**CONCAT_NULL_YIELDS_NULL** オプションの 2 つの異なる設定による連結動作の違いを示します。  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. クライアントの NOCOUNT 設定のテスト  
 次の例では、`NOCOUNT``ON` を設定し、`@@OPTIONS` の値を調べます。 `NOCOUNT``ON` オプションは、セッションで実行するすべてのステートメントごとに、要求するクライアントに対して影響を受ける行数に関するメッセージを戻さないようにします。 `@@OPTIONS` の値は、`512` (0x0200) に設定されます。 これは NOCOUNT オプションを表します。 この例では、クライアントで NOCOUNT オプションが有効になっているかどうかを調べます。 たとえば、これはクライアントにおけるパフォーマンスの違いを調べるのに役立ちます。  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>参照  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [user options サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
