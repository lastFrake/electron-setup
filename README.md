# Инсталятор для electron

1) Инициализировать пустой проект
```
npm init --yes
```
2) Установить electron
```
npm install electron -d
```
3) Глобально установить упаковщик
```
npm install electron-builder -g
```
4) Создать main.js в папке src
```javascript
const electron = require('electron');
const app = electron.app;
const BrowserWindow = electron.BrowserWindow;
let mainWindow;
function createWindow() {
    mainWindow = new BrowserWindow({
            width: 1024, 
            height: 768,
            webPreferences:{
                nodeIntegration:true
            }
        });
    mainWindow.loadURL('http://example.com/');
    mainWindow.on('closed', function () {
            mainWindow = null
        })
}
app.on('ready', createWindow);
app.on('window-all-closed', function () {
    if (process.platform !== 'darwin') {
        app.quit()
    }
});
app.on('activate', function () {
    if (mainWindow === null) {
        createWindow()
    }
});
```
5) Изменить package.json
```javascript
{
  ...
  "productName": "Example App",
  "main": "src/main.js",
  "scripts": {
    "start": "electron .",
    "pack": "electron-builder"
  }
  ...
}
```
6) Локальный запуск
```
npm run start
```
7) Упаковка инсталятора
```
npm run pack
```
