Nestable with 5 little callbacks and method 'dragStopAbort'
========

## This is a modified version of Nestable

Original can be found here: https://github.com/dbushell/Nestable

 * Now, after the 'feedback.abort = true', the item return to original position. The method called is the 'dragStopAbort'. The index and parent index were needed.

## Example JS
```
$('#nestable').nestable({
}).on('beforeDragStart', function(handle) {
    console.log('dragStart', handle);
})
.on('dragStart', function(event, item, source) {
    console.log('dragStart', event, item, source);
})
.on('dragMove', function(event, item, source, destination) {
    console.log('dragMove', event, item, source);
})
.on('dragEnd', function(event, item, source, destination) {
    console.log('dragEnd', event, item, source, destination);
})
.on('beforeDragEnd', function(event, item, source, destination, position, feedback) {
    // If you need to persist list items order if changes, you need to comment the next line
    if (source[0] === destination[0]) { feedback.abort = true; return; }

    feedback.abort = !window.confirm('Continue?');
})
.on('dragEnd', function(event, item, source, destination, position) {
    // Make an ajax request to persist move on database
    // here you can pass item-id, source-id, destination-id and position index to the server
    // ....

    console.log('dragEnd', event, item, source, destination, position);
});
```
## Example HTML
```
<div class="dd" id="nestable">
        <ol class="dd-list">
            <li class="dd-item" data-id="1" data-order="1">
                <div class="dd-handle">1 - Lorem ipsum</div>
            </li>
            <li class="dd-item" data-id="2" data-order="2">
                <div class="dd-handle">2 - Dolor sit</div>
                <ol class="dd-list">
                    <li class="dd-item" data-id="3" data-idparent="2" data-order="1">
                        <div class="dd-handle">3 - Adipiscing elit</div>
                    </li>
                    <li class="dd-item" data-id="4" data-idparent="2" data-order="2">
                        <div class="dd-handle">4 - Nonummy nibh</div>
                    </li>
                </ol>
            </li>
            <li class="dd-item" data-id="5" data-order="3">
                <div class="dd-handle">5 - Consectetuer</div>
                <ol class="dd-list">
                    <li class="dd-item" data-id="6" data-idparent="5" data-order="1">
                        <div class="dd-handle">6 - Aliquam erat</div>
                    </li>
                    <li class="dd-item" data-id="7" data-idparent="5" data-order="2">
                        <div class="dd-handle">7 - Veniam quis</div>
                    </li>
                </ol>
            </li>
            <li class="dd-item" data-id="8" data-order="4">
                <div class="dd-handle">8 - Tation ullamcorper</div>
            </li>
            <li class="dd-item" data-id="9" data-order="5">
                <div class="dd-handle">9 - Ea commodo</div>
            </li>
        </ol>
</div>
```
* * *

Original Author: David Bushell [http://dbushell.com](http://dbushell.com/) [@dbushell](http://twitter.com/dbushell/)

Copyright © 2012 David Bushell | BSD & MIT license
