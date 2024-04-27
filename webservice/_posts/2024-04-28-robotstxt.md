---
layout: post
categories:
  - webservice
title: "[WEB] robot.stxt"
date: 2024-04-24 01:53:00 +09:00
tags:
---
# \[WEB] robots.txt

>SEO를 높이기 위한 방법 중 하나인 robots.txt에 대한 설명이다.

- robots.txt는 크롤러가 사이트의 섹션에 엑세스 하지 못하도록 하는 규칙이 적힌 파일이다.
- 다르게 말하면 \"우리 사이트의 여기 저기를 확인해주세요!" 하는 가이드를 제공하는 역할을 한다.

---

## 규칙

- 파일 이름은 robots.txt여야 한다.
- 사이트에는 robots.txt는 하나만 있어야 한다.
- 웹사이트 호스트의 루트에 있어야 한다.
	- 예를 들어 \https://www.example.com/ 아래 모든 URL에 관한 크롤링 제어하려면  \https://www.example.com/robots.txt에 존재해야 한다.
		- 하위 디렉토리에 배치하면 안된다!!
- 하위 도메인 또는 비표준 포트에 게시할 수 있다.
	- 하위 도메인 예시: '\https://**website.**\example\.com/robots.txt'
	- 비표준 포트 예식: '\https://example.com\\**:8181**/robots.txt'
- 게시된 프로토콜, 호스트, 포트 내의 경로에만 적용된다.
	- 위 경로에 배치한 robots.txt 규칙은 '\https://**m.**\example\.com/'과 같은 하위 도메인이나 '**http**://example.com/'과 같은 대체 프로토콜에는 적용되지 않는다.
- ASCII를 포함한 UTF-8로 인코딩된 텍스트 파일이어야 한다.
	- UTF-8 범위 외 문자는 무시할 수 있어 robots.txt의 규칙이 무효화될 수 있다!!

--- 

## 예시

- 아래는 [google for developers](https://developers.google.com/search/docs/crawling-indexing/robots/robots_txt?hl=ko)에서 제시한 example이다.

`# This robots.txt file controls crawling of URLs under https://example.com.`
`# All crawlers are disallowed to crawl files in the "includes" directory, such`
`# as .css, .js, but Google needs them for rendering, so Googlebot is allowed`
`# to crawl them.`
`User-agent: *`
`Disallow: /includes/`

`User-agent: Googlebot`
`Allow: /includes/`

`Sitemap: https://example.com/sitemap.xml`

---

## 구문

- Sitemap을 제외한 모든 규칙은 경로 접두사, 접미사에 와일드카드 \*를 지원한다.

### User-agent: ${User-Agent}

- ${User-Agent}는 제어할 robots의 이름이다.
- 대표적인 예시는 아래 표와 같다.

| 이름           | User-Agent      |
| ------------ | --------------- |
| Google       | Googlebot       |
| Google Image | Googlebot-image |
| Msn          | MSNBot          |
| Naver        | Yeti            |
| Daum         | Daumoa          |
| ChatGPT      | ChatGPT-User    |
- 위 예시에서 \*를 쓴 이유는 모든 robots의 크롤링을 제어한 것이다.

### Disallow: ${DIR}
- 위에 적은 ${User-Agent} robot의 ${DIR} 디렉토리 내부 접근을 차단한다.
- 모든 접근을 차단하려면 \'/'을 적으면 된다.

### Allow: ${DIR}
- 위에 적은 ${User-Agent} robot의 ${DIR} 디렉토리 내부 접근을 허용한다.
- 모든 접근을 허용하려면 \'/'을 적으면 된다.

### Sitemap: ${URL}
- ${URL}은 웹사이트의 사이트맵 위치이다.
- 정규화된 URL이어야 한다.
	- 구글의 경우 http, https, www를 포함하는 URL과 대체 URL을 가정하여 확인하지 않는다.
	- 웬만해선 URL의 전문을 다 써야 한다!!

- 첫 페이지를 제외한 나머지 페이지 접근을 차단하려면 다음과 같이 작성하면 된다.

`User-agent: \*`
`Disallow: /`
`Allow: /$`
 