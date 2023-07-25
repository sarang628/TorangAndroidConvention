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
    namespace 'com.sryang.feedscreentestapp'
}

dependencies {
    /** hilt */
    implementation "com.google.dagger:hilt-android:$hiltVersion"
    kapt "com.google.dagger:hilt-android-compiler:$hiltVersion"

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
    implementation 'androidx.compose.material3:material3'
    implementation "androidx.compose.material3:material3-window-size-class"
    // collectAsState
    implementation "androidx.lifecycle:lifecycle-runtime-compose:2.6.1"
    // Optional - Integration with activities
    implementation 'androidx.activity:activity-compose:1.7.1'

    /** Retrofit */
    implementation 'com.squareup.retrofit2:retrofit:2.9.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
    implementation 'com.squareup.okhttp3:logging-interceptor:4.10.0'

    /** Room */
    def room_version = "2.5.1"
    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version"
    // To use Kotlin annotation processing tool (kapt)
    kapt "androidx.room:room-compiler:$room_version"
    // optional - RxJava2 support for Room
    implementation "androidx.room:room-rxjava2:$room_version"
    // optional - RxJava3 support for Room
    implementation "androidx.room:room-rxjava3:$room_version"
    // optional - Guava support for Room, including Optional and ListenableFuture
    implementation "androidx.room:room-guava:$room_version"
    // optional - Test helpers
    testImplementation "androidx.room:room-testing:$room_version"
    // optional - Paging 3 Integration
    implementation "androidx.room:room-paging:$room_version"
    implementation "androidx.room:room-ktx:$room_version"

    implementation project(path: ':library')
    implementation "com.github.sarang628:Theme:$themeVersion"
}


```

```
// Top-level build file where you can add configuration options common to all sub-projects/modules.
plugins {
    id 'com.android.application' version '8.0.1' apply false
    id 'com.android.library' version '8.0.1' apply false
    id 'org.jetbrains.kotlin.android' version '1.8.20' apply false
    id 'com.google.dagger.hilt.android' version '2.44' apply false
}

ext {
    // Sdk and tools
    compileSdk = 33
    minSdk = 24
    targetSdk = 30
    buildToolsVersion = '30.0.3'

    //hilt
    hiltVersion = '2.44'

    //navigation
    navigationVersion = '2.4.0-alpha06'

    torangImageLoaderVersion = 'f4a2359698'
    themeVersion = '7c191eb4e6'
    navigationModuleVersion = 'd98f57435d'
    repositoryVersion = '8d4bef8640'
    baseFeedVersion = 'aa5b46f3e0'
}
```