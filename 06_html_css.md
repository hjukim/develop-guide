# HTML5, CSS3 및 


## 퍼블리싱 UI 작업 시 우선사항

퍼블리싱의 *가장 중요한 것은 **tailwindcss 사용***입니다. *스타일 작업 시 우선사항으로 적극 활용하여 수정이 용이* 하게 하십시오.

- 퍼블리셔가 **커스텀 스타일**을 주는 경우 : **less파일에 정의**

- 클래스 네임 :  **케밥케이스로 '_'언더바**를 사용 (*tailwindcss와 커스텀 스타일을 구분하는 방법)

- 개발자가 커스텀 스타일을 주는 경우 : 클래스 네임을 정의하며 less파일이 아닌 vue파일 하단 스타일 영역에 정의.

  

## CSS Utils(tailwindcss) 사용방법

#### 스타일 작업 시 [CSS Utils: tailwindcss](https://v0.tailwindcss.com/docs/what-is-tailwind/)를 적극 활용하여 작업하십시오.

#### 클래스 정의

##### 클래스로 스타일 지정하기

스타일을 줄 때에 **tailwindcss**에 있는 스타일은 클래스로 지정하여 **수정을 간편**하게 하며 없는 경우에만 *사용자 정의 클래스를 만들어 정의* 하십시오. 사용자 정의 클래스는 `.framework_title`과 같이  **'_'(언더바)**를 이용하여 **케밥 케이스**로 표현하십시오.  

- 재사용이 많이되는 경우 : 1번과 같이 클래스를 만드십시오.
- 재사용이 거의 없는 경우: 2번과 같이 클래스를 만드십시오.

1. 여러 스타일을 하나의 클래스로 정의하는 방식           

   장점 : 재사용시 코드를 간결하게 쓸 수 있다.

   ​           ( `class="framework_title"`만 사용하면 됨)

   단점 :  html 코드만 보고 어떤 스타일이 적용되었는지 알 수 없다. 

   ​           ( `class="framework_title"`만 보고 어떤 스타일이 적용되어 있는지 알 수 없음)

```html
<div class="framework_title">
    UI Framework
</div>
```

```scss
.framework_title {
    width:50%;
    border-b: 1px solid @subColor_08;
    margin-bottom: 7px;
    padding-bottom: 7px;
}
```

2. 사용자 정의 클래스(.framework_title)는 꼭 필요한 스타일만 지정하고 나머지는  tailwindcss 의 클래스를 연결하는 방식

   적용할 스타일이 tailwindcss에 있는 경우 먼저 적용하고 없는 스타일만 사용자 정의클래스로 정의하여 적용합니다.  html코드를 보면 사용자 정의 클래스의 스타일을 제외하고 어떤 스타일들이 적용되어있는지 알 수 있습니다.

```html
<div class="w-1/2 border-b border-solid mb-2 pb-2 framework_title">
    UI Framework
</div>
```

```scss
.framework_title {
    border-color: @subColor_08;
}
```

#### 커스텀 클래스 정의

##### 재사용이 많이 되는 클래스

button과 같이 여러 페이지에서 사용되는 태크의 클래스를 하나로 정의하여 간편하게 사용할 수 있습니다. 반복되는 스타일은 **하나의 커스텀 클래스로 정의**하고 추가로 필요한 스타일은 클래스 기입 부분에 적용하십시오. 

- 예제) 버튼 스타일을 .btn_styl로 적용하십시오.  

  두 버튼의 사이를 조정하는 패딩 값은 클래스 부분에 따로 적용하여 간격 수정을 간편하게 할 수 있게 하십시오.

  ```scss
  /* .btn_style은 반복되는 패턴의 스타일을 @apply를 사용함으로써 재 사용성을 높임 */
  .btn_style {
    @apply border border-solid bg-white rounded text-base;
  }
  ```

  

  두 버튼은 같은 스타일을 가지고 있지만 아래 버튼이 보다 깔끔하게 정리됨

  ```html
  <button class="border border-solid bg-white rounded text-base">저장</button>
  ```

  ```html
  <!-- .ml-2 { margin-left: 0.5rem } 두 버튼의 간격을 조정하는 클래스 추가 -->
  <button class="btn_style ml-2">취소</button>
  ```



#### 커스텀 클래스 응용

`@apply`와 `@responsive`를 한번에 사용하여 반복되는 스타일과 사용자 정의 스타일을 하나의 클래스로 정의해 보십시오. 또 이렇게 만든 클래스를 일반 클래스에도 적용해 보십시오.

