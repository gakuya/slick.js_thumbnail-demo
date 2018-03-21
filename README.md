# slick demo

slick.js(http://kenwheeler.github.io/slick/) でメイン画像とサムネイル画像を連動させているとき、サムネイル画像の数が少なく `arrows` オプションのナビゲーションが出ていない場合に良い感じに表示させるデモです。

## どんなとき？

メイン画像とサムネイル画像があり、次のようなオプション設定にした場合、サムネイル画像(.slick-thumbnail)が `slidesToShow` よりも多い数が(この場合4つ以上)あれば、`arrows` のナビゲーションが表示され、サムネイル画像はメイン画像の切り替えと連動してスライドします。

~~~
$('.slick-img').slick({
    autoplay: true,
    autoplaySpeed: 3000,
    slidesToShow: 1,
    slidesToScroll: 1,
    arrows: false,
    asNavFor: '.slick-thumbnail',
});

$('.slick-thumbnail').slick({
    slidesToShow: 3,
    slidesToScroll: 1,
    asNavFor: '.slick-img',
    pauseOnFocus: false,
    pauseOnHover: false,
    focusOnSelect: true,
    centerMode: true,
    centerPadding: 0,
});
~~~

しかし、サムネイル画像が `slidesToShow` と同数以下のとき、左右のサムネイルのコピーが作成されず `centerMode` オプションも無視されて最初にフォーカスの当たっているサムネイルは左端の画像になります。

更にメイン画像と連動してサムネイル画像がスライドする動作は残っているため、サムネイル画像はどんどん左に消えていってしまいます。

## どうする？

サムネイル画像の数が `slidesToShow` の設定値以下の場合、サムネイルはスライドさせずにフォーカスが切り替わるだけにします。

## 具体的な対応方法

メイン画像が切り替わる際(`beforeChange` イベント発生時)に、サムネイル部分(`.slick-thumbnail`)を再表示します。

再表示(refresh)を実行できるのは `slickSetOption` メソッドのみのようなので、適当なオプションを設定しています。

これによりサムネイル画像のフォーカスだけが切り替わり、画像の表示位置はリセットされるので、フォーカスだけが移動しているように見えます。

## サンプル画像について

サンプル画像はぱくたそ(https://www.pakutaso.com/)を利用しています。
