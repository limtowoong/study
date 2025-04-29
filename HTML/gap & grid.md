# gap

flex나 grid 레이아웃에서 요소들 사이의 간격을 설정하는 데 최적화된 속성입니다.

<br>

## 사용 예시
```css
.container {
  display: flex;
  flex-direction: column;
  gap: 20px; /* 요소들 간의 간격을 20px로 설정 */
}
```

<br>

## gap은 **flex-direction**에 따라서 간격의 방향이 달라집니다.
```css
.container {
  display: flex;
  flex-direction: row; /* 기본값 */
  gap: 20px; /* 자식 요소들 간에 가로로 20px 간격 */
}
```
```css
.container {
  display: flex;
  flex-direction: column;
  gap: 20px; /* 자식 요소들 간에 세로로 20px 간격 */
}
```

<br>

# grid

2차원(가로+세로) 레이아웃을 만들기 쉽게 해주는 기술

<br>

## 사용 예시

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

```html
<div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
  <div>5</div>
</div>
```

### 결과
```css
[1] [2] [3]
[4] [5] [ ]
```

<br>

## 요약

| Flexbox                              | Grid                                  |
|--------------------------------------|----------------------------------------|
| 1차원(가로 또는 세로) 레이아웃에 적합     | 2차원(가로 + 세로) 레이아웃에 최적화       |
| "흐름 중심" (콘텐츠 크기에 따라 흐름)     | "레이아웃 중심" (미리 그리드 틀을 짜놓고 배치) |
| 자식 크기 기반 자동 배치                 | 부모가 격자(grid)를 정의함                  |
