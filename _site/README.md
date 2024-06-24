# GeunSuYoon.github.io

- 개인적인 공부 내용을 정리하기 위해 만든 블로그
- 처음 만드는 것은 [이곳](https://supermemi.tistory.com/entry/%EB%82%98%EB%A7%8C%EC%9D%98-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-Git-hub-blog-GitHubio)을 참고했습니다.
- 이후 내부 내용 추가 및 오류 수정은 [이곳](https://devpro.kr/posts/Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-(1)/)을 참고했습니다.
- 테마는 [Monos](http://jekyllthemes.org/themes/monos/)입니다.

### 오류 처리
#### bundle ca 인증서 문제
- linux에선 명령어 입력을 통해 자동으로 해결할 수 있는 문제이지만 windows에선 직접 해결해야한다.
- 검색을 통해 내부에 필요없는 파일을 지워주자. 나같은 경우엔 [이 블로그](https://devpro.kr/posts/Github-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0-(3)/)를 참고해 _posts 파일을 지워줬다.

#### bundle exec jekyll serve 문제
 `require': cannot load such file -- webrick (LoadError)
 - 위와 같은 오류가 발생했다. 말 그대로 webrick이 필요하다는 뜻.
- bundle을 이용해 webrick을 설치해주자.
`bundle add webrick`
