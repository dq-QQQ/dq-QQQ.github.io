---
title: jekyll Next 테마 자세히 알아보기
date: 2020-12-17 18:32:09
permalink: /:short_year-:month-:day/:title
categories:
- jekyll

tags: [blog, jekyll, blog, jekyll theme, NexT theme, 지킬 테마, GitHub Pages]
---

## _config.yml

대부분의 Jekyll의 환경설정은 `_config.yml`에서 합니다.

이번 포스팅에서는 `_config.yml`을 자세히 알아봅시다.



## Site

> Site 기본 설정입니다. 아래 이미지를 통해 어떤 내용이 어디에 뜨는지 확인해보세요.

```yaml
title: Blog 대문
subtitle: 개발자 조성국의 블로그입니다.
description: Python, django, algorithm, Computer science, IT 트렌드
author: likelionSungGuk 조성국
Support language: en, ko
language: en
date_format: '%Y-%m-%d'
```

![화면](/assets/img/IMG_0284.jpg)



## URl

```yaml
url: "https://likelionSungGuk.github.io"
baseurl: ""
permalink: pretty
```



## Pagination

> pagination은 게시글이 N개 이상일 경우 N+1개부터는 다음 페이지에서 보여주도록 하는 내용입니다. 
> paginate 10인 경우 게시물 10개까지는 한 페이지에 나오고 그 다음부터는 "NEXT"버튼 누르면 다시 10개가 노출되는 형식입니다.

```yaml
paginate: 10
paginate_path: "/page:num/"
archive:
  paginate: 10
  paginate_path: "/page:num/"
category:
  paginate: 10
  paginate_path: "/page:num/"
tag:
  paginate: 10
  paginate_path: "/page:num/"
```



## favicon

> favicon은 chrom 탭의 맨 앞에 나오는 조그마한 icon입니다.
> assets 폴더에 favicon을 넣으시면 해당 icon으로 favicon을 설정 가능합니다.

```yaml
# Put your favicon.ico into `assets/` directory.
favicon: /assets/favicon_terminal.ico
```



## index_with_subtitle

> Home 화면에서 subtitle까지 보여주는 지 여부에 대한 내용입니다.
> true로 설정하면 subtitle까지 나옵니다.

```yaml
# If true, will add site-subtitle to index page, added in jekyll config.
# subtitle: Subtitle
index_with_subtitle: true
```



## menu

>어떤 메뉴들을 활용하지 선택합니다.
>Home, Category, About, Archive, Tags 들을 활성화시켰으며 sitemap, commonweal의 경우 비활성화 하였습니다.

```yaml
# When running the site in a subdirectory (e.g. domain.tld/blog), remove the leading slash (/archives -> archives)
menu:
  home: /
  categories: /categories/
  about: about/
  archives: /archives/
  tags: /tags/
  #sitemap: /sitemap.xml
  #commonweal: /404.html
```



## menu icons

>  menu를 표현하는 icon들입니다.
> fontawesome 의  아이콘 이름들을 적어주면 해당 icon들로 변경됩니다.

```yaml
menu_icons:
  enable: auto
  # KeyMapsToMenuItemKey: NameOfTheIconFromFontAwesome
  home: home
  about: user
  categories: th
  schedule: calendar
  tags: tags
  archives: archive
  sitemap: sitemap
  commonweal: heartbeat
```

```html
<i class="fas fa-home"></i>
```

[fontawesome](https://fontawesome.com/icons/)사이트에서 위와 같이 `fa-`뒤에 나오는 이름들을 `_config.yml`에 넣어주면 됩니다.



## scheme settings

> Next theme중에서도 크게 3가지 디자인 형식이 있습니다.

```yaml
# Schemes
scheme: Muse
#scheme: Mist
#scheme: Pisces
```

Mist, Pisces 형식의 블로그를 보고 싶으시다면 [Mist 예시](https://blog.zzbd.org/) / [Pisces 예시](https://dandyxu.me/)를 통해 Demo를 확인해주세요.

([Muse 형식의 ㅎㄷㄷ한 Custom CSS 적용 사례](https://acris.me/))



## fonts

>각 영역별로 font를 내가 원하는 것으로 변경할 수 있습니다.

```yaml
# ---------------------------------------------------------------
# Font Settings
# - Find fonts on Google Fonts (https://www.google.com/fonts)
# - All fonts set here will have the following styles:
#     light, light italic, normal, normal italic, bold, bold italic
# - Be aware that setting too much fonts will cause site running slowly
# - Introduce in 5.0.1
# ---------------------------------------------------------------
font:
  enable: true

  # Uri of fonts host. E.g. //fonts.googleapis.com (Default)
  host: {웹 폰트 주소 넣는 곳: 예) fonts.googleapis.com} 

  # Global font settings used on <body> element.
  # Blog 전체의 글꼴 지정 (현 Lato)
  global:
    # external: true will load this font family from host.
    external: true
    family: Lato

  # Font settings for Headlines (h1, h2, h3, h4, h5, h6)
  # Fallback to `global` font settings.
  # h1, h2, h3, h4, h5, h6태그만 font바꾸고 싶다면 설정
  headings:
    external: true
    family:

  # Font settings for posts
  # Fallback to `global` font settings.
  # posting 파트 font설정
  posts:
    external: true
    family:

  # Font settings for Logo
  # Fallback to `global` font settings.
  # The `size` option use `px` as unit
  logo:
    external: true
    family:
    size:

  # Font settings for <code> and code blocks.
  codes:
    external: true
    family:
    size:
```



## search

> 검색기능을 원하시는 경우 enable: true로 설정해주세요
> trigger: manual의 경우 사용자가 search 아이콘을 클릭했을 때에만 나타나는 설정입니다.

```yaml
# Local search
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: manual
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```



이 외에 더 다양한 설정들이 있지만 대부분 중국 관련 Social 링크들이거나 불필요하다고 생각하여 스킵하였습니다.

추가로 궁금한 점이 있으시면 댓글 남겨주세요.

---

Copyright: likelionSungGuk 조성국