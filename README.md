# jrgraph617
Ga repository on GitHub

H:\Users\Ruizing\AndroidStudioProjects\Chapter_4_To-do_List_Part_21\app\build.gradle

apply plugin: 'com.android.application'

def releaseTime() {
    return new Date().format("yyyy-MM-dd", TimeZone.getTimeZone("UTC"))
}

android {
    compileSdkVersion 17
    buildToolsVersion "21.1.2"

    defaultConfig {
        applicationId "com.paad.todolist"
        minSdkVersion 14
        targetSdkVersion 21
        versionCode 1
        versionName "1.0"

        // dex突破65535的限制
        multiDexEnabled true
        // 默认是umeng的渠道
        manifestPlaceholders = [UMENG_CHANNEL_VALUE: "wandoujia"]
    }

//    signingConfigs {
//        debug {
//            // No debug config
//        }
//
//        release {
//            storeFile file("../yourapp.keystore")
//            storePassword "your password"
//            keyAlias "your alias"
//            keyPassword "your password"
//        }
//    }

    buildTypes {
//        debug {
//            // 显示Log
//            buildConfigField "boolean", "LOG_DEBUG", "true"
//
//            versionNameSuffix "-debug"
//            minifyEnabled false
//            zipAlignEnabled false
//            shrinkResources false
////            signingConfig signingConfigs.debug
//        }

        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.txt'
//            signingConfig signingConfigs.release

            applicationVariants.all { variant ->
                variant.outputs.each { output ->
                    def outputFile = output.outputFile
                    if (outputFile != null && outputFile.name.endsWith('.apk')) {
                        // 输出apk名称为 jrgraph_v1.0_2015-06-15_wandoujia.apk
                        def fileName = "jrgraph_v${defaultConfig.versionName}_${releaseTime()}_${variant.productFlavors[0].name}.apk"
                        output.outputFile = new File(outputFile.parent, fileName)
                    }
                }
            }
        }
    }

    productFlavors {
        xiaomi {}
        _360 {}
        baidu {}
        wandoujia {}
        tencent {}
        taobao {}
    }

    productFlavors.all {
        flavor -> flavor.manifestPlaceholders = [UMENG_CHANNEL_VALUE: name]
    }

//    dependencies {
//        compile fileTree(dir: 'libs', include: ['*.jar'])
//        compile 'com.android.support:support-v4:21.0.3'
//        compile 'com.jakewharton:butterknife:6.0.0'
////        ...
//    }

}