- 아래 예제는 버튼 기본 스타일을 정의해 놓은 클래스입니다. **@apply**를 사용해서 다양한 클래스를 만들 경우에는 **@responsive** 안에 클래스를 정의해야 합니다.

```scss
  /* 사용자 정의 클래스에 반복되는 스타일 적용하기 */
  @responsive {
    .btn_base {
      @apply rounded text-base;
      min-width: 80px;
      height: 26px;
      padding: 0 8px;
    }
  }
```

- 기본 스타일로 정의해놓은 `.btn_base` 클래스에 tailwindcss 클래스를 추가하여 다양한 스타일을 만들 수 있습니다. 따라서 `.btn_ver01` 하나의 클래스 만으로 원하는 스타일을 다 적용 할수 있습니다.
- **@responsive**에 기본 클래스를 정의해뒀기 때문에 **@apply**에서사용할 수 있습니다.

```scss
  /* 일반 클래스에 반복되는 스타일 적용하기(사용자클래스도 함께 적용) */
  .btn_ver01 {
    @apply btn_base border border-solid bg-white;
    color: @subColor_01 ;
    border-color: @subColor_01;
    &:focus {
      outline: none;
    }
    &:hover {
      background: @subColor_01;
      color: @subColor_09;
    }
  }
```

#### 커스텀 클래서 재가공

커스텀 클래스에 들어가 있는 스타일의 수정이 필요할 때 사용하는 방법입니다. 위의  `.btn_base`의 패딩값 수정 방법을 예로 들겠습니다.

1. 패딩값을 재정의 하는 클래스를 기존 클래스 안에 추가
2. 패딩값이 다른 새로운 클래스 정의

```scss
// 1. 패딩값을 재정의 하는 클래스를 기존 클래스 안에 추가하여 사용하십시오.
.btn_base {
    @apply rounded text-base;
    min-width: 80px;
    height: 26px;
    padding: 0 8px;
    &.py_5 {
        padding-left: 5px;
        padding-right: 5px;
    }
}
// 2. 패딩값이 다른 새로운 클래스를 정의하여 사용하십시오.
.btn_base_02 {
    @apply rounded text-base;
    min-width: 80px;
    height: 26px;
    padding: 0 5px;
}
```

```html
<!-- 1. .btn_base와 .py_5를 함께 적용 된 모습입니다. -->
<button type="button" class="btn_base py_5">
    이동하기
</button>
<!-- 2. .btn_base_02만 적용 된 모습입니다. -->
<button type="button" class="btn_base_02">
    이동하기
</button>
```

#### 반응형 작업

##### 기본

[반응형 디자인 가이드](https://v0.tailwindcss.com/docs/responsive-design/)를 보며  sm, md, lg, xl를 이용하여 간편하게 클래스를 조작하여 사용하십시오. 모바일 퍼스트로 기준이 잡혀 있으며 모바일, lg, xl 세가지만 정의하여 반응형을 작업하십시오. 세가지 모두 스타일이 같다면 모바일만 정의하고 lg와 xl의 스타일이 같다면 lg만 정의하여 사용하십시오.

- `w-full`: 기본일 적에 사용
- `lg`: 992px 이상일 경우 사용
- `xl`: 1200px 이상일 경우 사용
- 예제) .flex, .flex-wrap을 부모에 적용하여 수평축을 따라 정렬을 시키고 자식이 넓이가 넓은 경우 자식은 복수행으로  나열합니다.  
  lg와 xl이 같을 경우 더 작은 사이즈인 lg만 적용합니다.  

레이아웃을 나누고 필요에 따라 넓이값을 지정한 **자식 태그**에 `margin` 또는 `padding`으로 간격을 조정하십시오.  라벨과 인풋에 넓이값을 직접 입력하지 마시고 **부모태그에 넓이값을 적용**하십시오.

```html
  <!-- .flex { display: flex; }, .flex-wrap { flex-wrap: wrap; } -->
  <div class="flex flex-wrap">
    <!-- 모바일일 경우 .w-full 이고 lg,xl일 때는 .w-1/2 이다 -->  
    <!-- 아이디 -->
    <div class="w-full lg:w-1/2 mt-4">
      <div class="flex flex-wrap lg:mr-2">
        <div class="w-full lg:w-32 text-left">
          <label class="hiwayframe_lbl">
            <span class="icon_lbl">아이디</span>
          </label>
        </div>
        <div class="w-full lg:w-64">
          <input 
            type="text" 
            class="hiwayframe_txt w-full" 
            v-model="formExample.section1.id"
          >
        </div>
      </div>
    </div>
    <!-- 비밀번호 -->
    <div class="w-full lg:w-1/2 mt-4">
      <div class="flex flex-wrap lg:ml-2">
        <div class="w-full lg:w-32 text-left">
          <label class="hiwayframe_lbl">
            <span class="icon_lbl">비밀번호</span>
          </label>
        </div>
        <div class="w-full lg:w-64">
          <input
            type="password"
            class="hiwayframe_txt w-full"
            v-model="formExample.section1.password"
          >
        </div>
      </div>
    </div>
  </div>
```

