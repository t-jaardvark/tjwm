
# my dwm-flexipatch config 

## Keybindings
SUPER+x             rofi drun launcher
SUPER+CTRL+SHIFT+Q	quit
SUPER+CTRL+LEFT 	shiftview -1
SUPER+CTRL+RIGHT 	shiftview +1
SUPER+{1,2,3..0}	view tag number
SUPER+W             firefox

## restartsig patch
## dwm patches
patches.h
```
#define BAR_DWMBLOCKS_PATCH 1
#define BAR_DWMBLOCKS_SIGUSR1_PATCH 1
#define BAR_HEIGHT_PATCH 1
#define BAR_PANGO_PATCH 1
#define BAR_STATUSCMD_PATCH 1
#define AUTOSTART_PATCH 1
#define FAKEFULLSCREEN_PATCH 1
#define FULLSCREEN_PATCH 1
#define PLACEMOUSE_PATCH 1
#define RESTARTSIG_PATCH 1
#define RENAMED_SCRATCHPADS_PATCH 1
#define RENAMED_SCRATCHPADS_AUTO_HIDE_PATCH 1
#define SHIFTVIEW_PATCH 1
```

## increase border px size
change in config.h
``` after
static const unsigned int borderpx       = 3;   /* border pixel of windows */
```

## set expllicit bar height 
change in config.h
``` after
#if BAR_HEIGHT_PATCH
static const int bar_height              = 24;   /* 0 means derive from font, >= 1 explicit height */
#endif // BAR_HEIGHT_PATCH
```


## support unicode
change in config.h
``` after
#if BAR_PANGO_PATCH
static const char font[] = "Victor Mono Nerd Font Mono 10";
#else
static const char *fonts[]               = { "VictorMono Nerd Font Mono-Medium:size=10" };
#endif // BAR_PANGO_PATCH
static const char dmenufont[]            = "VictorMono Nerd Font Mono-Medium:size=10";
```

change in config.h
```
static char titleselfgcolor[]            = "#FFFFFF";
static char titleselbgcolor[]            = "#323232";
```

## add window rules
add to config .h
- around `static const Rule rules[] = {`
```
	RULE(.class = "Signal", .tags = 1 << 1)
	RULE(.class = "obsidian", .tags = 1 << 2)
	RULE(.class = "Cursor", .tags = 1 << 3)
	RULE(.class = "Nemo", .tags = 1 << 4)
```

remove from config.h around `RULE(.class = "Nemo", .tags = 1 << 4)`
```
    RULE(.class = "Gimp", .tags = 1 << 4)
```

## change modkey to super
change in config.h
``` before
#define MODKEY Mod1Mask
```
``` after
#define MODKEY Mod4Mask
```

change in config.h (make kitty as default terminal)
```
static const char *termcmd[]  = { "kitty", NULL };
```


change in config.h
```
	#if SHIFTVIEW_PATCH
	{ MODKEY|ControlMask,             XK_Left,   shiftview,              { .i = -1 } },
	{ MODKEY|ControlMask,             XK_Right,  shiftview,              { .i = +1 } },
	#endif // SHIFTVIEW_PATCH
```

change in config.h
```
	#if SHIFTVIEW_PATCH
	{ MODKEY|ControlMask,             XK_Left,   shiftview,              { .i = -1 } },
	{ MODKEY|ControlMask,             XK_Right,  shiftview,              { .i = +1 } },
	#endif // SHIFTVIEW_PATCH
```

# add mouse wheel up/down functionality
```
	#if BAR_STATUSCMD_PATCH && BAR_DWMBLOCKS_PATCH
	{ ClkStatusText,        0,                   Button1,        sigstatusbar,   {.i = 1 } },
	{ ClkStatusText,        0,                   Button2,        sigstatusbar,   {.i = 2 } },
	{ ClkStatusText,        0,                   Button3,        sigstatusbar,   {.i = 3 } },
	{ ClkStatusText,        0,                   Button4,        sigstatusbar,   {.i = 4 } },
	{ ClkStatusText,        0,                   Button5,        sigstatusbar,   {.i = 5 } },	
    #endif // BAR_STATUSCMD_PATCH && BAR_DWMBLOCKS_PATCH
```

## install libpango1.0-dev (linux mint)
```
sudo apt install libpango1.0-dev
```

## fix pango comile error
change in config.mk
``` 
# Uncomment for the pango patch / BAR_PANGO_PATCH
PANGOINC = `pkg-config --cflags xft pango pangoxft`
PANGOLIB = `pkg-config --libs xft pango pangoxft`
```


