# 手の関節情報とDTWを用いた手話動作の類似検索システム
## 概要
この研究では、検索された手話単語の映像を含む手話文章の動画をデータベースから検索するシステムの開発を目的としています。

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d275156b-155e-4757-8fb2-4b659528dd87/1ee49ff1-d6b0-4685-abd0-1d5ccb4992c3/Untitled.png)

このシステムにより、辞書に登録されていない単語についても、意味解析を補助することができます。

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d275156b-155e-4757-8fb2-4b659528dd87/137a4136-1681-48dc-9dd0-ebc8030b6ad7/Untitled.png)

具体的には、関節情報から抽出した特徴量を用いて、2つの手話映像の類似度を評価します。

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/d275156b-155e-4757-8fb2-4b659528dd87/7e834c89-725a-4117-a261-1c5c44b35dd3/02c6bae8-8e6d-4931-b4d3-7ef32b471727.png)

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
1. **p1_joint_from_video.py**を実行。動画フォルダと保存先フォルダ（**../data/handData/--/1_joint**）を指定し、関節位置データを作成。
2. **p2_smooth_joint.py**を実行。関節位置データフォルダと保存先フォルダ（**../data/handData/--/d3_smoothed_joint**）を選択し、平滑化済データを作成。
3. **p3_feature_from_joint.py**を実行。平滑化済データフォルダと保存先フォルダ（**../data/handData/--/d4_feature**）を選択し、手話特徴データを作成。
4. **p4_search_shuwa.py**を実行。検索手話と被検索手話の手話特徴データを選択し、時系列類似度推移データを作成・保存（**./result**）。
</pre>
- **p2_smooth_joint.py**では、線形補完と平滑化を行っています。予備実験で取得した線形補完済データを**../data/handData/--/d2_complemented_joint**に保存しています
- **handData**は検索手話を**key**、被検索手話を**tgt**として扱っています。