#### 반응형 작업

##### flex 스타일

`index.vue`의 template은 element인 `el-container`가 감싸고 있으며 기본적으로 `display: flex;` 속성이 적용 되어있습니다. **flex는 반응형에 유리**하며 **복수행를 지정**할 때는 `flex-warp: wrap;` 속성을 적용하여 사용하시기 바랍니다.  반응형은 박스로 되어 있으며 예제, 샘플과 같이 회색 선의 박스는 `.hiwayframe_box` 클래스로 정의 되어 있습니다.  [flex의 기본개념](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Flexbox%EC%9D%98_%EA%B8%B0%EB%B3%B8_%EA%B0%9C%EB%85%90)을 참고 하십시오.

- 최상위에 div에  `.flex`와 `.flex-wrap`를 적용하고 하위 `div`에 넓이값을 적용하십시오. 그리고 그 하위에 간격을 조정하는 마진을 주고 `.hiwayframe_box` 를 적용하여 박스형식으로 나눠줍니다.
- 화면 넓이에 따라 두줄 이상으로 지정할때만 `.flex-wrap`를 지정하십시오.

```html
<!-- .flex { display: flex; }, .flex-wrap { flex-wrap: wrap; } -->
<div class="flex flex-wrap">
    <div class="w-full lg:w-1/2 xl:w-1/3">
        <div class="hiwayframe_box lg:mr-2">
            클래스 적용하기
        </div>
    </div>
    <div class="w-full lg:w-1/2 xl:w-1/3">
        <div class="hiwayframe_box lg:mr-2">
            클래스 응용하기
        </div>
    </div>
</div>
```

#### 반응형 작업

##### @responsive를 이용한 반응형

