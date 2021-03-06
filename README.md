--- COPY OF slab.txt ---

SLAB6 (voxel viewer&editor for VOX/KVX/KV6 files)         by Ken Silverman

   SLAB6 is a highly optimized, purely software-based renderer and editor
for voxel models. The maximum grid size is 256x256x255. Supported formats:
   VOX: Simple uncompressed grid of 8-bit values
   KVX: Voxel sprite format used by the Build engine (Shadow Warrior/Blood)
   KV6: Voxel sprite format used by Voxlap, Evaldraw.

   My first voxel model editor was called SLABSPRI. It was included with
the registered versions of Shadow Warrior and Blood. SLAB6 is a complete
rewrite of SLABSPRI. Only a few features of SLABSPRI have not made it into
SLAB6 - most notably was the archaic facility that converted a series of
carefully crafted 2D images into a 3D model. It never worked really well.
If you want to do this, there's now a much better solution: POLY2VOX.EXE.
POLY2VOX can convert models directly from polygon to voxel format (It can
read the following formats: ASC,3DS,MD2,MD3) The only other useful feature
from SLABSPRI that has not been implemented is a merge feature ('U' in
SLABSPRI).

Some other features that I may implement in a future version of SLAB6:

   * 32-bit color. Would give a better preview for shading of KV6 models.
   * Z-buffer. This would allow better effects in the editor.
   * Use script files to generate 3D objects from 2D images - using PNG/JPG
        instead of ART&PAL (with similar functionality to the complex
        command line options of SLABSPRI).
   * Higher resolution for normals. KV6 uses 8-bit normals, which isn't
        enough for smooth surfaces. This would require a new format. :/
   * Better optimizations. I discovered some new tricks when implementing
        voxel rendering code for Evaldraw. :)
   * Collaborative editing.

----------------------------------------------------------------------------
Command line parameter syntax:

   SLAB6 [VOX/KVX/KV6 file] [/XDIMxYDIM] [/full]   (options can be any order)
   Examples:
      >slab6 duke
      >slab6 worm /512x384
      >slab6 /1024x768 wtc /full
----------------------------------------------------------------------------
Controls:

Hold down LEFT MOUSE BUTTON to change angle (y-inverted mouselook)
Hold down RIGHT MOUSE BUTTON in addition to LEFT MOUSE BUTTON to tilt screen
  4 ARROWS,WASD = move forward,backward,sidestep left/right
 RIGHT CTRL/KP0 = move up/down
     LEFT SHIFT = speed up 2x
    RIGHT SHIFT = speed up 4x
    BOTH SHIFTS = speed up 8x
        , and . = rotate object left/right around the pivot axis
      PGUP/PGDN = rotate object up/down around the pivot axis
    KP/ and KP* = zoom in / out
              / = reset position, orientation, and zoom

              B = set background color to color under cursor
              R = Toggle light source shading mode. Useful for preview in
                     game, and necessary for permanent light command 'F'.
              T = Toggle cube face shading mode. Useful for editing shape.
KP2,KP4,KP6,KP8 = Move light source left/right/up/down
        KP1,KP7 = Change scale of light source (lightmul)
        KP3,KP9 = Change offset of light source (lightadd)
            F12 = screen capture ("SL6D0000.PCX", "SL6D0001.PCX", etc.)


EDITING CONTROLS:

 TAB or RMB = set current color to color under cursor
  BACKSPACE = set current color to -1 (air). Useful for 2D editing.
      SPACE = Paint with current color (NOTE: it is often helpful to hold
                this key down while using the arrow keys / mouse)
