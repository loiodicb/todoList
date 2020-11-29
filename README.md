# PWA-TP3

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Functionality

# erasedAll()
the fonction erased all use the function removeItems() to erase all the elements inside the todoList.items using a forEach to go through all the items. a button with a click event has is connect to use the function with the web Interface.

'''angular
  erasedAll(){
        this.todoList.items.forEach(I =>this.todoService.removeItems(I));
    }
'''

# generateQrCode()
The source to execute the procedure can be follwed by this link : [Angular CLI README](https://www.npmjs.com/package/angularx-qrcode).

To replicate this function we need first to do the good import:
* Verify the version of angular with ng -version
    * if your version of angular is 8.x.x
    * install Install angularx-qrcode 2.1.x with Angular 8 with the following command :
```console
npm install angularx-qrcode@~2.1.4 --save
```
You need to import the module inside your **app.module.ts**
```angular
import { QRCodeModule } from 'angularx-qrcode';
```
You need also to declare the module **QRCodeModule** into  the **imports:[]**
```angular
imports: [
    BrowserModule, FormsModule,**QRCodeModule**
  ],
```
in the file **todo-list.component.ts**
I add the an empty string variable, it will be useful to get the the list of item from the todoList.items and push it inside the module to generate the QRcode image :
```angular
 myAngularxQrCode: string = "";
```
In the **todo-list.component.html** file I add a button to connect to the function **generateQrCode()** to excute the creation of the QrCode
and finally I add a controler to create the QrCode.
* This line will create an Qrcode image from the list and display it on our screen
```angular
<qrcode [qrdata]="myAngularxQrCode" [width]="256" [errorCorrectionLevel]="'M'"></qrcode>
```

## Problem/Solution
During the development of this function while the convertion I was not able to see which value was inside the todoList.items, because while I was try to print the contents of my variable the QRCode generated was not changing.

I tried to print the todoList.items and a **object** was printed. I needed to be sure of what was really sent to generate the QRcode.
After some research I need to decode the todolist.items with the function **JSON.stringify()** to convert a Javascript Object String value into a string.
After this I was able to see the modification when I was adding value and generate a new QrCode.