lg, xl를 이용하여 반응형 작업을 할때는 tailwindcss에 정의 되어있는 클래스만 적용이 가능합니다. `@responsive{ }`를 이용하여 사용자 정의 클래스를 정의 할수 있으며 여러 클래스도 가능합니다. [자세한 내용](https://v0.tailwindcss.com/docs/functions-and-directives/) 참고 하십시오.

```scss
  @responsive {
    .ui_width {
      width: calc(100% / 3 - 4px);
    }
    .ui_margin {
      margin: 0 2px;
    }
  }
```

```html
  <div class="w-full lg:w-1/3 xl:ui_width xl:ui_margin">1</div>
  <div class="w-full lg:w-1/3 xl:ui_width xl:ui_margin">2</div>
  <div class="w-full lg:w-1/3 xl:ui_width xl:ui_margin">3</div>
```

#### tailwindcss 구성파일

커스텀 클래스를 정의할 수도 있지만 구성 파일에 추가시켜 사용할 수도 있습니다. `tailwind.js` 파일에 width값을 추가하여 사용해 보겠습니다.

```js
// .w-1/10과 w-9/10를 추가하였습니다.
width: {
	...
    '1/10': '10%',
    '9/10': '90%'
  },
```

```html
<!-- 커스텀한 클래스로 less파일에 추가하지 않아도 사용이 가능합니다. -->
<div class="flex">
    <div class="w-1/10 text-left">
        <label class="iotframe_lbl">
            <span class="icon_lbl">아이디</span>
        </label>
    </div>
    <div class="w-9/10">
        <input type="text" class="w-full" v-model="formExample.section1.id">
    </div>
</div>
```



## less 사용방법

#### 변수 사용 - 스타일을 변수화 하여 사용

`envs.less`에 사용되는 색상을 변수화 시켜서 적용하면 컬러값을 수정하기 용이합니다. 
변수는 `@`를 사용하여 만듭니다.
아래와 같이 적용되어 있으면 envs.less만 수정하여 모든 컬러값을 한번에 변경할수 있습니다.
`@mainColor01`과 같은 방법을 사용하지 않고 `#fcf` 이렇게 컬러값을 적용했다면 모든 less파일에 컬러값을 찾아가며 수정해야 합니다. [Color 적용 가이드](http://115.90.93.3:1443/sexyguy/abacus-ui-framework/wikis/Color-%EC%A0%81%EC%9A%A9-%EA%B0%80%EC%9D%B4%EB%93%9C)를 참고 하십시오.

```css
/* envs.less */
@mainColor01: #014085;
@mainColor02: #2c2f31;
@mainColor03: #0097a1;
@mainColor04: mainColor03 + #111; /* 16진수로 표현된 색상에 특정 값을 더했다 */

/* main.less */
header {
  color: @mainColor01;
  border: 1px solid @mainColor02;
  background: @mainColor03;
}
```

#### 보기쉬운 중첩규칙

선택자가 중첩되어 상위(부모)속성을 반복해서 기입하지 않아도 됩니다.
그렇기 때문에 부모와 자식이 한눈에 파악됩니다.
`:hover`와 같이 부모 선택자를 참조하는 경우 부모 선택자를 `&`로 참조합니다.

```css
  /* css */
  header { }
  header .ui-box { }
  header .ui-box .li-list { }
  header .ul-box .li-list a { }
  header .ul-box .li-list a:hover { }
```

```scss
  /* less */
  header {
    .ul-box {
      .li-list {
        a {
          &:hover {
          }
        }
      }
    }
  }
```



## style 작업시 유의사항

#### 스타일 순서

less 파일, html class 영역에 스타일을 지정할때 아래순서와 같이 정렬하여 적용하십시오.

##### display(표시)

```scss
.display {
    display: flex;
    flex-wrap: wrap;
}
```

##### overflow(넘침)

```scss
.overflow {
    overflow: hidden;
}
```

##### position(위치)

```scss
.position {
    position: absolute;
    z-index: 9999;
}
```

##### width/height(크기)

```scss
.size {
    width: 100%;
    height: 500px;
}
```

##### padding/margin(간격)

```scss
.interval {
    padding: 4px;
    margin: 10px 0 20px 0;
}
```

##### border(테두리)

```scss
.border {
    border: 1px solid #333;
}
```

##### background(배경)

```scss
.background {
    background: red;
    background-size: auto;
}
```

##### color/font(글꼴)

```scss
.font_style {
    color: #333;
    font-size: 14px;
}
```

#### float 사용 지양

flex를 이용하여 스타일이 적용되어 있으므로 **float 사용없이 정렬이 가능**합니다.  *float는 반응형을 방해하는 요소로 사용을 지양*합니다.

#### important 사용 금지

작업 시 **`!important`  사용을 금지**합니다. **상위 부모부터 기입**하여 important 없이 스타일을 정의 하십시오.

#### ID 사용금지

모든 스타일은 클래스로 주며 id는 사용 할수 없습니다.



## html 작업시 유의사항

#### ID사용 금지

**ID는 전역변수**로 한 문서에 **한 번만 사용**이 가능합니다. 컴포넌트 재사용에 있어서 *오작동을 일으키는 원인* 이 됨으로 `ref`로 대체하여 사용하십시오. [자세한 사용방법](https://kr.vuejs.org/v2/guide/components.html#%EC%9E%90%EC%8B%9D-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%B0%B8%EC%A1%B0)를 참고하십시오.

```html
<div id="menuTree" class="lg:mr-2 menu_tree"></div>
<!-- id를 ref로 변경하여 사용합니다. -->
<div ref="menuTree" class="lg:mr-2 menu_tree"></div>
```

##### 클래스 순서

커스텀클래스는 오른쪽에 기입하고 tailwindcss는 외쪽에 기입하여 스타일 확인을 빨리하며 수정 시 용이하게 합니다.

```html
<div class="btn_vrtcl_align w-full lg:w-3/5 mt-4 lg:mt-0 lg:pr-6 text-right">
```



## Element UI를 이용하여 클래스를 적용하는 방법

html 작업시 꼭 필요한 경우에만  [Component Libs(el-element)](https://element.eleme.io/#/en-US)를 사용하십시오. 라이브러리를 가져와서 디테일한 스타일을 변경 또는 적용시킬 때 *개발자모드에서 클래스 확인 후 작업* 하십시오. el-element를 적용하면 보통 **태그네임**이 **클래스**로 적용되는데 그렇지 않은 경우도 있습니다.

```html
   <!-- index.vue -->
   <el-container>
     <el-main>
       <el-dropdown>
         <el-button>
           추가
         </el-button>
       </el-dropdown>
     </el-main>
   </el-container>
```

```html
   <!-- 개발자 모드에서 볼 때의 클래스 -->
   <section class="el-container">
     <main class="el-main">
       <div class="el-dropdown">
         <!-- el-button은 클래스로 정의되지 않고 button태그로 적용됨 -->
         <button>추가</button>
       </div>
     </main>
   </section>
```

