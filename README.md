# Pano360
[![Build Status](https://travis-ci.org/Martin20150405/Pano360.svg?branch=master)](https://travis-ci.org/Martin20150405/Pano360) [![license](https://img.shields.io/github/license/mashape/apistatus.svg)](LECENSE) [![](https://jitpack.io/v/Martin20150405/Pano360.svg)](https://jitpack.io/#Martin20150405/Pano360)  ![progress](http://progressed.io/bar/62?title=Progress)

Pure Java library to play 360 degree panorama video (VR video) on Android. Using OpenGL ES 2.0 
  
Pano 360は、Androidプラットフォーム上の純粋なJavaパノラマ（360度/ VR）ビデオ再生ライブラリで、ビデオレンダリングにOpenGL ES 2.0を使用し、サードパーティのライブラリは使用されません。

**Demo App [ここ](https://raw.githubusercontent.com/Martin20150405/Pano360/master/pano360demo/release/pano360demo-release.apk)~**

### Read this in other languages: [English](README.en.md)

## [一連のチュートリアル：Androidプラットフォームでパノラマ動画プレーヤーを最初から作成する](http://blog.csdn.net/Martin20150405/article/details/53149578)


## プラットフォーム要件
* OpenGL ES 2.0 
* Android 4.0.3 (API-15) 以上

## 特徴
* シングルおよびデュアル画面切り替え
* ジャイロ、タッチ（ドラッグ、ズーム）2つのインタラクティブモード切り替え
* 進行状況コントロールを再生します。コントロールバーは自動的に非表示になります
* GPUImageフィルターグループと同様に、重ねられた複数のフィルターをサポートします。フィルターの順序は、球体へのレンダリングの前でも後でもかまいません。
* オリジナルのビデオレンダリングをサポート（フルスクリーン/カット/アダプティブ）
* パノラマ写真の再生をサポート
* リアルタイムのビデオスクリーンショット
* オンラインビデオ再生（複数の形式のデコードの問題を自分で処理する必要がある場合があります）
* 座標軸のロックをサポートし、ユーザーはさまざまな角度から入り、同じシーンを見ることができます
     * ** LOCK_MODE_AXIS_Y **：Cardboard Motionと同様
* 座標軸の回転角度を無視するサポート
* 2DビデオVRシネマモード
* シンプルなホットスポットをサポート（写真/ビデオ）

## スクリーンショット
![ScreenShot](https://github.com/Martin20150405/Pano360/blob/master/screenshots/player_screen.png)

[**Youtube**](https://youtu.be/kTJfI_dRLUk)
[**youku**](http://v.youku.com/v_show/id_XMjY4ODI4OTM3Mg==?spm=a2h3j.8428770.3416059.1)

## 適切
* Androidプラットフォームでパノラマ動画プレーヤーを実装する方法に興味がある場合、または再生コントロール機能付きのパノラマ動画プレーヤーを使いたい場合、またはパノラマ動画プレーヤーにさまざまな奇妙な機能を追加する場合は、このプロジェクトが 手伝います。

## 使い方
	allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
	dependencies {
	        compile 'com.github.Martin20150405.Pano360:vrlib:v1.1.2'
	}
	
* ライブラリを使用するには2つの方法があります。詳細については、デモアプリを参照してください。  

* 1行のコードで使用`Activity`  （クラスライブラリが提供）
```java
Pano360ConfigBundle.newInstance().setFilePath(filePath).startEmbeddedActivity(this);
```

* `GLSurfaceView`を提供します。どこでも使用できますが、再生コントロールとモード切り替えを自分で処理する必要があります
```java
<android.opengl.GLSurfaceView
    android:id="@+id/surface_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```
```java
GLSurfaceView glSurfaceView=(GLSurfaceView) findViewById(R.id.surface_view);
panoViewWrapper =PanoViewWrapper.with(this)
		.setConfig(configBundle)
		.setGlSurfaceView(glSurfaceView)
		.init();
glSurfaceView.setOnTouchListener(new View.OnTouchListener() {
	@Override
	public boolean onTouch(View v, MotionEvent event) {
		return panoViewWrapper.handleTouchEvent(event);
	}
});
@Override
protected void onPause(){
	super.onPause();
	panoViewWrapper.onPause();
}

@Override
protected void onResume(){
	super.onResume();
	panoViewWrapper.onResume();
}

@Override
protected void onDestroy(){
	super.onDestroy();
	panoViewWrapper.releaseResources();
}
```

## 将来の機能（あまり期待しないでください-|||）
* 加速度+電子コンパスのサポート（ジャイロスコープのない携帯電話に適しています）
* IjkMediaPlayerなどの使用するデコーダーをすばやく切り替える
* 小さなウィンドウ/フラグメントの再生
* ハンドラ+ MessageQueue
* さまざまなパノラマ形式
* ホットスポットサポート（ホットスポット）、ヘッドコントロールサポート
* アンチディストーション
* RTSP RTMP（VLC / Vitamio付き）
* 完全な再生制御機能
* ビデオ録画/トランスコーディング/倍速再生（Mediacodec / ffmpeg）

## [過去のバージョン](https://github.com/Martin20150405/Pano360/releases)

## [更新ログ](https://github.com/Martin20150405/Pano360/wiki/ChangeLog)



## フィードバック

* 問題を開く
* martin20150405@163.comにメールを送信
* このプロジェクトがあなたに役立つと思われる場合は、スターを歓迎し、一緒にこのプロジェクトを改善することを歓迎します
