# color 속성
-색상 지정하기

### 예제
```
<style type="text/css">
/*
HSL : 색조(Hue), 채도(Saturation), 명도(Lightness)로 컬러 표현
HSLA : 색조,채도,명도,알파(투명도)
*/
div{width:300px;height:30px;}
div.c1{background-color:hsl(320,100%,25%);}
div.c2{background-color:hsl(320,100%,50%);}
div.c3{background-color:hsl(320,100%,75%);}

div.c4{background-color:hsla(165,35%,50%,1.0);}
div.c5{background-color:hsla(165,35%,50%,0.8);}
div.c6{background-color:hsla(165,35%,50%,0.6);}
div.c7{background-color:hsla(165,35%,50%,0.4);}
div.c8{background-color:hsla(165,35%,50%,0.2);}

</style>
</head>
<body>
<div class="c1"></div>
<div class="c2"></div>
<div class="c3"></div>

<br>

<div class="c4"></div>
<div class="c5"></div>
<div class="c6"></div>
<div class="c7"></div>
<div class="c8"></div>

</body>
```

### 결과
![](https://velog.velcdn.com/images/so2i/post/d585c502-6261-4ba3-ac1e-0926bedf8b4d/image.PNG)
