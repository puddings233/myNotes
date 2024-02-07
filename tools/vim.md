[video](https://www.bilibili.com/video/BV1CV4y167RA/)
## three kinds of Ctrl+V
**^V** or **&lt;C-V>** or **Ctrl-V**
## mode
#### normal +  
- **i** or **a** to insert  
- **R** to replace 
- **v** to visual
- **&lt;S-V>** to visual line
- **&lt;C-V>** to visual block
- **:** to command line 
#### other +
- **&lt;ESC>** to normal  
## keys  
- **:sp** create new window(like window manager)  
#### move function
- **w** move to forward by one word
- **b** move to backward by one word
- **e** move to end of the word
> **w**:wold **b**:back **e**:end  
- **0** move to beginning of a line  
- **$** move to end of a line   
- **^** move to the first non-empty character on a line   
> in regex **0, $, ^** is the same mean
- **&lt;C-U>** go up  
- **&lt;C-D>** go down
> **u**:up **d**:down    
- **G** move all the way down  
- **gg** move all the way up  
- **L** move the lowest on the screen  
- **M** move the middle on the screen  
- **H** move the highest on the screen  
> **L**:lowest **M**:middle **H**:highest  
> have remap the L,so L will not work for me
- **f + "any letter"** move to the first "any letter" after cursor   
- **F + "any letter"** move to the first "any letter" in front of cursor   
- **t + "any letter"** jump to the first "any letter" after cursor   
- **T + "any letter"** jump to the first "any letter" in front of cursor   
> **f** means **find** and include the **"any letter"** while **t** means **to** and not include **"any letter"**
#### edit function
- **y** yank(copy)，need combine with move function  
- **p** paste，need combine with move function  
- **d** delete，need combine with move function  
- **c** change, like "d" but after delete it will enter insect mod  
> these function can also combine with visual mod
- **o** open new line below and enter insect mod  
- **O** open new line above and enter insect mod  
- **x** delete the character on cursor  
- **r + "any letter"** replace the character on the cursor by "any letter"  
- **u** undo changes  
> have remap the u,so u will not work for me
- **&lt;C-R>**  redo changes  
- **~** change the case of the character, normally combine with visual mod  
- **i** inside, combine with y, p, d, c 
- **a** around, combine with y, p, d, c 
> e.g **di(** means delete anything in () but keep (), while **da(** will delete ()  
