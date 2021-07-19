
![](https://img.shields.io/npm/dy/swipe-angular-list.svg)
![](https://img.shields.io/github/stars/leifermendez/swipe-angular-list)
![](https://img.shields.io/github/license/leifermendez/swipe-angular-list)
# Angular Swiper List (swipe-angular-list)

You can now have a swipe effect on your Angular application, with which you can place delete or edit options. Ideal for task list or contacts.

__[VER DEMO](https://stackblitz.com/edit/angular-ejzvpz)__

<a href="https://www.buymeacoffee.com/leifermendez" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p  align="center">
<small>Preview</small>
<br>
<img src="https://i.imgur.com/WGotbov.png"  alt="Preview 1" />
</p>

----

<p  align="center" style="display:flex;justify-content: space-between;width:100%;align-content: center;">
<b>Examples</b><br>

<img height="400" src="https://i.imgur.com/qMXkbXm.gif"  alt="Preview 1" />
<img height="400" src="https://i.imgur.com/LspDKT6.gif"  alt="Preview 2" />
<img height="400" src="https://i.imgur.com/orpXyIv.gif"  alt="Preview 3" />
</p>


### Install

`npm i swipe-angular-list@latest --save`

### Import

__main.ts__

Import `hammerjs`

```typescript

import './polyfills';
import 'hammerjs'; // < ----- ********************************  IMPORT
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

```

__app.module.ts__

```typescript

import { BrowserModule, HammerModule } from "@angular/platform-browser";
import { NgModule } from "@angular/core";
import { AppComponent } from "./app.component";

import { SwipeAngularListModule } from "swipe-angular-list"; // <------ IMPORT

@NgModule({
  declarations: [AppComponent],

  imports: [
    BrowserModule,
    HammerModule, // < ----- ******************************** IMPORTANT ******************
    SwipeAngularListModule, // < ----- ******************************** IMPORTANT ******************
  ],

  providers: [],

  bootstrap: [AppComponent],
})
export class AppModule {}


```
__style.css__
> The scroll doesn't work on mobile devices?
```css
* {
  touch-action: pan-y !important;
}
```
  

### Use

Use in your component

```typescript

import { Component } from "@angular/core";

@Component({
  selector: "app-root",

  templateUrl: "./app.component.html",

  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  title = "for-test";

  list = [
    {
      id: 1,
      title: "Realizar la tarea asignada!",
      subTitle: "9:00pm",
    },
    {
      id: 2,
      title: "Visitar al perro en casa de tu amiga",
      subTitle: "9:00pm",
    },
    {
      id: 3,
      title: "Llamar al doctor",
      subTitle: "9:00pm",
    },
    {
      id: 4,
      title: "Buscar el auto en el taller",
      subTitle: "9:00pm",
    }
  ];

  action = (a) => {
    console.log(a);
  };
  
  swipeCallback = (a) => {
    console.log('Callback Swipe', a);
  }
}

```

### Template

```html

<div>
  <h3 style="text-align: center;">Task List</h3>

  <div>
    <sw-item-list
      *ngFor="let item of list"
      [inside]="item"
      [item-class]="'list-custom'"
      [editTemplate]="editTemplate"
      [trashTemplate]="trashTemplate"
      (callback)="action($event)"
      (swipeCb)="swipeCallback($event)">
    </sw-item-list>
  </div>
</div>

!<-- Defined yout template for icon button (edit)-->

<ng-template #editTemplate>
  <i class="fas fa-edit"></i>
</ng-template>

!<-- Defined yout template for icon button (trash)-->

<ng-template #trashTemplate>
  <i class="fas fa-trash"></i>
</ng-template>

```

### Options

__item__ structure defined :

``` text
{
   "id":1,
   "title":"Realizar la tarea asignada!",
   "subTitle":"9:00pm"
}

```
### Inputs
| Name   |      Default      |  Description |
|:----------:|:-------------:|:------:|
| item-class |  (string) '' | name of style class custom |
| show-mark |   (boolean) true   |   boolean show icon done or not |
| editTemplate | (TemplateRef) or null |  template for edit button |
| trashTemplate | (TemplateRef) or null | template for trash button | 
| markTemplate | (TemplateRef)  | template for icon check template | 
| notMarkTemplat | (TemplateRef) | template for icon not check template |
  
### Output
| Name   |      Default      |  Description |
|:----------:|:-------------:|:------:|
| (callback) |  (function) | function callback click option |
| (swClick) |  (function) | click on item |
| (swipeCb) |  (function) | function callback swipe item | 


``` html

<sw-item-list
  *ngFor="let item of list"
  [inside]="item"
  [item-class]="'list-custom'"
  [show-mark]="true"
  (swClick)="click(item)"
  (swipeCb)="swipeCallback($event)"
  [editTemplate]="editTemplate"
  [trashTemplate]="trashTemplate"
  [markTemplate]="defaultMark"
  [notMarkTemplate]="defaultNotMark"
  (callback)="action($event)"
>
</sw-item-list>

```


#### Example completed
```html 
<div>
  <h3 style="text-align: center;">TASK LIST</h3>
  <div>
    <sw-item-list
      *ngFor="let item of list"
      [inside]="item"
      [item-class]="'list-custom'"
      [show-mark]="false"
      [disable-mark]="item?.disable"
      (swClick)="click(item)"
      [editTemplate]="editTemplate"
      [trashTemplate]="trashTemplate"
      [markTemplate]="defaultMark"
      [customTemplate]="customTemplateSrc"
      [notMarkTemplate]="defaultNotMark"
      (callback)="action($event)">
    </sw-item-list>
  </div>
</div>

<ng-template #editTemplate>
  <i class="fas fa-edit"></i>
</ng-template>

<ng-template #trashTemplate>
  <i class="fas fa-trash"></i>
</ng-template>

<ng-template #defaultMark>
  <i class="far fa-check-circle"></i>
</ng-template>

<ng-template #defaultNotMark>
  <i class="far fa-circle"></i>
</ng-template>

<ng-template #customTemplateSrc let-item="item" let-id="id">
  <div style="display: flex;">
    <div style="padding-right: 10px;">
      <img
        style="width: 60px; height: 60px; border-radius: 60px;"
        [src]="'https://api.adorable.io/avatars/400/' + id + '.png'"
        alt=""/>
    </div>
    <div>
      <h3 style="margin-top: 0; margin-bottom: 0;">Lorem, ipsum dolor.</h3>
      <small style="color: gray; font-weight: 500;">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Non,optio.
      </small>
    </div>
  </div>
</ng-template>

```
