# Forkify

![Forkify](https://i.postimg.cc/NGKyjkJT/aa.png)

Demo: https://hopeful-banach-e9acd3.netlify.app/

## 簡介 Introduction

```
使用 原生 JavaScript 開發的食譜查詢網站
```

## 使用技術 Technologies

> 採用 MVC 架構來將關注點分離，其中 View 的部分使用 ES6 Class 來實作，再利用 Extends 去 inheritance View 的原型  

![Forkify](https://i.postimg.cc/mrhzqvnc/forkify-architecture-recipe-loading.png)  

> 採用 Publisher-Subscriber pattern，去有效執行 MVC 的規範，不讓 Controller 逾矩去做 View 的事情

![Forkify](https://i.postimg.cc/zBzg7Lrr/image.png) 
![Forkify](https://i.postimg.cc/FFfR4bG6/image.png) 

> 在 Class 中使用 private data 以及 private method 確保資料不會受外部影響

![Forkify](https://i.postimg.cc/TPyjm5fH/image.png) 

> 採用 DOM Algorithm 來針對需要改變節點做畫面更新，避免不需要的重新渲染

```
  update(data) {
    // 更新渲染結果 (不重新渲染整個 recipeView)
    this._data = data;
    const newMarkup = this._generateMarkup();

    // 產生 virtual DOM (更新過後) 去和網頁上現有的 DOM (原本) 去做比對
    const newDOM = document.createRange().createContextualFragment(newMarkup);
    const newElements = Array.from(newDOM.querySelectorAll('*'));
    const curElements = Array.from(this._parentElement.querySelectorAll('*'));

    newElements.forEach((newEl, i) => {
      const curEl = curElements[i];

      // Update change TEXT
      if (
        !newEl.isEqualNode(curEl) &&
        newEl.firstChild?.nodeValue.trim() !== ''
      ) {
        curEl.textContent = newEl.textContent;
      }

      // Update change ATTRIBUTE
      if (!newEl.isEqualNode(curEl))
        Array.from(newEl.attributes).forEach(attr => {
          curEl.setAttribute(attr.name, attr.value);
        });
    });
  }
```

## 特色及功能 Features
> 上方搜尋欄輸入食物名即在側邊顯示結果(pagination)，點選任意食譜呈現在畫面右側

![Forkify](https://i.postimg.cc/T1ZjtR0J/image.png) 


> 可隨意調整食譜份量(人數)，右側 icon 可加入我的最愛(localStorage)

![Forkify](https://i.postimg.cc/J7cBg5nW/image.png) 

> 點選 ADD RECIPE 即可新增個人食譜

![Forkify](https://i.postimg.cc/VvGsw6pX/image.png) 

> 右上方顯示我的最愛，可直接導覽到該食譜

![Forkify](https://i.postimg.cc/kgjHyS8Q/bb.png) 

## 聲明 Statement

- 僅作為個人作品練習，所有資料皆來自網路，無商業用途
- 圖片來源: Unsplash、Google、Closetcooking
