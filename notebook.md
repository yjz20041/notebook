### 取消浏览器保存表单信息 

autocomplete="false",可以加在form上或者单独的input上。但在username和password组合的时候，浏览器会忽略autocomplete。需要用一个hidden password input 辅助：
```html
<input type="password" name="a" tabindex="9999" style="display: block; height: 0px; border: 1px solid transparent; margin-top: -2px;" autocomplete="off" />
<input type="password" name="a" />
```
