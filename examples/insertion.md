## The simplest insertion sample:



```js
  let img = '![](' + event.detail.source + ')'

  // получаем позицию каретки и начала активной строки
  let caret = textarea.selectionStart || 0;    				                // remember caret position
  let startLine = (textarea.value.lastIndexOf('\n', caret - 1));

  // получаем позицию конца активной строки
  let endLine = (textarea.value.indexOf('\n', caret));
  if (endLine < 0) endLine = textarea.value.length;


  let preLine = textarea.value.substr(0, startLine ? startLine + 1 : startLine);            
  let postLine = textarea.value.substr(endLine);          // ~~ (end, textarea.value.length)


  actionhandler.storeAction(
      event, 
      () => ({ 
          line: (
              () => {                             
                  textarea.value = preLine + img + postLine;
                  return { length: img.length }
              })()
          }), 
      {
          startLine: startLine + 1
      }
  );

  textarea.selectionStart = textarea.selectionEnd = caret + img.length
```
