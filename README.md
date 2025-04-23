This repo is used to solve the ios pod install error when using ffmpegkit with https-lts.

Create on `ios/ffmpeg-kit-ios-https.podspec`
With content:
```
Pod::Spec.new do |s|
    s.name             = 'ffmpeg-kit-ios-https'
    s.version          = '6.0.LTS'
    s.summary          = 'Custom https FFmpegKit iOS frameworks from angelos3lex.'
    s.homepage         = 'https://github.com/angelos3lex/ffmpeg-kit-ios-https'
    s.license          = { :type => 'LGPL' }
    s.author           = { 'angelos3lex' => 'https://github.com/angelos3lex' }
    s.platform         = :ios, '12.1'
    s.static_framework = true
  
    # Use the HTTP source to fetch the zipped package directly.
    s.source           = { :http => 'https://github.com/angelos3lex/ffmpeg-kit-ios-https/archive/refs/tags/latest.zip' }
  
    # Because the frameworks are inside the extracted archive under:
    # ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/
    # we list each of the needed frameworks with the full relative path.
    s.vendored_frameworks = [
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libswscale.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libswresample.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libavutil.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libavformat.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libavfilter.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libavdevice.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/libavcodec.framework',
      'ffmpeg-kit-ios-https-latest/ffmpeg-kit-ios-https/6.0.LTS-7a080/ffmpegkit.framework'
    ]
  end
```

In your `Podfile`:
```
  pod 'ffmpeg-kit-ios-https', :podspec => './ffmpeg-kit-ios-https.podspec'
  pod 'ffmpeg-kit-react-native', :subspecs => ['https-lts'], :podspec => '../../../node_modules/ffmpeg-kit-react-native/ffmpeg-kit-react-native.podspec'
```

This is exactly the same logic as used in https://medium.com/@nooruddinlakhani/resolved-ffmpegkit-retirement-issue-in-react-native-a-complete-guide-0f54b113b390 article, but for http-lts instead of full-gpl used there.
