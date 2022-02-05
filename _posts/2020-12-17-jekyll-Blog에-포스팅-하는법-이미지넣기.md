---
title: jekyll Blog에 포스팅 하는법-이미지넣기
date: 2020-12-17 17:32:09
permalink: /:short_year-:month-:day/:title
categories:
- jekyll

tags: [blog, jekyll, blog, jekyll theme, NexT theme, 지킬 테마, 지킬 블로그 포스팅, GitHub Pages]
---

## Jekyll Blog Posting Basic

![image-20201217202444028](/assets/img/image-20201217202444028.png)

blog posting은 `_post` 폴더 안에 `markdown`문서를 작성하면 됩니다.

대신 이 때 지켜야할 형식이 있습니다.

바로 `markdown`문서의 최상단에 아래와 같은 `Yaml` 방식의 코드를 삽입해주는 것입니다.

아래는 이번 포스팅의 예시를 그대로 사용하였습니다.

```yaml
---
layout: post
title: jekyll Blog에 포스팅 하는법-이미지넣기
date: 2020-12-17 17:32:09
categories: 
- jekyll
- blog
tags: [blog, jekyll, blog, jekyll theme, NexT theme, 지킬 테마, 지킬 블로그 포스팅, GitHub Pages]
---- 
```

하나 하나 살펴보면

1. 위 아래를 세 개의 대시(-)로 막고 그 안에 내용을 작성합니다.
2. `layout`: 레이아웃은 이 글이 어떤 형식인지를 명시합니다. Next theme에서는 archive, post, page, category, tag,  등의 레이아웃이 있습니다. 
   이 중에서 포스팅은 `post`를 사용합니다.
3. `title`은 이 포스팅의 제목을 나타냅니다. (추후 자동적으로 해당 markdown 파일 자체의 이름이 됩니다.)
4. `categories`는 이 글의 카테고리를 나타내는 것으로 이 글이 어떻게 분류 되었으면 하는지 희망하는 대로 작성하면 됩니다. 예시의 모습처럼 대시(-) 이후 한 칸 띄고 엔터치는 방식으로도 작성이 가능하고 아래 tags와 같이 배열 형태로 두 가지 형식 모두 작성 가능합니다.
5. `tags`는 이 글에 여러개의 tag를 달아 추후 tag별 구분이 가능하도록 하고 검색엔진에 잘 잡히도록 `SEO`를 도와주기도 합니다. 



이 외에도 permalink, date 형식 변경 등 다양한 내용이 있습니다.

더 자세한 내용은 [**jekyll 공식 사이트**](https://jekyllrb.com/docs/front-matter/)에서 확인하시고 하나씩 테스트해보시면 됩니다.



이후 아래 부분에 평범한 markdown 형식으로 글을 작성하면 됩니다. 이후 Git Push 해주시면 몇 분 후 글이 포스팅 됩니다.

**만약 온라인에 어떻게 포스팅 될 지 미리 확인해 보고 싶으시다면,**

1. ``_draft` 폴더를 따로 만들어 온라인 상에서 확인하는 방법
2. `Atom` 에디터를 활용하여 markdown 작성과 동시에 Web에서 보여지는 화면을 보면서 작성
3. `bundle exec jekyll serve`로 로컬 서버로 먼저 돌려서 확인하는 방법

등 이 있습니다.



## 생각보다 난관인 이미지 넣기

### 문제상황

하지만 예전과 같이 `markdown`을 작성하시면서 글 중간 중간 이미지를 업로드 하실 경우, 웹상에서는 이미지가 제대로 뜨지 않는 오류가 심심찮게 발생합니다.

저의 경우 `Markdown`파일을 `Typora`라는 에디터를 활용해서 작성하는데, 이때 이미지가 자동으로 한 폴더에 모이도록 하는 설정을 활용합니다.

때문에 `포스팅과 똑같은 이름.assets`라는 폴더가 하나 더 생기게 되고 이때 상대경로로 이미지를 자동으로 찾아오기 때문에 막상 로컬에서는 제대로 동작하는 것처럼 보입니다.

![image-20201217204513035](/assets/img/image-20201217204513035.png)



그러나, 웹에서 해당 포스팅의 URL이 변경되면서 이 상대경로가 제대로 지정되지 않아 이미지가 불러와지지 않는 오류가 발생합니다.

![image-20201217204655892](/assets/img/image-20201217204655892.png)

아래 이미지에서 보듯이 URL에 보시면 `{날짜}`/`{title}`의 형식으로 되어 있는 것을 알 수 있습니다.



### 해결

이 문제를 해결하는 방법은 생각보다 **간단**하지만, **귀찮은 작업**이 될 수 있습니다.

해결방법은 `절대경로`를 이용하는 것입니다.

다시 파일트리를 살펴보면, `assets`폴더가 있습니다.

![image-20201217205015321](/assets/img/image-20201217205015321.png)

저의 경우 포스팅에 사용하는 이미지들은 모두 `img`라는 폴더에 넣어두고 해당이미지의 `절대주소`를 마크다운에 링크해두었습니다.

정리하면, 

1. assets에 img폴더를 만든다

2. 포스팅에 쓰인 img들을 모두 `/assets/img` 안에 넣는다. (복사 또는 이동)

3. 포스팅 내에 이미지들의 링크를 모두 다음과 같이 변경한다.

   ```markdown
   ![Foo](/assets/imge/Foo.jpg)
   ![Bar](/assets/imge/Bar.png)
   ```

   

이렇게 처리한 뒤 `git push`해보면 이미지까지 제대로 포스팅 된 것을 확인하실 수 있습니다 :smile:



혹시 참고하셔도 포스팅에 어려움을 겪으신 경우 댓글에 문의해주세요.

---

Copyright: likelionSungGuk 조성국