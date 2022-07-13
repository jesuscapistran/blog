---
title: "commands to work in nvim"
date: 2022-07-12T09:01:32-05:00
draft: false
author: "Jesus Capistran"
tags: ["nvim"]
---

## Exit nvim editor ##

vim or nvim are text editors based on the command line. If you dont know how to exit the nvim interface you shoul type `esc + esc` then write `:q`

- `:q` is the command to leave the nvim or vim editor.

## nvim modes ##

- Normal: You should type `esc + esc` 
- Insert: You should type `i` 
- Visual: You should type `v`


## Move the cursor in the text  ##

In Normal mode of nvim we can use the arrow keys to move in the text but there is a better solution, we can use the right hand using the `h`, `j`,  `k`, `l` keys. 

- `h` move to the right
- `l` move to the left 
- `j` move down
- `k` move up 


If we want to move faster forwar we can use the key `w`  and if we can move faster backward we can use `b`. In the same Normal Mode if we need to me fast forward but at the end of the word we should press the key `e`.  

Finally if we neet to reach the end of a long sentence (line in Normal Mode)  we can use the symbol `$`.

> Note: The purpose of use vim is to rid from the mouse to navigate faster in your editor only with the keyboard. 

## Insert text ##

How to insert text in nvim?

- The easy way is to press `i` key place the text we want and then press `esc + esc`

> Note: If we press esc only one, the editor delay the change from insert mode to the normal mode.

- There is other way to insert text, this is with `a` key. After placing this key we can insert text in front of the cursor.  

- If we type `A` in Normal Mode we will be able to write text at the end of a line. In other words, the Insert Mode is activate at the end of the line.

## Delete text ##

- In Normal Mode we place the cursor on the line and word we want to eliminate then we press the letter `x`

## Save the file ##

- The first way is to use `:w` to write the text 
- The second way is to use the command `:wq` which will save your file but nvim will close the file too. 

## Navigate between files ##
Remeber, to navigate and apply any command we should be in Normal Mode

- `gd` in the same text we can pres `gd` to reach the definition
- `gif` this command will move you to the new file (opening a buffer)
- `ctr + o` Buffer backward
- `ctr + i` Vuffer forward

## Eliminate lines and order lines  ##

To eliminate a whole line we should place the cursor at the beggining of the line, then we will press `dd` to cut the line and then I move the cursor into the line I want to paste the line: 

- Use `<p>` to place one line below the cursor
- Use `<P>` to paste the line one line above where the cursor is. 

> Note: In vim we do not eliminate text, we are cutting with `<dd>`

## Replace text in vim ##

The command replace in nvim works in Normal Mode. First we need to place the cursor infront the letter we want to replace then press `<r>` and write the new letter. 

If we want to replace a whole word we can place the cursor at the beggining of the word then type `<cw>` which means change word. In other words the word is delete to place your new word.  

There is a third command we can use to chane a whole word  and this is `<ciw>`  which means change inner word. This command while delete the whole word no mather where is placed the cursor. The only requirement is we need to be on the desired word. 

## Jump between lines and text search ##

- The command which send you to the beggining of the document we need to press two times de g letter `<gg>`
- If we want to go to the end of the file we should type `<G>` the capital letter G. 
- To search text we will go to Normal Mode and write the text after a forward slash `/search text`. This command will search  from the position of the cursor. To navigate between highlighted words we only press `<n>`. 


## Jump between parenthesis ##

- This command is useful for programming (dictonaries in python, for example). To jump between parenthesis we need to press `<%>` in the keyboard we obtain the % by pressing `shift + 5`. 

## Copy and paste ##

To copy text we need to change to the Visua Mode. Then for getting the visual mode I need to press `<v>`. Inmediatly if we move the cursor, the text will be selected. 

To copy the text we need to type `<y>`
To paste the text in Normal mode we need to type `<p>`


