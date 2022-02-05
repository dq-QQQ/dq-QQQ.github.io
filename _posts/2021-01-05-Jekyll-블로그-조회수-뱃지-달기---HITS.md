---
title: Jekyll 블로그 조회수 뱃지 달기 - HITS
date: 2021-01-05 20:18:01
permalink: /:short_year-:month-:day/:title
categories:
- jekyll

tags: [jekyll, blog, github pages, 깃헙페이지, 지킬 블로그, hits]
---

# 방문자에게 게시글 조회수 보여주는법

Jekyll과 같은 정적 블로그는 간편한 것이 장점입니다. 하지만 DB가 없기 때문에 누적 방문자 수를 체크하기가 어렵다는 단점이 있습니다.

이것을 해결하기 위해서는 써드파티 앱인 **[HITS](https://github.com/dwyl/hits)**를 사용하면 간단하게 해결가능합니다.

 **[HITS](https://github.com/dwyl/hits)**는 github repository에 방문하는 사람들을 세기 위한 프로젝트로 만들어졌다고 합니다. 아래 이미지에 표시된 부분은 **[HITS](https://github.com/dwyl/hits)**의 github repository의 `README.md`의 모습입니다.

![image-20210105103446971](/assets/img/image-20210105103446971.png)



#### *! 주의 ! 현재 Hits가 디스크 메모리 문제로 정상적으로 작동하고 있지 않아 잠시 사용을 보류해두었습니다.* 

## jekyll blog에서 Hits 사용하기

Hits를  사용하기 위해서는 적절한 위치에 아래와 같은 코드를 삽입해야 합니다.

```html
<div style="text-align: center;">
    <a
       href="http://hits.dwyl.com/{{ site.url | remove_first: 'https://' | remove_first: 'http://' }}{{ page.url }}"
       target="_blank"
     >
     <img
       src="http://hits.dwyl.com/{{ site.url | remove_first: 'https://' | remove_first: 'http://' }}{{ page.url }}.svg"
     />
    </a>
</div>
```

저는 제목과 본문이 시작하는 사이에 삽입해보았습니다. 적절한 위치를 찾기 위해 `크롬 개발자도구`를 활용해서 찾아보시면 됩니다.

근데 그 위치를 내 blog코드 내에서 찾는 것이 생각보다 복잡합니다. 아래 이미지를 보시면서 파일 트리를 찾으시면 좋습니다.

> '_includes' > '_macro' > 'post.html'

![image-20210105102831674](/assets/img/image-20210105102831674.png)

해당 위치에 삽입하면 아래 이미지와 같이 조회수가 표시됩니다.

![11](/assets/img/11.png)

---

references

[Hits 생성기](http://hits.dwyl.io/)

[Hits Github repository](https://github.com/dwyl/hits)

[HITS!를 이용하여 Jekyll 블로그에 조회수 배지 달기](https://ryanking13.github.io/2020/03/09/jekyll-views-count-badge.html)