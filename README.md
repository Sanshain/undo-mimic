## undo-mimic
Emulating undo and redo actions for textarea and input page elements

### Usage

Simple usage:

```
import { storeMultiactions, storeAction, undo } from "./undoManager/initialize";
import main from './undoManager/initialize';

var editor = null;
function initialize(){
  main(editor = document.querySelector('textarea'));
  editor.onkeydown = () => {
    if (event.ctrlKey && event.code === 'KeyZ') undo(event);
  }
  document.querySelector('button').onclick = () => {
      
		storeAction(event, () => editor.value += '123');
    editor.selectionStart = editor.selectionEnd = editor.value.length - 1;
    editor.focus();
  }
  document.querySelector('button_2').onclick = () => {
    
		storeMultiactions(event, () => editor.value = '123');
    editor.selectionStart = editor.selectionEnd = editor.value.length - 1;
    editor.focus();
  }  
}

```

Usage with [ta-hotkeys](https://github.com/Sanshain/ta-hotkeys):

```
  document.querySelector('button').onclick = () => {
    	let caret = editor.selectionStart;
	let preformat = storeAction(event, () => {
		var preformat = formatAction(line, event); // some actions
		editor.value = preLine + preformat.line + postLine;
		return preformat;
	}, {
		startLine: startLine, endLine: endLine
	})

	if (preformat.eventAbort) event.preventDefault();
	// selection turns back:
	editor.selectionStart = editor.selectionEnd = caret + preformat.offset * (preformat.undo ? -1 : 1);  
  }
```

### API:

- `main` - initialize editor element
- `undo` - undo action
- `storeAction` - store one line action inside callback
- `storeMultiactions` - store action inside callback for actions under selected multiline text

### Installation

```
npm i Sanshain/undo-mimic
```
