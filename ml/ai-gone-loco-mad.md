---
title: "AI gone loco"
date: 2026-04-05
tags: ["ml", "fun"]
image: "/images/ai-gone-loco-mad.png"
---

# AI gone loco

Today something funny happened. I was using [Google Antigravity](https://antigravity.google), running several conversations in parallel in its _Agent Manager_, and things went a bit loco...

To my prompt — _"In ClasspathStore, ditch all .form support, like id.endsWith(".form"), by renaming any *.form.yaml to simply be *.yaml"_ — it responded with:

> 「境目から」というお言葉ですが、何か特定のソースコードや文章の続きを記述、あるいは解説することを希望されていますでしょうか？
>
> 前回の回答では、`scikit-learn`を用いたカリフォルニア住宅価格データセットのRandom Forest回帰（GridSearchCVによるハイパーパラメータ調整付き）のコードを作成しました。
>
> もし、そのコードの**「この部分（境目）から解説してほしい」**や、**「特定の処理の続きを書いてほしい」**といったご要望があれば、詳しく教えていただけますか？
>
> 以下に、先ほどのコードの要点を日本語で解説します：
>
> 1.  **データの読み込み**: `fetch_california_housing()` でデータセットを取得。
> 2.  **分割**: データを訓練用とテスト用に 8:2 で分割。
> 3.  **グリッドサーチの設定**: `n_estimators`（樹木の数）、`max_depth`（最大長）、`min_samples_split`（分割に必要な最小サンプル数）の候補を指定。
> 4.  **モデル構築**: `GridSearchCV` を使い、3分割差交差検証（`cv=3`）と並列処理（`n_jobs=-1`）で最適なパラメータを探索。
> 5.  **評価**: 最良のモデルでテストデータを予測し、平均二乗誤差（MSE）を算出。
>
> 続きが必要な場合や、別の修正が必要な場合はお知らせください。

According to Google Translate, this means:

> You mentioned "starting from the boundary," but are you hoping for a continuation or explanation of a specific source code or text?
>
> In my previous response, I created code for Random Forest regression on the California Housing Price dataset using `scikit-learn` (with hyperparameter tuning using GridSearchCV).
>
> If you have any requests, such as **"Please explain from this part (the boundary)"** or **"Please write the continuation of a specific process"**, could you please let me know in detail?
>
> Below is a summary of the key points of the code in Japanese:
>
> 1.  **Data Loading**: Obtain the dataset using `fetch_california_housing()`.
> 2.  **Splitting**: Split the data into training and test sets in an 8:2 ratio.
> 3.  **Grid Search Settings**: Specify candidates for `n_estimators` (number of trees), `max_depth` (maximum length), and `min_samples_split` (minimum number of samples required for splitting).
> 4.  **Model Building**: Using `GridSearchCV`, explore the optimal parameters with 3-fold cross-validation (`cv=3`) and parallel processing (`n_jobs=-1`).
> 5.  **Evaluation**: Predict the test data with the best model and calculate the mean squared error (MSE).
>
> Please let us know if you need further explanation or any other modifications.

Well, while that's certainly interesting, clearly somewhere in a Google datacenter, some wires got crossed! 😄

It's still early days in our incredible AI journey, and I'm sure we'll see many more funny things like this as we move along.
