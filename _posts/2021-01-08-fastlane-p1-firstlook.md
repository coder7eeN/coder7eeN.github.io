---
layout: post
title: "Fastlane and beyond (Phần 1: First look)"
description: Fastlane là gì?
summary: Fastlane là gì?
tags: fastlane, cd
---

Bạn là dev à nhầm là phận code nô, công việc của bạn là code, push code lên Github, build file apk đẩy lên Firebase App Distribution cho tester soi bug, lâu lâu lại phải share file apk kia lên Slack cho một mục đích nào đó mà PM hoặc đồng nghiệp nhờ bạn làm :) Lúc đầu bạn thấy công việc thật thú vị nhưng làm đến lần thứ n thì bạn đã lãng phí quá nhiều thời gian để ngồi làm tay chừng đó việc. 

Vậy giải pháp là gì, đó chính là CD **(Continuous Delivery)**. Hiểu đơn giản, CD là cách giúp triển khai tất cả thay đổi về code (apk đã được build và test) đến các môi trường debug, staging hoặc tự động hóa hoàn toàn quy trình release phần mềm. Để giúp bạn tiếp cận CD đơn giản hơn, mình xin được giới thiệu Fastlane - tool giúp bạn tiết kiệm khối thời gian lãng phí kia để làm được nhiều việc hơn.

## 1. Fastlane là gì?

<p align="center" >
  <img src="/images/blog_illustration/fastlane_usage.png" width="70%" />
</p>

