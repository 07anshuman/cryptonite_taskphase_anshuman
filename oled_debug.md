Looking at the output gif it was clear the mistake had something to do with either incorrect addressing mode or wrong cursor increment. 

How I approached it: 
As per SSD1306 datasheet: `In horizontal addressing mode, after the display RAM is read/written, the column address pointer is increased automatically by 1. If the column address pointer reaches column end address, the column address pointer is reset to column start address and page address pointer is increased by 1.`

which in code i translated to:
```
if column > col_end:
    column = col_start
    page = page+1
```
In my handle_data function:
```
def handle_data(b):
    global column, page, write_count
    if 0 <= page < PAGES and 0 <= column < BUFFER_WIDTH:
        gddram[page, column] = b
    else:
        print(f"[WARN] Out-of-bounds write: page={page}, column={column}")
    if mode == MODE_PAGE:
        column += 1
        if column > col_end:
            column = col_start
    elif mode == MODE_HORIZONTAL:
        column += 1
        if column > col_end:
            column = col_start
            page = page + 1 if page < page_end else page_start
    elif mode == MODE_VERTICAL:
        page += 1
        if page > page_end:
            page = page_start
            column = column + 1 if column < col_end else col_start
    write_count += 1
    if write_count % frame_interval == 0:
        frames.append(render())
```
I keep track of the cursor by keeping track of page + column. For writing one byte of data, it updates gddram[page,column] and increments the cursor by 1 (depending on addressing mode). My approach essentially was a live emulation of SSD1306, as you'd get if you get live incoming bit streaming. It obeys the CMD followed by 0x20, used to convey that the next incoming bit is a command. 

the working script:
```
if (data == '0x21'):
    columns = (int(reader[i+2][2], 16), int(reader[i+4][2], 16))
    pages   = (int(reader[i+11][2], 16), int(reader[i+13][2], 16))
```
here it doesn't work with a cursor at all, instead `0x21` is for `col_start/col_end` and `0x22` is for `page_start/page_end` so basically the frame area is already calculated here by width*height bytes. All the code does is update that particular frame space by the bytes followed. The csv doesn't have a live incoming bit stream instead it has saved capture of exactly where the bytes are. 

<img width="983" height="380" alt="image" src="https://github.com/user-attachments/assets/17543a1c-4be6-426e-92b2-366a73f3c3ce" />

So in the image here 0x21 and 0x22 exactly provided with the dimesnions of how many squares are used. No cursor tracking. Plus because of the emulating behaviour and cursor tracking i had to update the gddram the entire buffer of it keeping the old pixels, hence the overlapping text problem. Look at the write_count and how it is appended in the gddram in the handle_data function above. In the new script it just updates with the given block and so no overlapping behaviour. 

My logic to choosing the live update way was 1. how would i know what one frame of this would look like if i don't follow the CMD structure and protocol of SSD1306 and replicate its behaviour. It made sense looking at the CSV, it looked as if those were commands given and I had to mimic the behaviour to obtain the frames. 
In the datasheet under Addressing modes they had mentioned incrementing after each write (cursor tracking) so again emulation felt logical 
I also looked at the begin few commands of the CSV and it looked like horizontal mode addressing, only solidifying that since there were addressing mode changes in the CSV, the only way was to mimic the behaviour. So I just treated 0x21 and 0x22 as just commands, I didn't see much of it at the beginning of the csv either so didn't think much of it. Instead I should have realised if im getting page and column address I don't need to emulate just use the addresses and print. Now that I look further down in the CSV, it makes so much more sense. 



