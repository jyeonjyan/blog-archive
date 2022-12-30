# upload convention

## directory convention
업로드 하고자 하는 post의 number(`-p`)를 넣어 `post-p`와 같이 디렉토리를 만든 후 하위에 작업한다. (이때 `-p`는 `1` 이다.)  
e.g
```markdown
/post-1
- post-1-title.md
```

이미지는 `~./assets/-p/` 디렉토리를 만든 후 하위에 넣는다.  
e.g
```markdown
/1
- foo-bar.png
```

## image location with convetion 
markdown 문법 `![]()`을 사용하여 이미지를 첨부할 수 있다.