Chả có hình nào minh họa cho Android nên mình đành lấy bên iOS vậy. Như bạn thấy, Fastlane là tool giúp làm những công việc như chụp ảnh màn hình, thông báo lên Slack, đẩy bản build đến cho tester hoặc release phần mềm lên store một cách tự động. Ngoài những việc như vậy, Fastlane còn làm được nhiều thứ hơn nữa, tham khảo tại [link](https://docs.fastlane.tools/#why-fastlane) này để biết thêm nè. 

## 2. Cài đặt Fastlane

Yêu cầu phải có Ruby version từ **2.5.1** trở lên. Nếu chưa có hoặc version nhỏ hơn thì bạn có thể sử dụng **rbenv**, **rvm** hoặc **npm** để cài đặt hoặc nâng cấp (mình khuyến khích mọi người nên xài **rbenv** vì tham khảo ý kiến mấy thằng team Ruby tụi nó bảo tool này quản lí version ngon lắm).

Sau khi đã nâng cấp Ruby thành công thì bạn hãy nhập dòng lệnh này vào terminal để cài đặt Fastlane

```bash
sudo gem install fastlane -NV
```

Để kiểm tra đã cài thành công Fastlane chưa thì sử dụng câu lệnh này

```bash
fastlane -v
```

Và ta sẽ có được kết quả như sau

```bash
fastlane installation at path:
/Users/huypham/.rbenv/versions/2.5.8/lib/ruby/gems/2.5.0/gems/fastlane-2.171.0/bin/fastlane
-----------------------------
[✔] 🚀 
fastlane 2.171.0
```

Giờ thì chúng ta có thể thêm Fastlane vào project rồi.

#### 2.1 Khởi tạo Fastlane 

Đầu tiên, bạn hãy tạo một project Android mới, tham khảo view tại [project](https://github.com/coder7eeN/fastlane_and_beyond/tree/main/app/src/main) mẫu này. 

Tiếp theo, tạo file **Gemfile**, thêm những dòng này vào file **Gemfile** vừa mới tạo

```
"https://rubygems.org"

gem "fastlane"
```

Chạy lệnh khởi tạo Fastlane (nếu yêu cầu permission hãy thêm `sudo` vào trước là xong)

```bash
fastlane init
```

Sẽ có vài lần dừng tiến trình để ta có thể config cho Fastlane phù hợp với project của mình. Lần đầu tiên, ta sẽ phải config package name, để lấy được package name ta mở file **AndroidManifest** copy tên trong param **package**. Ví dụ ở đây project của mình tên package: `com.huypham.fastlaneandbeyond`

```bash
Package Name (com.krausefx.app): com.huypham.fastlaneandbeyond
```

Lần dừng thứ 2, tiến trình nhắc ta config path cho file Json phục vụ việc upload bản build và metadata lên GooglePlay, ở bước này chỉ cần `enter` để skip. Lần dừng thứ 3, tiến trình hỏi **Download existing metadata and setup metadata management? (y/n)** chỉ cần `n` để skip. Những việc này ta đều có thể config sau, nó không ảnh hưởng đến việc khởi tạo. Sau khi đã khởi tạo xong Fastlane vào project, chạy lệnh sau để kiểm tra

```bash
bundle exec fastlane test
```

Nếu thấy được thông báo `fastlane.tools finished successfully 🎉` thì chúc mừng bạn, cuộc vui đã bắt đầu.

#### 2.2 Fastfile

Bạn sẽ thấy folder fastlane có 2 files là Appfile và Fastfile.

- **Appfile**: nơi bạn có thể chứa key của app, token của Firebase, những thứ sẽ liên quan đến việc build app. Nhưng vẫn có 1 nơi khác để lưu trữ token và key ngon, xịn, mịn hơn, mình sẽ đề cập ở đoạn sau.
- **Fastfile**: nơi để viết những đoạn script cấu hình. Sử dụng ngôn ngữ Ruby để viết nhưng bạn không cần phải quá lo, chỉ cẩn nắm những cú pháp cơ bản là có thể cấu hình được lane, ghé qua [Fastlane Document](https://docs.fastlane.tools/) để hiểu rõ hơn.

```ruby
default_platform(:android)

platform :android do
  desc "Runs all the tests"
  lane :test do
    gradle(task: "test")
  end

  desc "Submit a new Beta Build to Crashlytics Beta"
  lane :beta do
    gradle(task: "clean assembleRelease")
    crashlytics
  
    # sh "your_script.sh"
    # You can also use other beta testing services here
  end

  desc "Deploy a new version to the Google Play"
  lane :deploy do
    gradle(task: "clean assembleRelease")
    upload_to_play_store
  end
end
```

Có 2 khái niệm bàn cần nắm để có thể viết những đoạn script trong Fastfile đó là **lanes** và **actions**. Hiểu đơn giản, 1 file Fastfile là 1 con đường cao tốc, lanes là những làn đường nơi chứa những actions là những phương tiện giao thông, mỗi phương tiện lại có 1 công dụng khác nhau.

Cùng phân tích và đế ý chút về cú pháp ở file Fastfile

- **decs** + **mô tả** đây là phương thức dùng để làm những việc như: mô tả lane phía dưới để làm gì; khi chạy Fastlane nó sẽ báo đang chạy đến đoạn nào; ghi lại log trong file README sau khi chạy Fastlane.
- **do**, **end** tương đương với **{}**.
- **lane** bắt đầu bằng keyword `lane` tiếp theo là tên mà bạn muốn đặt cho lane đó, ví dụ `:test`.
- **default_platform(:android)** đây là 1 action giúp khai báo platform mặc định bạn sử dụng.
- **platform :android** xác định platform để chạy là Android chứ không phải là iOS.

Vậy còn **gradle(task: "test")** là gì, đó chính là hành động (action) mà lane đó sẽ làm. Điển hình ở lane test, hành động của lane này là chạy test trên tất cả variants thông qua [Gradle](https://docs.fastlane.tools/actions/gradle/) action. 

Còn rất nhiều actions phục vụ cho nhiều mục đích khác nhau, bạn có thể tham khảo [actions](https://docs.fastlane.tools/actions/) để khám phá thêm. Lanes cũng vậy, ghé qua [lanes](https://docs.fastlane.tools/advanced/lanes/) để tìm thêm được nhiều cú pháp giúp "custom" lane theo cách bạn muốn.

## 3. Thực hành

Sau khi đã ngâm cứu về cú pháp, chúng ta cùng bắt tay vào viết thử 1 lane và chạy nó để xem thử có nên ngô nên khoai gì không nào. Lane của chúng ta sẽ thực hiện 2 hành động, clean toàn bộ folder build và build file apk cho debug.

```ruby
desc "Clean build and build apk debug"
lane :clean_and_build_apk do
  gradle(task: "clean")
  gradle(task: "assembleDebug")
end
```

Chạy lane này trên terminal

```bash
bundle exec fastlane clean_and_build_apk
```

Kết quả

```bash
+------+------------------+-------------+
|           fastlane summary            |
+------+------------------+-------------+
| Step | Action           | Time (in s) |
+------+------------------+-------------+
| 1    | default_platform | 0           |
| 2    | clean            | 5           |
| 3    | assembleDebug    | 35          |
+------+------------------+-------------+

fastlane.tools finished successfully 🎉
```

Oh yeahhh!! vậy là chúng ta đã tạo được lane chạy đúng với mục đích như đã đề ra.

## 4. Save the best for last

Ở phía trên mình có nói về một nơi chứa token và key ngon, xịn, mịn hơn Appfile - đó chính là file `.evn`. Nếu ai chịu khó lặn trên document của Fastlane thì bạn sẽ thấy được phần **Environment Variables** nằm ở [Other](https://docs.fastlane.tools/advanced/other/). Vậy nó ngon ở chỗ nào? Xem ví dụ dưới đây nào (ở bài sau mình sẽ giải thích rõ hơn về action Slack này)

```ruby
desc "Show message on Slack"
lane :slack_message do
  f = File.open("../local.properties", "r")
  ENV["SLACK_URL"] = f.each_line.to_a.last.split('=').last
  f.close
  
  gradle(task: "clean assembleDebug")
  slack(message: "Slack Message Delivered Successfully")
end
```

Thông thường bạn sẽ chứa token, key ở Appfile hoặc local.properties, muốn xài được những key hoặc token này thì chỉ có cách viết câu lệnh đọc từ file ra. Ở đây, muốn lấy giá trị cho **ENV["SLACK_URL"]** ta phải đọc dòng cuối cùng trong file local.properties và lấy giá trị sau dấu **=**. Bạn thấy cực không, mình thấy có, giờ hãy nhìn cách `.env` giải quyết vấn đề.

```ruby
desc "Show message on Slack"
lane :slack_message do
  ENV["SLACK_URL"]
  
  gradle(task: "clean assembleDebug")
  slack(message: "Slack Message Delivered Successfully")
end
```

Bạn có thể vứt luôn cả **ENV["SLACK_URL"]** mà lane vẫn chạy phà phà, magic chưa. Config của file `.env` sẽ như vầy

```
SLACK_URL="https://hooks.slack.com/services/xxx"
```

Để đảm bảo tính bảo mật thì háy nhớ thêm file này vào gitignore nữa nhá.

Tới đây chắc bạn cũng đã có chút mường tượng được những thứ mà bạn muốn "tự động hóa" trong project của mình. Bài viêt tiếp theo chúng ta sẽ vọc những actions như Slack hay Screengrab.