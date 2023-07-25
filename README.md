# TorangAndroidConvention

settings
```
pluginManagement {
    repositories {
        google()
        mavenCentral()
        gradlePluginPortal()
    }
}
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}

rootProject.name = "Feed(프로젝트명)"
include ':app'
include ':library'
```


라이브러리
```
plugins {
    id 'com.android.library'
    id 'kotlin-android'
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

android {
    compileSdk rootProject.compileSdk

    defaultConfig {
        minSdk rootProject.minSdk
        targetSdk rootProject.targetSdk
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
        consumerProguardFiles "consumer-rules.pro"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }

    compileOptions {
        targetCompatibility JavaVersion.VERSION_17
        sourceCompatibility JavaVersion.VERSION_17
    }

    buildFeatures {
        dataBinding true
        viewBinding true
        compose true
    }

    composeOptions {
        kotlinCompilerExtensionVersion = "1.4.6"
    }

    namespace 'com.example.screen_feed'
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    /** hilt */
    implementation "com.google.dagger:hilt-android:$hiltVersion"
    kapt "com.google.dagger:hilt-compiler:$hiltVersion"

    /** compose */
    def composeBom = platform('androidx.compose:compose-bom:2023.05.01')
    implementation composeBom
    androidTestImplementation composeBom
    //없으면 @Composable import 안됨
    implementation 'androidx.compose.ui:ui'
    //없으면 Text("Hello") 안됨
    implementation 'androidx.compose.material:material'
    // Android Studio Preview support
    implementation 'androidx.compose.ui:ui-tooling-preview'
    debugImplementation 'androidx.compose.ui:ui-tooling'
    //JetNews Main 따라하기
    implementation 'androidx.compose.material3:material3'
    implementation "androidx.compose.material3:material3-window-size-class"
    // collectAsState
    implementation "androidx.lifecycle:lifecycle-runtime-compose:2.6.1"
    implementation "androidx.lifecycle:lifecycle-viewmodel-compose:2.6.1"

    /** local */
    implementation "com.github.sarang628:Theme:$themeVersion"
}
```

애플리케이션
```
plugins {
    id 'com.android.application'
    id 'org.jetbrains.kotlin.android'
    id 'com.google.dagger.hilt.android'
    id 'kotlin-kapt'
    id 'dagger.hilt.android.plugin'
}

android {
    compileSdk rootProject.compileSdk

    defaultConfig {
        applicationId "com.sryang.feedscreentestapp"
        minSdk rootProject.minSdk
        targetSdk rootProject.targetSdk
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
    buildFeatures {
        compose true
    }

    composeOptions {
        kotlinCompilerExtensionVersion = "1.4.6"
    }
    compileOptions {
        targetCompatibility JavaVersion.VERSION_17
        sourceCompatibility JavaVersion.VERSION_17
    }
    namespace 'com.posco.feedscreentestapp'
}

```