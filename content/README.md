# upload convention

## directory convention
업로드 하고자 하는 post의 number(`-p`)를 넣어 `post-p`와 같이 디렉토리를 만든후 하위에 작업한다.  
e.g
```markdown
/post-1
- post-1-title.md
```

## image location with convetion 
tistory-markdown은 github-markdown과 다르게 파일 상대경로 파싱을 통한 이미지 삽입이 불가능하다. github에 올라갈(`~./assets/**`) 원격 이미지 주소를 참조하게 해주면 되는데. 

예를들어
```
절대경로(~./assets/13/tistory-select-docs-type.png)의 원격 주소는 다음과 같을 것으로 예상한다.
원격경로: https://github.com/jyeonjyan/blog-archive/blob/main/assets/13/tistory-select-docs-type.png
```

어차피 깃허브에 올라갈(`git push`) 이미지의 원격 주소는 다음과 같은 convention으로 업로드 되기에 예측샷으로 `<img src="">`의 경로(src)를 참조시키는 것이 지금으로써 가장 빠른 솔루션이라고 볼 수 있다.