# ZMK Config Optimized for Sofle Keyboards

This is a zmk config that uses a [zmk fork that is optimized for the sofle keyboard](https://github.com/infused-kim/zmk/tree/sofle). It improves encoder, display and underglow support of zmk.

While it's been optimized for and tested with a sofle choc keyboard, it can be benificial for and should work with any split keyboard that is using encoders and displays.

## It adds the following features and fixes:

* Adds underglow (used for backlight) support to Sofle shield ([PR #1188](https://github.com/zmkfirmware/zmk/pull/1188))
* Fixes split side encoder not working ([PR #728](https://github.com/zmkfirmware/zmk/pull/728))
* Fixes display not working if you toggle external power off and then on again ([Issue #674](https://github.com/zmkfirmware/zmk/issues/674))
* Adds automatic disabling and enabling of external power when USB is disconnected or connected ([PR #1184](https://github.com/zmkfirmware/zmk/pull/1184))
* Adds automatic disabling of backlight if the keyboard is idle ([PR #1179](https://github.com/zmkfirmware/zmk/pull/1179))

Most of these fixes and features have not made it into the official zmk yet, because they don't meet the (very resaonable and completely understandable) code standards of the zmk maintainers.

However, while these fixes and features may not meet the quality standards of the official project, they work well enough to be used until these features get properly implemented in the official zmk.

# XCMKB users
## How to use through github's built in editor
1. Fork this repo
2. Edit keymap in Sofle-zmk/config/sofle.keymap 
3. Commit changes
4. Go to `Actions`, click `Build`, `Run workflow`.
5. Download the firmware from the `Actions` tab.

## First time bluetooth connection
![sofle connection](https://user-images.githubusercontent.com/79617315/229802255-4f432314-0723-4f06-a501-366b27930b86.jpg)

## Common Issues and Troubleshooting
1. [Mac or Window OS connected but not responding](https://zmk.dev/docs/features/bluetooth#macos-connected-but-not-working), this is working for Bluetooth 5.2 Windows.
2. Master connected and can type, but not slave refer to [Split Keyboard Halves Unable to Pair](https://zmk.dev/docs/troubleshooting#split-keyboard-halves-unable-to-pair).
3. You may compile the reset.uf2 yourself or get it from [setting reset.uf2](https://drive.google.com/file/d/1r3C8MBEVbgs5SK3Hc2CyoOIaiAPLB_zp/view?usp=drive_link).


## Example of keycodes for ZMK remap
The default firmware does not support mousekeys. However, the encoders on both sides are working as written and prepared by author snstein. For additional features, please refer to the ZMK website. If you have any questions, you can ask in their Discord server. The following are some basic and essential keycodes:


### Single tap
Always remember their prefix `&kp` or `&trans` or `to` etc. Refer to [Keyboard Codes of ZMK](https://zmk.dev/docs/codes).

### Hold
The most basic `&lt 5 Z` means hold to access layer 5, tap as z; while `&mt LSHIFT TAB` means hold as modifier Left Shift, tap as Tab.


### Macro
You can copy the following and edit according to your needs. Just need to note that for Left Shift+X it is `&macro_press &kp LSHFT &macro_tap &kp X &macro_release &kp LSHFT`; while single key tap for example c8 is `&macro_tap &kp C &kp N8`. In key remap, use `&gmail` to register macro.

```
/ {
    macros {
		gmail: gmail {
        compatible = "zmk,behavior-macro";
        label = "ZM_gmail";
        #binding-cells = <0>;
        wait-ms = <10>;
        tap-ms = <10>;
        bindings = <&macro_tap &kp X &kp C &kp H &kp C &kp L &kp O &kp W &kp AT_SIGN &kp G &kp M &kp A &kp I &kp L &kp PERIOD &kp C &kp O &kp M>;
        };

    };
};
```

## Flashing u2f to split
1. Connect left and right splits to your pc (both connect together using type c cable)
2. Put right into bootloader mode (press the reset button), one window is popped out showing "nicenano" folder. Dont do anything yet, remember this folder as right split. 
3. Now press reset button on your left split, one window will be popped out as previous step.
4. Drag left and right u2f to respective folders.
5. Do not disconnect right split yet. 
6. Remove left split from type c cable. Proceed to `First time bluetooth connection` to connect your board to pc. If successfully connected, you shall able to type without cable now. 
8. If so, remove the right split from type c cable. Both should be working good now!

:star: If you like our service or products, please tell your friends and family about us so we can grow and offer more options in the future. We strive to provide comprehensive user manuals to save you time exploring our products. We welcome any suggestions you have to help us improve our boards.



