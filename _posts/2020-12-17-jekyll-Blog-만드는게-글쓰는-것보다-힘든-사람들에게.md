---
title: jekyll Blog 만드는게 글쓰는 것보다 힘든 사람들에게
date: 2020-12-17 12:32:09
permalink: /:short_year-:month-:day/:title
categories:
- jekyll

tags:
- jekyll
- jekyll theme
- ruby
- rails
- blog
- mac
- 지킬 테마
---

# [mac] Jekyll Blog 지킬 블로그 NeXT theme 따라하기

## 1. 준비사항

1. github pages 호스팅을 기본으로 합니다.

   `username.github.io`라는 이름의 repository를 github에 만들어 줍니다.
   
2. `mac OS`에서 `ruby on rails`를 활용합니다. (windows는 좀 더 복잡한 것 같습니다... 추후 windows에서도 해보고 2탄을 올릴까 생각중입니다)
   

ruby 를 설치하지 않고 jekyll 을 활용하고 싶으시다면  [쉽고 빠르게 수준 급의 GitHub 블로그 만들기 - jekyll remote theme으로](https://dreamgonfly.github.io/blog/jekyll-remote-theme/) 포스팅을 참고하세요. 
   저의 포스팅에서는 좀 더 custom이 가능한 `ruby on rails`를 활용하는 방법을 설명드리겠습니다.

3. 마음에 드는 jekyll theme를 선택합니다. 아래 사이트 들을 돌아다니며 자신이 원하는 theme를 찾아보세요

   - http://jekyllthemes.org/
   - https://jekyllthemes.io/free
   - http://themes.jekyllrc.org/
   - https://github.com/topics/jekyll-theme

   제 블로그에는 다음의 것들이 꼭 필요하다고 생각했습니다.

   - 마크다운으로 글 작성

   - 카테고리
- tag기능 
   - 검색기능
- 포스트 댓글 기능 등
  

위의 요소들을 포함하는 테마 중에서 깔끔하다고 생각한[ `Next theme`](https://github.com/Simpleyyt/jekyll-theme-next)를 선택했습니다.

개인적으로 깔끔한 테마를 추천하자면 [Tale](https://github.com/chesterhow/tale)테마도 추천합니다. `Next theme`과 Tale 사이에서 많이 고민했었습니다.



선택한 theme의 github repository를 로컬 환경에 다운받습니다. 이후 username.github.io 에 git remote 를 연결해줍니다.

```bash
   $ git remote add origin https://github.com/username/username.github.io
```

3. .gitignore 를 추가해줍니다.
   

[jekyll gitignore](https://gist.github.com/bradonomics/cf5984b6799da7fdfafd) 페이지를 활용하시면 됩니다.

5. Jekyll은 기본적으로 `ruby on rails` 의 정적 페이지 프로젝트입니다. 따라서 ruby 언어 설치가 필요합니다.
   만약 mac OS를 쓰고 계시면 ruby가 기본적으로 설치되어 있을 수도 있습니다. 
   (아니면 homebrew를 통해 간단히 설치도 가능합니다.)
   (만약 windows OS를 쓰고 계시다면[ `rubyinstaller`](https://rubyinstaller.org/)를 활용해 설치하시면 됩니다. )
   저희는 이번에는 rvm 을 사용해서 ruby를 설치해보겠습니다.
   ruby는 2.1.x 이상 버전으로 설치해주세요.

6. 루비를 설치하기 전에 rvm을 설치하고 이후 ruby의 버전을 맞추어 설치해줍니다.

   ```bash
   $ \curl -L https://get.rvm.io | bash -s stable
   ```

   rvm 설치 후  체크

   ```bash
   $ rvm list known
   ```

   ```bash
   $ rvm install [ruby-version]
   예: rvm install ruby-2.7.0
   ```

   ruby version확인

   ```bash
   $ ruby -v 
   또는
   $ ruby --version
   ```

   

## 2. Gem

***만약 해당 과정 중  오류가 발생한다면  포스팅아래 3. errors & actions를 확인해주세요.***



### 2-1. Gemfile 설치하기

```ruby
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
#gem 'jekyll-admin', group: :jekyll_plugins
gem 'bigdecimal', '1.3.5'
```

`Gemfile`을 아래와 같이 작성해주세요.

- github-pages gem을 추가해주고, jekyll-admin 부분은 주석처리 합니다.
- bigdecimal의 경우 mac OS 사용 시 `gem` 버전이 맞지 않아 버전까지 추가로 설정해주었습니다.

### 2-2. rails, bundler 설치하기

1. ruby의 프레임워크인 rails를 설치해줍니다.

```bash
$ gem install rails
```

2. 다음으로 라이브러리 관리를 도와주는 bundler를 설치해줍니다.

```bash
$ gem install bundler
```

3. 그리고 update를 실행해줍니다.

(왜 처음 설치할 때부터 최신버전이 아닌지에 대해서는 정확히 모르겠지만, 아마 bundler뿐만 아니라 관련 gem 라이브러리들이 bundler 버전에 맞춰 업데이트 해줘야 하는 것 같습니다..;;)

```bash
$ bundle update --bundler
```

```bash
$ bundle install
```

### 2-3. 로컬에서 제대로 돌아가는지 확인하기

```bash
$ bundle exec jekyll server
```

이 명령어를 입력하면 `http://127.0.0.1:4000` 에서 서버가 구동되는 것을 확인할 수 있습니다.

일단 여기까지만 제대로 되면 아주 Nice한 상황입니다만...

실제로 저는 이 화면을 띄우는데 꼬박 하루 걸렸던 것 같습니다.

다음은 jekyll을 설치하고 실행시키면서 마주쳤던 오류 메시지들과 그에 대한 해결책들을 보여드리겠습니다.



---

## 3. errors & actions

크게 4가지의 error들이 괴롭혔었는데요 하나씩 소개해드리겠습니다.

### 3-1. [oh-my-zsh] permission error

저는 terminal을 `oh-my-zsh`를 사용하고 있습니다. 여기서 계속 이런 오류가 발생합니다.

![oh-my-zsh-permission](https://blog.kakaocdn.net/dn/bxXXV2/btqF00zWrWO/kZ0TIFBgWggC57LXO8MJBK/img.png)

이 문제는 해당 directory의 ower가 현재 user와 다른 경우에 발생한다고 합니다.

예를 들어, 맥에 2개의 계정이 있는데 서로 다른 계정을 사용하면서 생긴 문제라고 합니다. (하지만 저는 그렇지 않았던 것 같은데 계속 이 메시지가 떴습니다...;;)

### 3-1. [oh-my-zsh] permission error actions 대응 방법

해결 방법은 이미지의 마지막에서도 볼 수 있듯이 `ZSH_DISABLE_COMPFIX`를 true로 설정해주는 것입니다.

```bash
$ vi ~/.zshrc
```

명령어를 입력하여 vi editor 모드로 변경합니다.

```bash
...
ZSH_DISABLE_COMPFIX="true"

source $ZSH/oh-my-zsh.sh
...
```

**!주의!**

여기서 가장 중요한 것은 위치입니다. 반드시 `source $ZSH/oh-my-zsh.sh`보다 위쪽에 `ZSH_DISABLE_COMPFIX="true"`를 입력해주세요

`source $ZSH/oh-my-zsh.sh` 는 위의 scripts 들을 적용하는 명령어인데 이것보다 뒤에 있으면 적용되지 않는다고 이해하시면 됩니다.

`:wq`로 저장 후 vi editor를 빠져나옵니다.

이 에러는 이렇게 해결할 수 있었습니다.



### 3-2. undefined method `new' for BigDecimal:Class, Ruby 2.7

```bash
bundler: failed to load command: fastlane (/Users/REDACTED/.gem/ruby/2.7.0/bin/fastlane)
NoMethodError: [!] undefined method `new' for BigDecimal:Class
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext/object/duplicable.rb:111:in `<class:BigDecimal>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext/object/duplicable.rb:106:in `<top (required)>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext/object.rb:3:in `require'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext/object.rb:3:in `<top (required)>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext.rb:2:in `require'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext.rb:2:in `block in <top (required)>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext.rb:1:in `each'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/activesupport-4.2.11.1/lib/active_support/core_ext.rb:1:in `<top (required)>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/slack-ruby-client-0.14.4/lib/slack-ruby-client.rb:39:in `require'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/slack-ruby-client-0.14.4/lib/slack-ruby-client.rb:39:in `<top (required)>'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/fastlane-2.146.1/fastlane/lib/fastlane/fastlane_require.rb:10:in `require'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/fastlane-2.146.1/fastlane/lib/fastlane/fastlane_require.rb:10:in `install_gem_if_needed'
  /Users/REDACTED/.gem/ruby/2.7.0/gems/fastlane-2.146.1/fastlane/lib/fastlane/fast_file.rb:232:in `fastlane_require'
  Fastfile:55:in `block in parsing_binding'
```

이 에러는 ruby 버전과 `BigDecimal` 이라는 gem의 버전 차이 문제로 발생한 것 같습니다.

Gemfile 내에 `gem 'bigdecimal', '1.3.5'` 로 버전까지 명확히 추가한 후 `bundle install` 하니 해결되었습니다.



### 3-3. bundle / bundle install 이 안되는 에러

이 에러도 꽤나 고생했던 에러였습니다.

저는 `homebrew`를 사용하여 ruby 등 다양한 것들을 설치하고 했었는데 이게 mac OS 최신 버전인 Catalina와의 충돌 문제인건지, 아니면 rbenv와의 충돌인건지는 잘 모르겠습니다. 

### Actions 해결법 

저는 아래와 같은 두 줄의 코드를 `vi ~/.zshrc`에 추가하여 해결했습니다.

위와 같이 `source $ZSH/oh-my-zsh.sh` 보다 위쪽에 입력하고 저장하면 됩니다.

```bash
...
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"

source $ZSH/oh-my-zsh.sh
...
```



한 이틀 정도 지나고나서 작성하다보니 그새 에러와 대응법을 많이 잊었습니다.

포스팅의 방법이 완벽하지 않을 수 있으니 사용에 주의해주시고, 혹시 잘못된 부분을 발견하신 분은 아래 댓글로 남겨주시면 정말 감사하겠습니다.

이 외에도 여러가지 에러가 더 생각나거나 제보받으면 추가해보겠습니다.

Windows 컴퓨터에서도 한 번 해보고 올려보도록 하겠습니다.



감사합니다!

---

Copyright: likelionSungGuk 조성국



