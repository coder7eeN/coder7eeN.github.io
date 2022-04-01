---
layout: post
title: "Make PowerShell great again"
description: How to config PowerShell 
summary: How to config PowerShell
tags: powershell
---

<style>

img {
  max-width: 100%;
  height: auto;
  border-radius: 4px;
}

.single-img {
  max-width: 100%;
  height: auto;
  margin-top: 10px;
}

.column {
  float: left;
  width: 50%;
  padding: 4px;
  margin-top: 10px;
}

.single {
  text-align: center;
  width: 100%;
  padding: 4px;
}

.row::after {
  content: "";
  clear: both;
  display: table;
}

</style>

<div class="single">
  <img src="/images/blog_illustration/config_powershell/thumbnail_terminal.png" style="width=100%" class="single-img">
</div>

Chuyện là mình có một con máy tính chạy Windows lâu nay chỉ để lướt web và đánh Dota2. Nhân sự kiện sắp phải chia tay với macOS sau gần 4 năm gắn bó, thì mình quyết định chuyển nó thành máy code chính của mình. Mọi thứ đều hoàn hảo đến khi mình mở Windows PowerShell lên để sử dụng, với mình terminal + oh-my-zhs đã là một thứ gì đó không thể thiếu, thì trải nghiệm lúc đó khá là 3 chấm.

Muốn ăn thì lăn vào bếp, mình phải xắn tay áo lên để "clone" lại những trải nghiệm đã có của mình từ terminal + oh-my-zhs bên macOS qua. Và đây là câu chuyện nâng cấp nhan sắc và điện nước cho PowerShell của mình :)

## 1. Tổ chức thư mục và thư viện

Đầu tiên là cách tổ chức các thư mục để lưu phần cấu hình cho PowerShell và custom theme cho nó.

    └─ $env:USERPROFILE\.config          general folder for library
        └─ powershell                    build powershell
           ├─ user_profile.ps1           config file
           └─ my.omp.json                prompt customizations
        
Tiếp theo là các thư viện mà mình sẽ sử dụng
  - Nerd fonts - fonts và symbols
  - Scoop - a command line installer
  - Oh My Posh - prompt theme engine
  - Terminal Icons - file and folder icons
  - PSReadLine - cmdlets cho phép custom môi trường edit, dùng cho autocompletion
  - z - directory jumper
  - Fzf, PSFzf - fuzzy finder
  - Neovim - vim

## 2. Cài đặt Windows Terminal, PowerShell

Đây là bước quan trọng nhất, mình cần cài Windows Terminal để có thể cấu hình cho PowerShell và chạy đa nhiệm. Hơn nữa Windows Terminal cho phép chúng ta custom giao diện cho terminal. Tiếp theo là cài PowerShell, nó giúp mình có thể cài được rất nhiều thư viện bên thứ 3 cũng như có rất nhiều cải tiến so với Windows PowerShell mặc định trong máy. Cả 2 apps này đều có thể tải trực tiếp ở Windows Store.

<div class="row">
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/windows_terminal.png" style="width=100%">
  </div>
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/powershell.png" style="width=100%">
  </div>
</div>

## 3. Terminal settings

