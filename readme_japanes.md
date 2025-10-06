# Your Project

BasketLiDAR: The First LiDAR-Camera Multimodal Dataset for Professional Basketball MOT

BasketLiDARの概要
～～何か～～
論文PDFのリンク(11月公開予定)を乗っけて、詳細はこちらとする。

Data visualization
～～カメラ画像とLiDARをタイリングした動画を乗っける～～
あとはpointcloudの画像もあったら乗せる。すぐ見つからなかったらあきらめる

Setup
conda環境でのセットアップを推奨
condaでの仮想環境作成方法
依存ライブラリのインストールのためにrequirements.txtを実行してねということを書く

Datasets
    Downloads（中のより小さい見出し）
    利用したかったらその目的を私たちに連絡して伝えてね。
    それが適切なものであると判断でき次第、google driveのリンクを送らせていただくので、そこからダウンロードしてくださいということを書く。
    フォルダ構成
    （データセットフォルダのディレクトリ構成をtreeで出力してのっける）

LiDAR-base-Tracking
～～Trackingした動画を乗っける～～
    lvx2点群ファイル(formatのPDFリンクを乗っける)の読み込み～鳥観図と物体検出ラベルの生成プロセスは
    pointcloud_to_BEV-detection.ipynbを参照と書く

    物体検出ラベルを入力としたTracking結果の生成プロセスは
    BEV-detection_to_track.ipynbを参照と書く。順次より詳細なマニュアルを追記予定とも（見出し分けしてもいいかも）

cam-fusion-Tracking
    camfusion_postprocess.ipynbを参照と書く。順次より詳細なマニュアルを追記予定とも
