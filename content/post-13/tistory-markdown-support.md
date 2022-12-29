## 목표

-   마크다운 문법을 이용해 티스토리를 작성 할 수 있다.

## 소개

우선 마크다운 라이브러리로 [이 라이브러리를](https://github.com/sindresorhus/github-markdown-css) 사용할건데요.  
오픈소스는 저 링크⬆️ 에서 확인하시고, 세팅은 짧게 블로그 내용만 참고하시면 됩니다.

## Get Start

<img src="https://github.com/jyeonjyan/blog-archive/blob/main/assets/13/tistory-select-docs-type.png" alt="alt를 캡션으로 사용">

스킨편집 > HTML 편집에서 신행하실 수 있습니다.  
아래 코드를 `</head>` 직전에 붙여넣어주세요.

```html
<link href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/5.1.0/github-markdown.min.css" rel="stylesheet">
```

CSS에는 아래 코드를 추가해주면 됩니다.

```css
.markdown-body { 
	box-sizing: border-box; 
	min-width: 200px; 
	max-width: 980px; 
	margin: 0 auto; 
	padding: 45px; 
} 

@media (max-width: 767px) { 
	.markdown-body { 
		padding: 15px;
	} 
}
```

## 결과

아래 사진과 같이 마크다운 파일로 편하게 작성하다가 tistory에 붙여넣기만 하면된다.
근데 이 방법으로는 생산성을 높이는데 한계가 있는 것 같아서 더 좋은 방법을 찾아야 할 것 같다.

### 아직 부족한 점
1. tistory에 이미지를 첨부 해야 하는데. tistory가 깃헙과 단리 원본 이미지를 가지고 있을 수 없어서 편하게 상대경로를 통한 이미지 파싱이 어렵다.