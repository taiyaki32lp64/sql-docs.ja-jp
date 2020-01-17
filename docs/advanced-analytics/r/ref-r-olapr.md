---
title: olapR R 関数ライブラリ
description: SQL Server 2016 R Services での olapR 関数ライブラリと、SQL Server Machine Learning Services (R 付属) の概要について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 507bd04140880a3c15f1e72eed49c29ade56769c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715006"
---
# <a name="olapr-r-library-in-sql-server"></a>olapR (SQL Server の R ライブラリ)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**olapR** は、SQL Server Analysis Services OLAP キューブに対する MDX クエリに使用される、R 関数の Microsoft ライブラリです。 関数はすべての MDX 操作をサポートするわけではありませんが、ディメンションに対してスライス、ダイス、ドリルダウン、ロールアップ、およびピボットを行うクエリを作成できます。 

このパッケージは、R セッションに事前に読み込まれていません。 次のコマンドを実行してライブラリを読み込みます。

```R
library(olapR)
```

このライブラリは、すべてのサポート対象バージョンの SQL Server 上の Analysis Services OLAP キューブへの接続に使用できます。 現時点では、表形式モデルへの接続はサポートされていません。

## <a name="package-version"></a>パッケージ バージョン

すべての Windows 限定の製品、およびライブラリを提供するダウンロードにおける現行バージョンは 1.0.0 です。

## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**olapr** ライブラリは複数の Microsoft 製品に配布されていますが、SQL Server または別の製品のどちらからライブラリを入手しても、使用方法は同じです。 これらの関数は同じであるため、[個々の sqlrutils 関数のドキュメント](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr)は Microsoft Machine Learning Server の [R リファレンス](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="availability-and-location"></a>可用性と場所

このパッケージは、Azure 上の複数の仮想マシン イメージの他に、次の製品にも用意されています。 パッケージの場所はそれに応じて異なります。

Product | Location |
--------|----------|
SQL Server Machine Learning Services (R 統合あり) | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library | 
SQL Server 2016 R Services | C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library
Microsoft Machine Learning Server (R Server) | C:\Program Files\Microsoft\R_SERVER\library |
Microsoft R Client | C:\Program Files\Microsoft\R Client\R_SERVER\library |
Data Science Virtual Machine (Azure 上) | C:\Program Files\Microsoft\R Client\R_SERVER\library |
SQL Server Virtual Machine (Azure 上) <sup>1</sup> | C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library |

<sup>1</sup> R 統合は SQL Server では省略可能です。 olapR ライブラリは、VM の構成中に Machine Learning または R 機能を追加するとインストールされます。


## <a name="see-also"></a>参照

[olapR を使って MDX クエリを作成する方法](how-to-create-mdx-queries-using-olapr.md)
