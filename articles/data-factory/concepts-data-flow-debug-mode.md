---
title: Azure Data Factory Mapping Data Flow のデバッグ モード
description: データ フローの構築時に対話型デバッグ セッションを開始する
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 10/04/2018
ms.openlocfilehash: 567f64b8b720588807caeb5e49bae15f14c5b0a7
ms.sourcegitcommit: d2329d88f5ecabbe3e6da8a820faba9b26cb8a02
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2019
ms.locfileid: "56329798"
---
# <a name="mapping-data-flow-debug-mode"></a>Mapping Data Flow のデバッグ モード

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

Azure Data Factory Mapping Data Flow にはデバッグ モードがあり、デザイン サーフェスの上部にある [デバッグ] ボタンを使って有効にすることができます。 データ フローを設計するときにデバッグ モードを有効に設定すると、データ フローの構築およびデバッグ時にデータ シェイプの変換を対話的に監視できます。

<img src="media/data-flow/debugbutton.png" width="400">

## <a name="overview"></a>概要
デバッグ モードが有効なときは、実行中の Azure Databricks の対話型クラスターを使用して対話的にデータ フローを構築します。 Azure Data Factory でデバッグを無効にすると、セッションは終了します。 デバッグ セッションを有効にしている間に Azure Databricks によって発生する 1 時間あたりの料金を把握しておく必要があります。

ほとんどの場合、デバッグ モードでデータ フローを構築し、ビジネス ロジックを検証してデータ変換を確認してから、Azure Data Factory で作業内容を公開することをお勧めします。

## <a name="debug-mode-on"></a>デバッグ モードの有効化
デバッグ モードを有効にすると、サイドパネル フォームが表示され、対話型の Azure Databricks クラスターを指定し、ソース サンプリングのオプションを選択するように求められます。 Azure Databricks の対話型クラスターを使用して、各ソース変換からサンプリング サイズを選択するか、テスト データに使用するテキスト ファイルを選択する必要があります。

<img src="media/data-flow/upload.png" width="400">

> [!NOTE]
>デバッグ モードで Data Flow を実行している場合、データはシンク変換に書き込まれません。 デバッグ セッションは、変換のテスト ハーネスとして機能することを目的としています。 シンクはデバッグ中には必要ではなく、データ フローでは無視されます。 シンクへのデータの書き込みをテストする場合は、Azure Data Factory パイプラインから Data Flow を実行し、パイプラインからデバッグの実行を使用します。

## <a name="debug-settings"></a>デバッグ設定
デバッグ設定は Data Flow から各ソースに行うことができます。デバッグ設定はサイド パネルに表示され、Data Flow のデザイン ツールバーで [ソースの設定] を選択して編集することもできます。 ここで、各ソース変換に使用する制限やファイル ソースを選択できます。 また、デバッグに使用する Databricks クラスターを選択することもできます。

## <a name="cluster-status"></a>クラスターの状態
デザイン サーフェスの上部にはクラスター状態インジケーターがあり、クラスターのデバッグの準備が整うと緑色に変わります。 クラスターが既に実行されている場合、緑色のインジケーターはほぼ瞬時に表示されます。 デバッグ モードを開始したときにクラスターがまだ実行されていなかった場合は、クラスターが起動するまで 5 分から 7 分待つ必要があります。 準備ができるまでインジケーターのライトは黄色になります。 クラスターが Data Flow のデバッグを実行する準備が整うと、インジケーターのライトは緑色に変わります。

デバッグが終了したら、[デバッグ] スイッチをオフにして、Azure Databricks クラスターを終了できるようにします。

<img src="media/data-flow/datapreview.png" width="400">

## <a name="data-preview"></a>データのプレビュー
デバッグが有効な場合、下部のパネルに [Data Preview]\(データのプレビュー\) タブが表示されます。 デバッグが有効ではない場合、Data Flow では、各変換に含まれる、または含まれない現在のメタデータのみが [Inspect]\(検査\) タブに表示されます。データのプレビューでは、リソース設定で制限として設定した行数のみのクエリが実行されます。 データのプレビューを更新するには、[Fetch data]\(データのフェッチ\) をクリックする必要があります。

<img src="media/data-flow/stats.png" width="400">

## <a name="data-profiles"></a>データのプロファイル
[Data Preview]\(データのプレビュー\) タブで個々の列を選択すると、データ グリッドの右端にグラフがポップアップ表示され、各フィールドに関する詳細な統計情報が示されます。 Azure Data Factory では、表示するグラフの種類のデータ サンプリングに基づいて判断が下されます。 カーディナリティが高いフィールドの既定は NULL/NOT NULL グラフです。一方、カーディナリティが低いカテゴリ データや数値データでは、データ値の頻度を示す棒グラフが表示されます。 また、文字列フィールドの最大/長さ、数値フィールドの最小/最大値、標準偏差、百分位、カウント、および平均も表示されます。 

<img src="media/data-flow/chart.png" width="400">