Mình lên [Nerd font github](https://github.com/ryanoasis/nerd-fonts) để tải font đã được custom lại với các symbol đặc biệt. Ví dụ như font Ubuntu Mono mình tải trên trang chủ và tải trên này thì font trên trang chủ mình không thể show được các symbol trong lúc mình custom lại phần giao diện cho terminal cũng như lúc xài các theme có sẵn trên Oh My Posh.

Sau khi đã tải được font đúng với sở thích thì mình mở sẽ bắt đầu custom lại cho Windows Terminal, vào phần settings và chỉnh lại các phần sau:
  - Default profile: **PowerShell**
  - Show acrylic in tab row: **On**
  - Font face: **font bạn mới tải**
  - Acrylic: **On** 
  - Acrylic opacity: **50%**

## 4. Scoop

Để có thể cài đặt các thư viện thông qua command line thì mình sử dụng [Scoop](https://scoop.sh/). Sử dụng lệnh sau để cài đặt Scoop

```bash
iwr -useb get.scoop.sh | iex
```

## 5. Git

Thư viện quan trọng nhất mà code nô nào cũng phải có trong máy. Ở đây cài đặt git thì có 2 cách, tải file cài về rồi chạy hoặc tải bằng command line, tất nhiên mình sẽ chọn cách sau rồi. Câu lệnh để cài đặt git 

```bash
winget install -e --id Git.Git 
```

Trong lúc đợi nó cài đặt thì mình sẽ ghé qua [powershell-git-aliases](https://github.com/gluons/powershell-git-aliases) để xem thử có bản cập nhật mới chưa. Đây là thư viện gì, sao mình lại không nói ở trên. Xin đáp đây là thư viện clone lại toàn bộ Oh My Zhs cheatsheet :) 

Sau 1 thời gian dài code trên macOS thì Oh My Zsh là shell chính của mình. Khi xài git thì mình toàn sử dụng các lệnh gõ tắt, dần nó thành 1 thói quen. Việc viết tắt này giúp cho mình có thể làm việc với git nhanh hơn, ví dụ bạn muốn sử dụng 

```bash
git commit -a -m "your commit"
```
thì chỉ cần gõ 
 
```bash
gcam "your commit"
```

Việc sử dụng thư viện này là tùy theo sở thích của mỗi người nên mình đưa nó vào phần này như một option thêm. Để cài đặt nó thì sử dụng lệnh sau

```bash
// Powershell
Install-Module git-aliases -Scope CurrentUser -AllowClobber

// or from Scoop
scoop bucket add extras
scoop install git-aliases
```

<div class="row">
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/git_demo.png" style="width=100%">
  </div>
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/git_alias.png" style="width=100%">
  </div>
</div>

## 6. NeoVim

PowerShell mặc định không có hỗ trợ vim nhưng mình cần sử dụng vim để có thể viết các file config cho PowerShell và Git. Cài đặt NeoVim bằng câu lệnh sau

```bash
scoop install neovim gcc
```

Kiểm tra việc cài đặt NeoVim đã thành công hay chưa thì mình gõ `nvim` rồi `Enter`. Nếu giao diện sau hiện ra thì bước này đã xong.

<div class="single">
    <img src="/images/blog_illustration/config_powershell/neo_vim.png" style="width=100%" class="single-img">
</div>

Với mình nếu chỉ dừng ở đây thì vẫn chưa vừa ý lắm, mình muốn làm sao vim có thể hiển thị số dòng, tùy chỉnh khi xuống dòng và thêm vài thứ nữa. Để có thể custom vim mình tạo folder `nvim` và file `init.vim` trong folder Local theo cấu trúc sau

    └─ $env:USERPROFILE\AppData          
        └─ Local                    
           └─ nvim          
              └─ init.vim               

Lên trang [linode](https://www.linode.com/docs/guides/introduction-to-vim-customization/) và copy những lệnh để config cho vim. Giờ thì tận hưởng kết quả thôi :)

<div class="single">
    <img src="/images/blog_illustration/config_powershell/vim_custom.png" style="width=100%" class="single-img">
</div>

## 6. Config PowerShell

> - Từ đoạn này mình nghĩ các bạn nên search nhanh cách làm việc với Vim để đọc dễ dàng hơn
> - Restart lại Windowns Terminal sau khi cài thành công NeoVim
> - Mình cũng bắt đầu để cấu trúc thư mục để các bạn có thể biết được những thư viện của mình sử dụng sẽ cài vào đâu
> - Các câu lệnh ở đây chạy tuần tự, xong câu lệnh đầu rồi mới chạy câu lệnh sau

    └─ $env:USERPROFILE\

Bây giờ mình sẽ tạo file `user_profile.ps1` để có thể chứa các config thông dụng hay sử dụng. Sử dụng câu lệnh sau

```bash
nvim .config/powershell/user_profile.ps1
```

Trong file này đầu tiên chúng ta sẽ cấu hình các alias, đây là các cách gọi nhanh khác khi sử dụng thư viện.

```bash
Set-Alias vim nvim                                        // viết tắt nvim thành vim
Set-Alias ll ls                                           // để hiển thị danh mục gõ ll thay vì ls
Set-Alias g git                                           // viết tắt g cho git
Set-Alias tig 'K:\Program Files\Git\usr\bin\tig.exe'      // truy cập nhanh đến tig 
Set-Alias less 'K:\Program Files\Git\usr\bin\less.exe'    // truy cập nhanh đến less 
```

Tiếp theo, mình sẽ thiết lập môi trường chạy cho file cấu hình này. Sử dụng câu lệnh sau

```
nvim $PROFILE.CurrentUserCurrentHost
```

Và cấu hình môi trường bằng câu lệnh

```bash
. $env:USERPROFILE\.config\powershell\user_profile.ps1
```

Khi làm đến bước này mình có 1 issue, đó là không thể tìm thấy folder PowerShell trong Documents. Đồng thời đường dẫn của mình thông qua OneDrive. Vậy đây là cách xử lý cho nó, mình vào trong folder Documents của OneDrive và tạo folder PowerShell, sau đó chạy lại 2 câu lệnh trên. 

    └─ $env:USERPROFILE\OneDrive          
        └─ Documents                 
           └─ PowerShell                         

Gõ `ls`, `g` test thử coi nó hoạt động có đúng như mong đợi không nào.

## 7. Oh My Posh

    └─ $env:USERPROFILE\.config          
        └─ powershell                    

Để cái terminal có thể lòe loẹt hết mức có thể thì mình sử dụng [Oh My Posh](https://ohmyposh.dev/docs/) :) 

Chạy lệnh sau để cài đặt

```bash
Install-Module posh-git -Scope CurrentUser -Force
Install-Module oh-my-posh -Scope CurrentUser -Force
```

Mình sẽ cấu hình nó vào file `user_profile.ps1` để lần sử dụng Windows Terminal tiếp theo nó sẽ tự động được kích hoạt.

```bash
nvim .config/powershell/user_profile.ps1
```

Và thêm vào

```bash
Import-Module posh-git              // chạy posh-git 
Import-Module oh-my-posh            // chạy oh-my-posh
Set-PoshPrompt M365Princess         // sử dụng theme M365Princess
```

Oh My Posh cung cấp rất nhiều theme khác nữa, nếu bạn thích thì có thể lên [themes của Oh My Posh](https://ohmyposh.dev/docs/themes) để ngắm và chọn lựa.

Như mình thích vọc vạch thì mình sẽ tự custom lại theme, để làm việc này thì mình tạo file `coder7een.omp` để custom lại phần json cho theme. Bạn có thể lên github của từng theme, copy lại phần json rồi tùy chỉnh theo ý muốn của bản thân. Sức mạnh của mã nguồn mở giúp những người thích vọc vạch được phát huy tối đa sở thích của mình :)

Sau khi đã tùy chỉnh xong theme đúng với sở thích của mình thì bạn cần cấu hình nó trong `user_profile.ps1`

```bash
function Get-ScriptDirectory { Split-Path $MyInvocation.ScriptName }
$PROMPT_CONFIG = Join-Path (Get-ScriptDirectory) 'coder7een.omp.json'
oh-my-posh --init --shell pwsh --config $PROMPT_CONFIG | Invoke-Expression
```

Và nhớ xóa đi dòng lệnh sau để không còn chạy theme chọn từ Oh My Posh

```bash
Set-PoshPrompt M365Princess
```

## 8. Terminal Icons

    └─ $env:USERPROFILE\.config          
        └─ powershell    

Khi mình xài lệnh `ll` để hiển thị danh mục thì nó hơi trơ trọi, để tăng sức lòe loẹt cho terminal thì mình cài vào thư viện icon. Sử dụng câu lệnh sau

```bash
Install-Module -Name Terminal-Icons -Repository PSGalery -Force
```

Cấu hình nó trong `user_profile.ps1`

```bash
Import-Module -Name Terminal-Icons
```

Kết quả thu được :) Lòe loẹt và rõ ràng hơn cũ nhiều ha.

<div class="single">
    <img src="/images/blog_illustration/config_powershell/terminal_icon.png" style="width=100%" class="single-img">
</div>

## 9. Cài đặt z - directory jumper

    └─ $env:USERPROFILE\.config          
        └─ powershell    

Thư viện z này giúp mình có thể quay lại các folder đã mở lúc trước một cách nhanh chóng mà không cần phải `cd` nữa, chỉ cần `z <tên thư mục>` là nó tự động nhảy đến. Cài đặt thông qua câu lệnh

```bash
Install-Module -Name z -Force
```

## 10. PSReadline

    └─ $env:USERPROFILE\.config          
        └─ powershell    

Khi làm việc với zsh của macOS thì thư viện autocompletion của nó đã giúp mình có thể nhanh chóng sử dụng các câu lệnh cũ đã gõ. Việc nhắc lệnh tự động giúp mình làm việc được thoải mái hơn, nhiều lúc không nhớ lúc trước chỗ đó mình đã viết cái gì thì có thư viện này, mọi thứ đều hiện lên lại.

Cài đặt như sau

```bash
Install-Module -Name PSReadLine -AllowPrerelease -Scope CurrentUser -Force -SkipPublisherCheck
```

Thêm cấu hình trong `user_profile.ps1`

```bash
Set-PSReadLineOption -PredictionSource History        // lấy câu lệnh từ History
```

Bây giờ khi gõ lệnh, mình chỉ cần gõ vài kí tự đầu là nguyên câu lệnh đã được nhắc sẵn rồi, cool :)

## 11. Fuzzy finder

    └─ $env:USERPROFILE\.config           

Phần cuối cùng khi custom lại cái PowerShell chính là tìm kiếm thư mục. Nếu macOS mình chỉ cần tab 2 lần là có thể di chuyển đến thư mục mình cần thì ở đây tab chỉ hiển thị thư mục, khá bất tiện. Fuzzy finder sinh ra để giúp mình làm việc này. Cài đặt như sau

```bash
scoop install fzf
Install-Module -Name PSFzf -Scope CurrentUser -Force
```

Update thêm vào `user_profile.ps1` 

```bash
Import-Module PSFzf
Set-PSFzfOption -PSReadLineChordProvider 'Ctrl+f' -PSReadLineChordReverseHistory 'Ctrl+r'
```

Giờ đây chỉ cần nhấn `ctrl + f` là mình đã có thể tìm kiếm nhanh các thư mục và trở đến thư mục mình cần sử dụng. Tuy thao tác phải tốn thêm 1 bước tổ hợp phím nhưng kết quả thì tương đương.

## 12. Tinh chỉnh thêm cho git-alias 

    └─ $env:USERPROFILE\.config          
            └─ powershell    

Ở trên mình đã cài đặt thư viện `powershell-git-aliases` nhưng để có thể tự động chạy mỗi lần xài git thì mình cần phải cấu hình nó trong `user_profile.ps1`

```bash
Import-Module git-aliases -DisableNameChecking
```

## 13. Kết

Giờ thì chạy lại PowerShell để có thể tận hưởng thành quả của mình thôi.

<div class="row">
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/finish_1.png" style="width=100%">
  </div>
  <div class="column">
    <img src="/images/blog_illustration/config_powershell/finish_2.png" style="width=100%">
  </div>
</div>

Đối với mình, sau khi nâng cấp thành công PowerShell thì cảm hứng làm việc của mình cũng được thêm kha khá. Mình mong bài chia sẻ này có thể giúp các bạn có thể nâng cấp cái terminal đang xài của mình trên Windows lên 1 tầm cao mới, lòe loẹt và tiện dụng hơn :) 

## 14. Tham khảo
Yup, mình không thể nào tự mò hết tất cả thư viện trong này được, nguồn tham khảo của mình ở đây.

[devaslife - How to set up PowerShell prompt with Oh My Posh on Windows 11](https://youtu.be/5-aK2_WwrmM)
