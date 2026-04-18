# Tv-player-
Tv-player
tv-player/
 ├── app/
 │    ├── src/main/java/com/example/tvplayer/MainActivity.java
 │    ├── src/main/AndroidManifest.xml
 │    └── res/
 ├── build.gradle
 ├── settings.gradle
 rootProject.name = "TVPlayer"
include ':app'
buildscript {
    repositories {
        google()
        mavenCentral()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:8.1.0'
    }
}
allprojects {
    repositories {
        google()
        mavenCentral()
    }
}
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.example.tvplayer'
    compileSdk 34

    defaultConfig {
        applicationId "com.example.tvplayer"
        minSdk 21
        targetSdk 34
    }

    buildTypes {
        release {
            minifyEnabled false
        }
    }
}

dependencies {
    implementation 'com.google.android.exoplayer:exoplayer:2.19.1'
}
<manifest xmlns:android="http://schemas.android.com/apk/res/android">

    <uses-feature android:name="android.software.leanback" android:required="true"/>

    <application
        android:label="TV Player">

        <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LEANBACK_LAUNCHER"/>
            </intent-filter>
        </activity>

    </application>

</manifest>
package com.example.tvplayer;

import android.net.Uri;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import com.google.android.exoplayer2.*;
import com.google.android.exoplayer2.ui.PlayerView;

public class MainActivity extends AppCompatActivity {

    private ExoPlayer player;

    String[] streams = {
        "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
    };

    int current = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        PlayerView view = new PlayerView(this);
        setContentView(view);

        player = new ExoPlayer.Builder(this).build();
        view.setPlayer(player);

        play();
    }

    void play() {
        MediaItem item = MediaItem.fromUri(Uri.parse(streams[current]));
        player.setMediaItem(item);
        player.prepare();
        player.play();
    }
}
