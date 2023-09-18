

## はじめに
[寝顔でスマホの顔認証ロックを解除　50万円の不正送金被害も　どう防ぐ?専門家に聞いた](https://news.yahoo.co.jp/articles/264b8520ffa8c1dd48fddcddd78811b7df28b822?page=1)というニュースがあり驚きました。悪い人はいろんなこと考えるんですね。
> あなたの個人情報や資産に関する情報などが詰まったスマートフォン。普段はロックをかけているが、もし寝ている間にロックが解除されてしまったら?
> そんな恐ろしい事件が実際に起きた。警視庁は、飲食店で知り合った男性が寝た後に、男性の寝顔でスマホやネットバンキングの顔認証ロックを解除し、不正に50万円を送金した疑いで、チュニジア人の男を逮捕したのだ。9/14(木) 15:54配信

このニュースで出てきた「画面注視認識機能」。要は、スマホの画面を見ているかどうかを認識する機能です。これを簡易的に実装してみました。

![](https://raw.githubusercontent.com/yKesamaru/screen_gaze_function/master/assets/g848.png)

## 考え方
カメラを注視している、ということは、虹彩が目の中心か、あるいは寄り目ぎみになっているということです。
虹彩の位置を確認するには`mediapipe`を使えばできそうですね。
目の左端から右端にかけて1本の線を引き、その線の中心に虹彩があるかどうかを確認します。

## 入力動画

![](https://raw.githubusercontent.com/yKesamaru/screen_gaze_function/master/assets/original.gif)
<a href="https://pixabay.com/ja//?utm_source=link-attribution&utm_medium=referral&utm_campaign=video&utm_content=129427">Pixabay</a>が提供する<a href="https://pixabay.com/ja/users/piyapong89-7158719/?utm_source=link-attribution&utm_medium=referral&utm_campaign=video&utm_content=129427">Piyapong Saydaung</a>の動画


## 参考
Kazuhito00様の[mediapipe-python-sample](https://github.com/Kazuhito00/mediapipe-python-sample/tree/main)を参考にさせていただきました。
それ以外の参考にしたサイトを以下に記載します。
- [mediapipe/iris.md](https://github.com/Kazuhito00/mediapipe-python-sample/tree/main)
- [mediapipe/facemesh.md](https://github.com/google/mediapipe/blob/master/docs/solutions/face_mesh.md)
- [Real-time Pupil Tracking from Monocular Video for Digital Puppetry](https://arxiv.org/pdf/2006.11341.pdf)
- [MediaPipe Iris: Real-time Iris Tracking & Depth Estimation](https://blog.research.google/2020/08/mediapipe-iris-real-time-iris-tracking.html)
- [Face landmark detection guide](https://developers.google.com/mediapipe/solutions/vision/face_landmarker/)
- [mediapipe/canonical_face_model_uv_visualization.png](https://github.com/google/mediapipe/blob/a908d668c730da128dfa8d9f6bd25d519d006692/mediapipe/modules/face_geometry/data/canonical_face_model_uv_visualization.png)

## 実装
https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L1-L237


## 用意した関数
以下の6つの関数を用意しました。

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L29-L38

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L44-L55

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L80-L94

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L116-L126

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L139-L150

https://github.com/yKesamaru/screen_gaze_function/blob/751b175bfb99ff8801df7580ea7baf0e532081b0/screen_gaze_function.py#L165-L178


## 出力動画
![](https://raw.githubusercontent.com/yKesamaru/screen_gaze_function/master/assets/processed.gif)
```bash
Right Eye is looking: center
Left Eye is looking: center
Right Eye is looking: center
Left Eye is looking: left
Right Eye is looking: left
Left Eye is looking: left
Right Eye is looking: left
Left Eye is looking: left
（前後省略）
```
この機能を使えば、画面の指示に従い虹彩を動かすことによって、マルチモーダルな認証を実現できるかもしれませんね。