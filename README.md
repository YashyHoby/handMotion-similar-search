# 手の関節情報とDTWを用いた手話動作の類似検索システム
## 概要
この研究では、検索された手話単語の映像を含む手話文章の動画をデータベースから検索するシステムの開発を目的としています。

![手話動画類似検索1](https://github.com/YashyHoby/handMotion-similar-search/assets/145910837/3792cbb5-bf4e-459d-869c-5504ab8ad631)

このシステムにより、辞書に登録されていない単語についても、意味解析を補助することができます。

![手話動画類似検索2](https://github.com/YashyHoby/handMotion-similar-search/assets/145910837/9f74438f-545b-4ef5-bfee-af6154492f08)

具体的には、関節情報から抽出した特徴量を用いて、2つの手話映像の類似度を評価します。

![手話動画類似検索3](https://github.com/YashyHoby/handMotion-similar-search/assets/145910837/22073f82-3593-48a9-9bfb-43b9ef73d9b7)

## コードの概要
<pre>
<code>
project
+---main_app
|   |   p1_joint_from_video.py      # 動画データから関節位置データを取得
|   |   p2_smooth_joint.py          # 関節情報を平滑化
|   |   p3_feature_from_joint.py    # 関節位置データから手話特徴データを作成
|   |   p4_search_shuwa.py          # Dynamic Time Warpingアルゴリズムを用いて類似度を計算
|   |   p_adjustment_cost_TH.py     # 計算に用いる閾値を調整
|   |   p_gui.py                    # GUI処理
|   |
|   +---result
|   |   |   # 類似検索結果（png）
|   |   |
|   |   +---path
|   |   |       # DTWの出力結果（png）
|   |   |
|   |   \---values
|   |           # 計算に用いたパラメータ（txt）
|   |
|   +---similar_sections
|   |       # 出力に描画する類似区間の情報（png）
|   |
|   \---values
|           # 計算に用いるパラメータ（txt）
|
+---tool_app
|       mediapipe_video_player.py   # メディアパイプを挺起用した動画再生
|       video_player.py             # 動画再生
|
\---utility_app
        my_functions.py             # 汎用関数
</code>
</pre>

## 実験の流れ
<pre>
1. <b>p1_joint_from_video.py</b>を実行。動画フォルダと保存先フォルダ（<b>../data/handData/--/1_joint</b>）を指定し、関節位置データを作成。
2. <b>p2_smooth_joint.py</b>を実行。関節位置データフォルダと保存先フォルダ（<b>../data/handData/--/d3_smoothed_joint</b>）を選択し、平滑化済データを作成。
3. <b>p3_feature_from_joint.py</b>を実行。平滑化済データフォルダと保存先フォルダ（<b>../data/handData/--/d4_feature</b>）を選択し、手話特徴データを作成。
4. <b>p4_search_shuwa.py</b>を実行。検索手話と被検索手話の手話特徴データを選択し、時系列類似度推移データを作成・保存（<b>./result</b>）。
</pre>
- **p2_smooth_joint.py**では、線形補完と平滑化を行っています。予備実験で取得した線形補完済データを**../data/handData/--/d2_complemented_joint**に保存しています
- **handData**は検索手話を**key**、被検索手話を**tgt**として扱っています。