SHIFT+SPACE = Paint all nearby voxels. Much faster than using SPACE.
     INSERT = Insert voxel at cursor
     DELETE = Delete voxel at cursor
       HOME = Voxel mold insert (hold it down) Much faster than INSERT.
        END = Voxel mold delete (hold it down) Much faster than DELETE.
        [,] = Change default radius. Valid range is 1-12, default is 4
                Affects these functions: HOME END J ; . CTRL+SPACE
  SHIFT+[,] = Change mold speed (HOME/END keys). The speed is the number of
                 voxels/sec inserted or deleted. Possible values are:
                 16,32,64,128,256,512,1024,2048. Default is 512.

    ENTER = Show / hide 2D slice editor (shows 3 windows, 1 for each axis)
PGUP/PGDN = Change slice number in a 2D slice window
 HOME/END = Change slice number to first or last one in 2D slice window
        ` = Adjust pivot mode: move cursor over 2D slice window and use
               arrow keys to adjust the pivot
        / = When adjust pivot mode is on, use this to center the 3 pivots
      LMB = Hold down to drag one of the windows.
 KP*, KP/ = Press to change the zoom of a 2D slice window.
    SHIFT = Hold down while cursor is in a 2D slice window to copy a
               rectangular region to memory. Works similar to selecting text
               in a text editor.
SH+INSERT = When used while cursor is inside a 2D slice window, it will
               paste the contents in memory to the slice.
        4 = X-flip contents in memory buffer
        5 = Y-flip contents in memory buffer
        6 = Swap X&Y axes of contents in memory buffer

  KP+/KP- = increment / decrement color by 1 (good for fine color editing)
        C = Change all voxels with color under cursor to current color. If
               cursor is in a slice window, then it only affects that slice
        F = Safe floodfill: follow color under cursor (2D slice mode only)
   CTRL+F = Dangerous floodfill: uses cursor color as border, nothing else
               stops it, so make sure you don't have any gaps!
               (2D slice mode only)

        J = Junk function: Force nearby voxels to have different colors.
        ; = Smooth colors, crossing palette groups
        ' = Smooth colors, preserve palette groups

  SHIFT+R = If cursor is in a 2D slice window: Rotates the entire object 90
               degrees (clockwise). The window you choose selects the axis.
            If cursor is in 3D window: Rotates object so that its default
               orientation is aligned to way you're currently looking at it.
  SHIFT+F = Cursor must be in a 2D slice window. Mirror-flips the entire 3D
               object. The window you choose select the axis.
      '=' = Use this to copy a mirror image from the left side of the sprite
              to the right side. It always uses the X-pivot as the mirror
              plane. If you're working on a symmetric object, using this key
              can save you a lot of time!

        L = Quick load VOX/KVX/KV6 file. Another way to load files. I like it
               better than than File..Open from the menu because you can
               quickly load files using the sequence: "L..Down..Enter".

ScrollLock = Toggle 3D selection/drag mode. While in this mode, use:
              KP1,KP3,KP5,KP2,KP4,KPEnter to change selection, and Shift+
              KP1,KP3,KP5,KP2,KP4,KPEnter to move (overwriting like a glacier)

 PALETTE EDITING CONTROLS:
    KP1-6 = When mouse is over palette window and slice editor is enabled,
               use these keys modify the RGB value of the selected palette
               index.
      KP. = When mouse is over palette window and slice editor is enabled,
               use this key to perform interpolation (default is linear:
               gamma=1.0) for RGB between the selected palette index and
               the index under the mouse cursor.
  KP+/KP- = When mouse is over palette window and slice editor is enabled,
               use these keys to change the gamma for KP. interpolation.
               I use this equation for gamma interpolation:
               new_red = ((red0^gamma)*(1-t) + (red1^gamma)*t) ^ (1/gamma)
                  (similar equations for green and blue, 0<=t<=1)

Description of selected menu options:

Save file: KVX format: In versions previous to 12/25/2003, SLAB6 saved only
   the first mip-map level. This results in a smaller file size. However,
   if you want to use your voxel object in the Build Engine, you must save
   all 5 mips. Also, be aware that the (classic) Build Engine can not load a
   KVX voxel model larger than 128x128x200! Anything larger will likely
   crash (classic) Build. SLAB6 can handle up to 256x256x255. It is up to
   you to make sure the limits are not exceeded.

   Note: If you load a KV6 file (written from a version of SLAB6 previous to
   July 2007) directly from the command line, it will use the first 256 colors
   it finds. If you load a KV6 file while inside the editor, it will convert
   the colors to the current palette. As of July 2007, SLAB6 stores a
   suggested palette at the end of KV6 files, so there is no need to also
   write a KVX file to save the palette.

There are 6 rendering methods:
   Dots                  FASTEST         UnderDraws
   Ortho cubes           Fast            Wrong perspective
   Cubes (default)       Slow            Ideal
   Bounded cubes         Fast            OverDraws
   Spheres               Slowest         OverDraws
   Bounded spheres       Fast when far   OverDraws

   Press 'T' to toggle options for the following rendering methods:
      Cubes&Ortho cubes: Toggle face shading. (default=unshaded)
      Spheres/Bounded spheres: Choose big/small spheres (default=small)

Converting to a new color palette: First decide whether you want to replace
   the palette without changing colors, or replace the palette and map to
   the nearest color. (Note that mapping to the nearest color is a lossy
   operation). The palette can be extracted from one of the following file
   formats: PCX,PALETTE.DAT,KVX,VOX,PAL

Hollow Fill: Sometimes, there are holes left in the interior of a model. It
   never hurts to use this tool. Use this function to remove any unexposed
   voxels. Doing so can save precious bytes of disk space, memory, and even
   speed up the rendering.

Optimize dimensions: Reduces voxel dimensions until no side is fully
   transparent. This is done automatically while saving.

Double dimensions: Doubles the size of all 3 axes, duplicating each voxel
   to a size of 2x2x2.

Brighten/Darken all colors by 2x: (In 3D window): darkens/brightens all
   colors in model to half intensity. Changes are permanent and lossy.

Burn Shaded Colors: (In 3D window): applies lighting permanently to model.
   You must enable lighting first using the 'R' key. Once permanent
   lighting is applied to the model, 'R' is automatically turned off. You
   will see that the lighting has been applied permanently when you rotate
   the model.

----------------------------------------------------------------------------
VOX file format:

Both SLABSPRI&SLAB6(D) support a simpler, uncompressed voxel format using
the VOX file extension. Here's some C pseudocode that describes the format:

long xsiz, ysiz, zsiz;          //Variable declarations
char voxel[xsiz][ysiz][zsiz];
char palette[256][3];

fil = open("?.vox",...);
read(fil,&xsiz,4);              //Dimensions of 3-D array of voxels
read(fil,&ysiz,4);
read(fil,&zsiz,4);
read(fil,voxel,xsiz*ysiz*zsiz); //The 3-D array itself!
read(fil,palette,768);          //VGA palette (values range from 0-63)
close(fil);

VOX files use color 255 to define empty space (air). This is a limitation
of the VOX format. Fortunately, KVX doesn't have this problem. For
interior voxels (ones you can never see), do not use color 255, because
it will prevent SLABSPRI/SLAB6(D) from being able to take advantage of
back-face culling.

----------------------------------------------------------------------------
KVX file format:

   I'm always interested in adding more sample voxels to my collection.
Because I'm such a nice guy, I am describing my KVX voxel format here so
you can use them in your own programs.
   The KVX file format was designed to be compact, yet also renderable
directly from its format.  Storing a byte for every voxel is not efficient
for large models, so I use a form of run-length encoding and store only
the voxels that are visible - just the surface voxels.  The "runs" are
stored in the ceiling to floor direction because that is the best axis to
use for fast rendering in the Build Engine.

Each KVX file uses this structure for each of its mip-map levels:
   long xsiz, ysiz, zsiz, xpivot, ypivot, zpivot;
   long xoffset[xsiz+1];
   short xyoffset[xsiz][ysiz+1];
   char rawslabdata[?];

The file can be loaded like this:
   if ((fil = open("?.kvx",O_BINARY|O_RDWR,S_IREAD)) == -1) return(0);
   nummipmaplevels = 1;  //nummipmaplevels = 5 for unstripped KVX files
   for(i=0;i<nummipmaplevels;i++)
   {
      read(fil,&numbytes,4);
      read(fil,&xsiz,4);
      read(fil,&ysiz,4);
      read(fil,&zsiz,4);
      read(fil,&xpivot,4);
      read(fil,&ypivot,4);
      read(fil,&zpivot,4);
      read(fil,xoffset,(xsiz+1)*4);
      read(fil,xyoffset,xsiz*(ysiz+1)*2);
      read(fil,voxdata,numbytes-24-(xsiz+1)*4-xsiz*(ysiz+1)*2);
   }
   read(fil,palette,768);

numbytes: Total # of bytes (not including numbytes) in each mip-map level

xsiz, ysiz, zsiz: Dimensions of voxel. (zsiz is height)

xpivot, ypivot, zpivot: Centroid of voxel.  For extra precision, this
   location has been shifted up by 8 bits.

xoffset, xyoffset: For compression purposes, I store the column pointers
   in a way that offers quick access to the data, but with slightly more
   overhead in calculating the positions.  See example of usage in voxdata.
   NOTE: xoffset[0] = (xsiz+1)*4 + xsiz*(ysiz+1)*2 (ALWAYS)

voxdata: stored in sequential format.  Here's how you can get pointers to
   the start and end of any (x, y) column:

      //pointer to start of slabs on column (x, y):
   startptr = &voxdata[xoffset[x] + xyoffset[x][y]];

      //pointer to end of slabs on column (x, y):
   endptr = &voxdata[xoffset[x] + xyoffset[x][y+1]];

   Note: endptr is actually the first piece of data in the next column

   Once you get these pointers, you can run through all of the "slabs" in
   the column.  Each slab has 3 bytes of header, then an array of colors.
   Here's the format:

   char slabztop;             //Starting z coordinate of top of slab
   char slabzleng;            //# of bytes in the color array - slab height
   char slabbackfacecullinfo; //Low 6 bits tell which of 6 faces are exposed
   char col[slabzleng];       //The array of colors from top to bottom

palette:
   The last 768 bytes of the KVX file is a standard 256-color VGA palette.
   The palette is in (Red:0, Green:1, Blue:2) order and intensities range
   from 0-63.

   Note: To keep this ZIP size small, I have stripped out the lower mip-map
   levels.  KVX files from Shadow Warrior or Blood include this data.  To
   get the palette data, I recommend seeking 768 bytes before the end of the
   KVX file.
----------------------------------------------------------------------------
KV6 file format:

   //C pseudocode for loader:

   typedef struct { long col; unsigned short z; char vis, dir; } kv6voxtype;
   long xsiz, ysiz, zsiz;
   float xpiv, ypiv, zpiv;
   unsigned long xlen[xsiz];
   unsigned short ylen[xsiz][ysiz];
   long numvoxs;

   FILE *fil = fopen("?.KV6",rb");

   fread(&fileid,4,1,fil); //'Kvxl' (= 0x6c78764b in Little Endian)

       //Voxel grid dimensions
   fread(&xsiz,4,1,fil); fread(&ysiz,4,1,fil); fread(&zsiz,4,1,fil);

      //Pivot point. Floating point format. Voxel units.
   fread(&xpiv,4,1,fil); fread(&ypiv,4,1,fil); fread(&zpiv,4,1,fil);

   fread(&numvoxs,4,1,fil); //Total number of surface voxels
   for(i=0;i<numvoxs;i++) //8 bytes per surface voxel, Z's must be sorted
   {
      red  [i]    = fgetc(fil); //Range: 0..255
      green[i]    = fgetc(fil); //"
      blue [i]    = fgetc(fil); //"
      dummy       = fgetc(fil); //Always 128. Ignore.
      height_low  = fgetc(fil); //Z coordinate of this surface voxel
      height_high = fgetc(fil); //"
      visibility  = fgetc(fil); //Low 6 bits say if neighbor is solid or air
      normalindex = fgetc(fil); //Uses 256-entry lookup table
   }

      //Number of surface voxels present in plane x (extra information)
   for(x=0;x<xsiz;x++) fread(&xlen[x],4,1,fil);

      //Number of surface voxels present in column (x,y)
   for(x=0;x<xsiz;x++) for(y=0;y<ysiz;y++) fread(&ylen[x][y],2,1,fil);

      //Added 06/30/2007: suggested palette (optional)
   fread(&suggpalid,4,1,fil); //'SPal' (= 0x6C615053 in Little Endian)
   fread(suggestedpalette,768,1,fil); //R,G,B,R,G,.. Value range: 0-63

   fclose(fil);

----------------------------------------------------------------------------

Update history:

05/27/1999: SLAB6D.TXT started!
01/25/2000: Added EDITING CONTROLS to documentation
01/30/2000: Fixed really stupid bug relating to VESA modes. It should no
            longer crash upon entering the program.
05/01/2000: Added support for the loading of VOX files.
06/26/2000: Re-worded some documentation in this file.
06/30/2001: Updated save menu documentation & fixed 2 typos in KVX format
07/05/2001: Fixed a few recently introduced bugs... sorry about that!
07/07/2001: Added a facility for converting palettes and my KJS logo ;)
01/10/2002: Added the 2D slice editor, some new controls, and released the
               first Windows/DirectX version (SLAB6DW.EXE).
03/15/2002: Added 3D box selection for dragging, ALT+R, ALT+F, selectable
               radius&speed for HOME/END, toggle mouse Y inversion, and some
               helpful messages.
08/16/2002: Updated cursor so it's visible with white background.
08/18/2002: Added ALT+H function to help reduce file sizes slightly.
01/28/2003: Added support for loading KV6 (as well as saving). Also fixed
               recently introduced crash bug with voxel spray key (Home).
01/31/2003: Added palette editor: Modify RGB and linear interpolation.
02/09/2003: Added gamma value for (KP+/-) for palette interpolation.
03/11/2003: Renamed SLAB6DW->SLAB6. VOX/KVX with bad palette format no
               longer crash SLAB6(D) when attempting to load them.
09/13/2003: Fixed bug with pasting bitmap from Windows clipboard.
12/25/2003: Improved key repeat in SLAB6; added savekvx option for mip-maps.
            With key repeat working, I decided there wasn't any advantage to
               SLAB6D any more, so I removed it from the distribution.
            Renamed SLAB6D.TXT to SLAB6.TXT to save extra typing&confusion.
08/02/2004: Added scale&offset adjustment to lighting using KP1,KP3,KP7,KP9.
05/18/2006: Released SLAB6 source code.
07/01/2007: Added menus. Reorganized controls, such as ALT+.. -> SHIFT+..
            Now store suggested palette in KV6 files, leaving no reason to
               avoid the format - other than file size I guess.
            KV6 is now the default save format.
07/08/2007: Fixed some bugs and changed some keys. Some of the changes:
               * KP. is now T (face shade toggle)
               * Dragging 2D windows is now done with the left mouse button.
               * Right mouse button is now equivalent to Tab (grab color).
07/13/2008: Added optimize and double dimesions to tools menu.
07/14/2008: Fixed bug with doubling dimensions. Models doubled w/yesterday's
               version will be unoptimized. Run 'hollow fill' to fix.
07/15/2008: Fixed keyboard repeat rate when fps exceeds 1000.
07/19/2008: Added halve dimensions to tools menu. The replace palette tool
               now supports loading a suggested palette from a KV6 file.
03/22/2010: Mouse handling now works under Windows 7. Invert mouse y now
               defaults to unchecked.

----------------------------------------------------------------------------
Ken's official website: http://advsys.net/ken
