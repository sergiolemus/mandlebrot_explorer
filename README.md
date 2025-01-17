# mandlebrot_explorer

## Purpose:
The purpose of this program is to be an easy to use fractal explorer and a demo of interactivity using the SDL2 library.

## Dependancies:
To install this program, one must have *SDL2* (available from their website or most package managers) and must have lpthreads (available on most POSIX systems)

## Compile & Install:

### ON POSIX SYSTEMS

Tested on MacOS with XCode and on multiple Linux Distros

Clone the repository and run **make && make install** from the *src/* directory. 
This will compile the program and copy it to your **$PATH**.
Depending on your system, *make install* may require administrative privileges.


    $ make && make install

To uninstall the program, run:

    $ make clean && make uninstall


### On Windows

I assume that the code would install on Cygwin / Mingw if you get the appropriate header file. You could also install in the WSL, and host an XServer on Windows.

SDL offers Windows headers so I assume on could import all the headers and files into a Visual Studio to compile.

Finally you could make a VM.

If anyone has tried any of these with success, please let me know.

## Usage:

Run the program, you can then use the:

*Left Click* to recenter the fractal on the mouse

*arrow keys* to coarse pan 

*hjkl*       to fine pan

*+* / *-*    to coarse zoom

*y* / *u*    to fine zoom

*[* / *]* to increase or decrease the amount of iterations done. Decreasing the iterations reduces sharpness but greatly speeds up rendering. It could be nice to allow the image to be blurry while you find an area of interest, speed drawing, then sharpen for desired effect

*i* / *o* increases or decreases the amount of modulo blending. This is crucial to get things to look coherent at
different zoom levels.

*m* toggles to 'modulo view'

*n* toggles to 'histogram view'

Numbers *1 - 4* allow you to toggle between preloaded color maps from *src/config.cpp* (from this repo
1 and 2 are loaded with data, 3 and 4 are not).

*r* to reset your view and scale back to the main fractal

*p* to print the current state, to replicate it

*q* to quit

*t* to pull up the controls menu

All printing statements will show up on the terminal you used to call the program, but effort
will be made to made interactions more graphical.

### Customization:

To customize, copy *src/config.cpp.def* into *src/config.cpp* and make your edits there

*src/config.cpp* is in the .gitignore, so you can edit without worrying about syncing with the repo.

However, beware when you pull if there are changes that will cause your *src/config.cpp* to become incompatable.

In the file, you can modify the color palette, num threads, pixelWidth, etc.

It should be fairly self explanatory.

After customizing, you must re-run make and make install, but it should be fairly quick because only a few cosntants were changed.

##  TODO:

1)  More intellegently setup a color gradient for historgram. Now histogram looks great at some zoom 
    levels but garbage at others. Also more intellegent "bucket" placing for histogram
2)  More intellegently split work between threads, rather than having each take a stripe.
    Maybe guess where the most work would need to be done?
3)  Have a better interface to scroll multiple steps at once, 
    perhaps click and drag and/or boxes to type in Xmin/Xmax Ymin/Ymax
4)  Add GUI elements to ajust the colormap
5)  Add a second window as a "HUD" to show where you are on the fractal
6)  Investigate bug where at high zoom levels thread panes get out of sync
7)  Take advantage that panning reuses many existing pixels to not recalculate everything

## Examples Images

Depending on what you are looking for, both the Historgram and Modulo renderings can look nice.

However, the Modulo rendering tends to be more consistently nice. It also has zoom invariance

The Histogram renderings are a bit finicky in my experience. It tends to look very nice on certain structures and
confused on others. Playing with the gradient, and how much automtic vs manual shading can give you some interesting results.

Here are some comparisons. Look closely at the ring around the mandlebrot itself. The modulo's tend to show more detail 
at the cost of looking bust or almost messy.

By Contrast, around spirals or areas where the set is very thin (little black), the histogram coloring can look very nice.

Modulo:

![Modulo 1]( /screenshots/modulo1.png?raw=true) 

Histogram:

![Histogram 2](/screenshots/histogram2.png?raw=true)

Modulo:

![Modulo 2](/screenshots/modulo2.png?raw=true)

Histogram:

![Histogram 1]( /screenshots/histogram1.png?raw=true) 

## Easter Eggs

It turns out that in modulo mode, holding *i* or *o*, changing the blending of the modulo can make for very neat looking animations that are fun to play with. I might spend more effort making this an animation recording software, I'm not sure.