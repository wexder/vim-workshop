# Editing and more movements

Now that we can enter "insert" mode and type some text we need to learn how to do proper editing.
Because when we want to delete something, we can just move our cursor there, enter "insert" mode and delete something, but that seems like too much.
Instead we can just use the `x` to delete correct character under the cursor.
But again for long words, this is exhausting. What we can do instead is to select the text in visual mode and again press `x`.

Ok, but I've just deleted parts of this tutorial. Don't worry to undo your action use `u` as many times as you want to.
To redo we can use the `Ctrl-r`.

Let's learn some better navigations so we can move around faster and edit thing more effectively.
Here we have perhaps the move famous javascript function lately the Left pad.

``` js
function leftPad (str, len, ch) {
  // convert `str` to a `string`
  str = str + '';
  // `len` is the `pad`'s length now
  len = len - str.length;
  // doesn't need to pad
  if (len <= 0) return str;
  // `ch` defaults to `' '`
  if (!ch && ch !== 0) ch = ' ';
  // convert `ch` to a `string` cuz it could be a number
  ch = ch + ''; // cache common use cases
  if (ch === ' ' && len < 10) return cache[len] + str;
  // `pad` starts with an empty string
  var pad = '';
  // loop
  while (true) {
    // add `ch` to `pad` if `len` is odd
    if (len & 1) pad += ch;
    // divide `len` by 2, ditch the remainder
    len >>= 1;
    // "double" the `ch` so this operation count grows logarithmically on `len`
    // each time `ch` is "doubled", the `len` would need to be "doubled" too
    // similar to finding a value in binary search tree, hence O(log(n))
    if (len) ch += ch;
    // `len` is 0, exit the loop
    else break;
  }
  // pad `str`!
  return pad + str;
}
```

The most used movement shortcuts are `e` to jump to the end of the next word and `w` to just to the start of next word.
Of course we can also jump back by using `b` to the start of the word, the end of the word is little more complicated by using `ge`.
All of these can be used in the "visual" modes to move faster when selecting something.
There is also `{` and `}` to jump between paragraphs. And `(`,`)` to jump around sentences. But these are generally not that useful when editing code.

On the other hand being able to find characters fast is super useful. Use `f` followed by character you want to jump to on the line for "e" `fe`. But if we want to go further ? Then `;` is our friend.
This will move us to the next occurrence of our character. To jump back to character use `F`.

Sometimes (we just want to select) something inside parenthesis. This brings us to the advanced usage of the visual mode.
There are two keys you can use in visual mode to make selecting much easier. To select something "inside" we can you `i`.
(For example to select something inside parenthesis) we can use `vi(`, this also works different parenthesis with `}` or `[`.
Of course for our frontend friends there's also option to do it in html/jsx with `t` so `vit`.
```html
<body>
 <p> Nice </p>
</body>
```
But we can do this with quotes `"`, `'` or even with `w` words, `s` sentences or `p` paragraphs. To include parenthesis or whitespaces use `a` instead of `i`.

When we select something we can again use `x` to delete, but what if we want edit it after ? We can just press `xi` to delete and "insert", but there's better way.
The 'c' key does exactly that, deletes and enters "insert" mode. Some to edit the body of function we can do 'vi{c'.
 
For quick search and jump the `/` followed by regexp pattern can be used. While in this mode to cycle between occurrences use `Ctrl-g` and `Ctrl-t` or comfirm with `Enter`.
Now we can jump around the highlights with `n` and `N`. To clear selection use `:noh` command.

Last useful "normal" mode edit feature is replace `r`, we can again replace either single character or whole selection.

Illustration of what we can delete:
	"dl"	delete character (alias: "x")	    
	"diw"	delete inner word			         
	"daw"	delete a word				         
	"diW"	delete inner WORD 		             
	"daW"	delete a WORD 	                     
	"dgn"   delete the next search pattern match 
	"dd"	delete one line				         
	"dis"	delete inner sentence			     
	"das"	delete a sentence			         
	"dib"	delete inner '(' ')' block	
	"dab"	delete a '(' ')' block		
	"dip"	delete inner paragraph		
	"dap"	delete a paragraph			
	"diB"	delete inner '{' '}' block	
	"daB"	delete a '{' '}' block		


## Copy

Copy is little complicate and for some people it might be confusing.
Vim doesn't by default use the system clipboard, but instead have concept of registers. 
Which are basically places where you can store text. The advanced usage of registers are out of scope for this tutorial.
But we will be setting up vim to use the clipboard from your system.

Now vim call copying "yanking" so to yank something we selectect it and use `y`. Just for context this saved the selection to
register "0", use `:reg 0` to see what you saved.
To paste it back, move your cursor where you want to paste it and pres `p`.

To confuse people a little you can also yank whole lines and when pasting them, instead of pasting them after your cursor they are pasted on the next line.
Yanking the whole line is done with `yy`.

Second twist is that vim also saves almost every operation in visual mode to registers. For example if you delete lien `dd`
it's saved the same way as if you would yank the whole like `yy`.
