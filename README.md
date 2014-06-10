#touchpadMacbookDebianConfig
===========================

##Configuration script for macbook4,1 synaptics touchpad on Debian Wheezy

See Options on manual below for more information.

===========================

From http://www.x.org/archive/X11R7.5/doc/man/man4/synaptics.4.html:

===========================

###Table of Contents

1.Name
2.Synopsis
3.Description
4.Configuration Details
5.Device Properties
6.Notes
7.Removed Options
8.Authors
9.See Also

===========================

###Name

synaptics - Synaptics touchpad input driver

===========================

###Synopsis


Section "InputDevice"
  Identifier "devname"
  Driver "synaptics"
  Option "Device"   "devpath"
  Option "Path"     "path"
  ...
EndSection


===========================

###Description

Synaptics is an Xorg input driver for the touchpads from Synaptics Incorporated. Even though these touchpads (by default, operating in a compatibility mode emulating a standard mouse) can be handled by the normal evdev or mouse drivers, this driver allows more advanced features of the touchpad to become available. Some benefits would be:
Movement with adjustable, non-linear acceleration and speed.
Button events through short touching of the touchpad.
Double-Button events through double short touching of the touchpad.
Dragging through short touching and holding down the finger on the touchpad (tap-and-drag gesture).
Middle and right button events on the upper and lower corner of the touchpad.
Vertical scrolling (button four and five events) through moving the finger on the right side of the touchpad.
The up/down button sends button four/five events.
Horizontal scrolling (button six and seven events) through moving the finger on the lower side of the touchpad.
The multi-buttons send button four/five events for vertical scrolling and button six/seven events for horizontal scrolling.
Adjustable finger detection.
Multifinger taps: two finger for middle button and three finger for right button events. (Needs hardware support. Not all models implement this feature.)
Pressure dependent motion speed.
Run-time configuration using shared memory. This means you can change parameter settings without restarting the X server.
Note that depending on the touchpad firmware, some of these features might be available even without using the synaptics driver. Note also that some functions are not available on all touchpad models, because they need support from the touchpad hardware/firmware. (Multifinger taps for example.)

===========================

###Configuration Details

Please refer to xorg.conf(5) for general configuration details and for options that can be used with all input drivers.This section only covers configuration details specific to this driver.
The following driver Options are supported:

**Option** "Device" "string"
This option specifies the device file in your "/dev" directory which will be used to access the physical device. Normally you should use something like "/dev/input/eventX", where X is some integer.

**Option** "Protocol" "string"
Specifies which kernel driver will be used by this driver. This is the list of supported drivers and their default use scenarios.
auto-dev	automatic, default (recommend)
event	Linux 2.6 kernel events
psaux	raw device access (Linux 2.4)
psm	FreeBSD psm driver

**Option** "SHMConfig" "boolean"
Switch on/off shared memory for run-time configuration. Note that this is considered a security risk since any user can access the configuration. This option is not needed with synaptics 1.0 or later. See section Device Properties.

**Option** "LeftEdge" "integer"
X coordinate for left edge. Property: "Synaptics Edges"

**Option** "RightEdge" "integer"
X coordinate for right edge. Property: "Synaptics Edges"

**Option** "TopEdge" "integer"
Y coordinate for top edge. Property: "Synaptics Edges"

**Option** "BottomEdge" "integer"
Y coordinate for bottom edge. Property: "Synaptics Edges"

**Option** "FingerLow" "integer"
When finger pressure drops below this value, the driver counts it as a release. Property: "Synaptics Finger"

**Option** "FingerHigh" "integer"
When finger pressure goes above this value, the driver counts it as a touch. Property: "Synaptics Finger"

**Option** "FingerPress" "integer"
When finger pressure goes above this value, the driver counts it as a press. Currently a press is equivalent to putting the touchpad in trackstick emulation mode. Property: "Synaptics Finger"

**Option** "MaxTapTime" "integer"
Maximum time (in milliseconds) for detecting a tap. Property: "Synaptics Tap Durations"

**Option** "MaxTapMove" "integer"
Maximum movement of the finger for detecting a tap. Property: "Synaptics Tap Move"

**Option** "MaxDoubleTapTime" "integer"
Maximum time (in milliseconds) for detecting a double tap. Property: "Synaptics Tap Durations"

**Option** "ClickTime" "integer"
The duration of the mouse click generated by tapping. Property: "Synaptics Tap Durations"

**Option** "FastTaps" "boolean"
Makes the driver react faster to a single tap, but also makes double clicks caused by double tapping slower. Property: "Synaptics Tap FastTap"

**Option** "VertEdgeScroll" "boolean"
Enable vertical scrolling when dragging along the right edge. Property: "Synaptics Edge Scrolling"

**Option** "HorizEdgeScroll" "boolean"
Enable horizontal scrolling when dragging along the bottom edge. Property: "Synaptics Edge Scrolling"

**Option** "CornerCoasting" "boolean"
Enable edge scrolling to continue while the finger stays in an edge corner. Property: "Synaptics Edge Scrolling"

**Option** "VertTwoFingerScroll" "boolean"
Enable vertical scrolling when dragging with two fingers anywhere on the touchpad. Property: "Synaptics Two-Finger Scrolling"

**Option** "HorizTwoFingerScroll" "boolean"
Enable horizontal scrolling when dragging with two fingers anywhere on the touchpad. Property: "Synaptics Two-Finger Scrolling"

**Option** "VertScrollDelta" "integer"
Move distance of the finger for a scroll event. Property: "Synaptics Scrolling Distance"

**Option** "HorizScrollDelta" "integer"
Move distance of the finger for a scroll event. Property: "Synaptics Scrolling Distance"

**Option** "EdgeMotionMinZ" "integer"
Finger pressure at which minimum edge motion speed is set. Property: "Synaptics Edge Motion Pressure"

**Option** "EdgeMotionMaxZ" "integer"
Finger pressure at which maximum edge motion speed is set. Property: "Synaptics Edge Motion Pressure"

**Option** "EdgeMotionMinSpeed" "integer"
Slowest setting for edge motion speed. Property: "Synaptics Edge Motion Speed"

**Option** "EdgeMotionMaxSpeed" "integer"
Fastest setting for edge motion speed. Property: "Synaptics Edge Motion Speed"

**Option** "EdgeMotionUseAlways" "boolean"
If on, edge motion is also used for normal movements. If off, egde motion is used only when dragging. Property: "Synaptics Edge Motion Always"

**Option** "MinSpeed" "float"
Minimum speed factor. Property: "Synaptics Move Speed"

**Option** "MaxSpeed" "float"
Maximum speed factor. Property: "Synaptics Move Speed"

**Option** "AccelFactor" "float"
Acceleration factor for normal pointer movements. Property: "Synaptics Move Speed"

**Option** "TrackstickSpeed" "float"
Speed scale when in trackstick emulation mode. Property: "Synaptics Move Speed"

**Option** "PressureMotionMinZ" "integer"
Finger pressure at which minimum pressure motion factor is applied. Property: "Synaptics Pressure Motion"

**Option** "PressureMotionMaxZ" "integer"
Finger pressure at which maximum pressure motion factor is applied. Property: "Synaptics Pressure Motion"

**Option** "PressureMotionMinFactor" "integer"
Lowest setting for pressure motion factor. Property: "Synaptics Pressure Motion Factor"

**Option** "PressureMotionMaxFactor" "integer"
Greatest setting for pressure motion factor. Property: "Synaptics Pressure Motion Factor"

**Option** "UpDownScrolling" "boolean"
If on, the up/down buttons generate button 4/5 events. If off, the up button generates a double click and the down button generates a button 2 event. Property: "Synaptics Button Scrolling"

**Option** "LeftRightScrolling" "boolean"
If on, the left/right buttons generate button 6/7 events. If off, the left/right buttons both generate button 2 events. Property: "Synaptics Button Scrolling"

**Option** "UpDownScrollRepeat" "boolean"
If on, and the up/down buttons are used for scrolling (UpDownScrolling), these buttons will send auto-repeating 4/5 events, with the delay between repeats determined by ScrollButtonRepeat. Property: "Synaptics Button Scrolling Repeat"

**Option** "LeftRightScrollRepeat" "boolean"
If on, and the left/right buttons are used for scrolling (LeftRightScrolling), these buttons will send auto-repeating 6/7 events, with the delay between repeats determined by ScrollButtonRepeat. Property: "Synaptics Button Scrolling Repeat"

**Option** "ScrollButtonRepeat" "integer"
The number of milliseconds between repeats of button events 4-7 from the up/down/left/right scroll buttons. Property: "Synaptics Button Scrolling Time"

**Option** "EmulateMidButtonTime" "integer"
Maximum time (in milliseconds) for middle button emulation. Property: "Synaptics Middle Button Timeout"

**Option** "EmulateTwoFingerMinZ" "integer"
For touchpads not capable of detecting multiple fingers (Alps), this sets the Z pressure threshold to emulate a two finger press. Property: "Synaptics Two-Finger Pressure"

**Option** "EmulateTwoFingerMinW" "integer"
Some touchpads report a two-finger touch as wide finger. This sets the finger width threshold to emulate a two finger press. This feature works best with (PalmDetect) off. Property: "Synaptics Two-Finger Width"

**Option** "TouchpadOff" "integer"
Switch off the touchpad. Valid values are:
0	Touchpad is enabled
1	Touchpad is switched off
2	Only tapping and scrolling is switched off
Property: "Synaptics Off"

**Option** "GuestMouseOff" "boolean"
Switch on/off guest mouse (often a stick). Property: "Synaptics Guestmouse Off"

**Option** "LockedDrags" "boolean"
If off, a tap-and-drag gesture ends when you release the finger. If on, the gesture is active until you tap a second time, or until LockedDragTimeout expires. Property: "Synaptics Locked Drags"

**Option** "LockedDragTimeout" "integer"
This parameter specifies how long it takes (in milliseconds) for the LockedDrags mode to be automatically turned off after the finger is released from the touchpad. Property: "Synaptics Locked Drags Timeout"

**Option** "RTCornerButton" "integer"
Which mouse button is reported on a right top corner tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "RBCornerButton" "integer"
Which mouse button is reported on a right bottom corner tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "LTCornerButton" "integer"
Which mouse button is reported on a left top corner tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "LBCornerButton" "integer"
Which mouse button is reported on a left bottom corner tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "TapButton1" "integer"
Which mouse button is reported on a non-corner one-finger tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "TapButton2" "integer"
Which mouse button is reported on a non-corner two-finger tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "TapButton3" "integer"
Which mouse button is reported on a non-corner three-finger tap. Set to 0 to disable. Property: "Synaptics Tap Action"

**Option** "ClickFinger1" "integer"
Which mouse button is reported when left-clicking with one finger. Set to 0 to disable. Property: "Synaptics Click Action"

**Option** "ClickFinger2" "integer"
Which mouse button is reported when left-clicking with two fingers. Set to 0 to disable. Property: "Synaptics Click Action"

**Option** "ClickFinger3" "integer"
Which mouse button is reported when left-clicking with three fingers. Set to 0 to disable. Property: "Synaptics Click Action"

**Option** "CircularScrolling" "boolean"
If on, circular scrolling is used. Property: "Synaptics Circular Scrolling"

**Option** "CircScrollDelta" "float"
Move angle (radians) of finger to generate a scroll event. Property: "Synaptics Circular Scrolling Distance"

**Option** "CircScrollTrigger" "integer"
Trigger region on the touchpad to start circular scrolling
0	All Edges
1	Top Edge
2	Top Right Corner
3	Right Edge
4	Bottom Right Corner
5	Bottom Edge
6	Bottom Left Corner
7	Left Edge
8	Top Left Corner
Property: "Synaptics Circular Scrolling Trigger"

**Option** "CircularPad" "boolean"
Instead of being a rectangle, the edge is the ellipse enclosed by the Left/Right/Top/BottomEdge parameters. For circular touchpads. Property: "Synaptics Circular Pad"

**Option** "PalmDetect" "boolean"
If palm detection should be enabled. Note that this also requires hardware/firmware support from the touchpad. Property: "Synaptics Palm Detection"

**Option** "PalmMinWidth" "integer"
Minimum finger width at which touch is considered a palm. Property: "Synaptics Palm Dimensions"

**Option** "PalmMinZ" "integer"
Minimum finger pressure at which touch is considered a palm. Property: "Synaptics Palm Dimensions"

**Option** "CoastingSpeed" "float"
Coasting threshold scrolling speed. 0 disables coasting. Property: "Synaptics Coasting Speed"

**Option** "SingleTapTimeout" "integer"
Timeout after a tap to recognize it as a single tap. Property: "Synaptics Tap Durations"

**Option** "GrabEventDevice" "boolean"
If GrabEventDevice is true, the driver will grab the event device for exclusive use when using the linux 2.6 event protocol. When using other protocols, this option has no effect. Grabbing the event device means that no other user space or kernel space program sees the touchpad events. This is desirable if the X config file includes /dev/input/mice as an input device, but is undesirable if you want to monitor the device from user space. When changing this parameter with the synclient program, the change will not take effect until the synaptics driver is disabled and reenabled. This can be achieved by switching to a text console and then switching back to X.

**Option** "TapAndDragGesture" "boolean"
Switch on/off the tap-and-drag gesture. This gesture is an alternative way of dragging. It is performed by tapping (touching and releasing the finger), then touching again and moving the finger on the touchpad. The gesture is enabled by default and can be disabled by setting the TapAndDragGesture option to false. Property: "Synaptics Gestures"

**Option** "VertResolution" "integer"
Resolution of X coordinates in units/millimeter. The value is used together with HorizResolution to compensate unequal vertical and horizontal sensitivity. Setting VertResolution and HorizResolution equal values means no compensation. Default value is read from the touchpad or set to 1 if value could not be read. Property: "Synaptics Pad Resolution"

**Option** "HorizResolution" "integer"
Resolution of Y coordinates in units/millimeter. The value is used together with VertResolution to compensate unequal vertical and horizontal sensitivity. Setting VertResolution and HorizResolution equal values means no compensation. Default value is read from the touchpad or set to 1 if value could not be read. Property: "Synaptics Pad Resolution"
The LeftEdge, RightEdge, TopEdge and BottomEdge parameters are used to define the edge and corner areas of the touchpad. The parameters split the touchpad area in 9 pieces, like this:

   LeftEdge    RightEdge
           Physical top edge
1
4
7
Physical left edge
Coordinates to the left of LeftEdge are part of the left edge (areas 1, 4 and 7), coordinates to the left of LeftEdge and above TopEdge (area 1) are part of the upper left corner, etc. A good way to find appropriate edge parameters is to enable the SHMConfig option and run "synclient -m 1" to see the x/y coordinates corresponding to different positions on the touchpad.

**Option** "AreaLeftEdge" "integer"
Ignore movements, scrolling and tapping which take place left of this edge. The option is disabled by default and can be enabled by setting the AreaLeftEdge option to any integer value other than zero. Property: "Synaptics Area"

**Option** "AreaRightEdge" "integer"
Ignore movements, scrolling and tapping which take place right of this edge. The option is disabled by default and can be enabled by setting the AreaRightEdge option to any integer value other than zero. Property: "Synaptics Area"

**Option** "AreaTopEdge" "integer"
Ignore movements, scrolling and tapping which take place above this edge. The ption is disabled by default and can be enabled by setting the AreaTopEdge option to any integer value other than zero. Property: "Synaptics Area"

**Option** "AreaBottomEdge" "integer"
Ignore movements, scrolling and tapping which take place below this edge. The option is disabled by default and can be enabled by setting the AreaBottomEdge option to any integer value other than zero. Property: "Synaptics Area"


A tap event happens when the finger is touched and released in a time interval shorter than MaxTapTime, and the touch and release coordinates are less than MaxTapMove units apart. A "touch" event happens when the Z value goes above FingerHigh, and an "untouch" event happens when the Z value goes below FingerLow.

The MaxDoubleTapTime parameter has the same function as the MaxTapTime parameter, but for the second, third, etc tap in a tap sequence. If you can't perform double clicks fast enough (for example, xmms depends on fast double clicks), try reducing this parameter. If you can't get word selection to work in xterm (ie button down, button up, button down, move mouse), try increasing this parameter.

The ClickTime parameter controls the delay between the button down and button up X events generated in response to a tap event. A too long value can cause undesirable autorepeat in scroll bars and a too small value means that visual feedback from the gui application you are interacting with is harder to see. For this parameter to have any effect, "FastTaps" has to be disabled.

The MinSpeed, MaxSpeed and AccelFactor parameters control the pointer motion speed. The speed value defines the scaling between touchpad coordinates and screen coordinates. When moving the finger very slowly, the MinSpeed value is used, when moving very fast the MaxSpeed value is used. When moving the finger at moderate speed, you get a pointer motion speed somewhere between MinSpeed and MaxSpeed. If you don't want any acceleration, set MinSpeed and MaxSpeed to the same value.

The MinSpeed, MaxSpeed and AccelFactor parameters don't have any effect on scrolling speed. Scrolling speed is determined solely from the VertScrollDelta and HorizScrollDelta parameters. To disable vertical or horizontal scrolling, set VertScrollDelta or HorizScrollDelta to zero.

When hitting an egde, movement can be automatically continued. If EdgeMotionUseAlways is false, edge motion is only used when dragging. With EdgeMotionUseAlways set to true, it is also used for normal cursor movements.

Edge motion speed is calculated by taking into account the amount of pressure applied to the touchpad. The sensitivity can be adjusted using the EdgeMotion parameters. If the pressure is below EdgeMotionMinZ, EdgeMotionMinSpeed is used, and if the pressure is greater than EdgeMotionMaxZ, EdgeMotionMaxSpeed is used. For a pressure value between EdgeMotionMinZ and EdgeMotionMaxZ, the speed is increased linearly.

When pressure motion is activated, the cursor motion speed depends on the pressure exerted on the touchpad (the more pressure exerted on the touchpad, the faster the pointer). More precisely the speed is first calculated according to MinSpeed, MaxSpeed and AccelFactor, and then is multiplied by a sensitivity factor. The sensitivity factor can be adjusted using the PressureMotion parameters. If the pressure is below PressureMotionMinZ, PressureMotionMinFactor is used, and if the pressure is greater than PressureMotionMaxZ, PressureMotionMaxFactor is used. By default, PressureMotionMinZ and PressureMotionMaxZ are equal to EdgeMotionMinZ and EdgeMotionMaxZ. For a pressure value between PressureMotionMinZ and PressureMotionMaxZ, the factor is increased linearly.

Since most synaptics touchpad models don't have a button that corresponds to the middle button on a mouse, the driver can emulate middle mouse button events. If you press both the left and right mouse buttons at almost the same time (no more than EmulateMidButtonTime milliseconds apart) the driver generates a middle mouse button event.

Circular scrolling acts like a scrolling wheel on the touchpad. Scrolling is engaged when a drag starts in the given CircScrollTrigger region, which can be all edges, a particular side, or a particular corner. Once scrolling is engaged, moving your finger in clockwise circles around the center of the touchpad will generate scroll down events and counter clockwise motion will generate scroll up events. Lifting your finger will disengage circular scrolling. Use tight circles near the center of the pad for fast scrolling and large circles for better control. When used together with vertical scrolling, hitting the upper or lower right corner will seamlessly switch over from vertical to circular scrolling.

Coasting is enabled by setting the CoastingSpeed parameter to a non-zero value. Coasting comes in two flavors: conventional (finger off) coasting, and corner (finger on) coasting.

Conventional coasting is enabled when coasting is enabled, and CornerCoasting is set to false. When conventional coasting is enabled, horizontal/vertical scrolling can continue after the finger is released from the lower/right edge of the touchpad. The driver computes the scrolling speed corresponding to the finger speed immediately before the finger leaves the touchpad. If this scrolling speed is larger than the CoastingSpeed parameter (measured in scroll events per second), the scrolling will continue with the same speed in the same direction until the finger touches the touchpad again.

Corner coasting is enabled when coasting is enabled, and CornerCoasting is set to true. When corner coasting is enabled, edge scrolling can continue as long as the finger stays in a corner. Coasting begins when the finger enters the corner, and continues until the finger leaves the corner. CornerCoasting takes precedence over the seamless switch from edge scrolling to circular scrolling. That is, if CornerCoasting is active, scrolling will stop, and circular scrolling will not start, when the finger leaves the corner.

Trackstick emulation mode is entered when pressing the finger hard on the touchpad. The FingerPress parameter controls the minimum required finger pressure. If the finger hasn't moved more than MaxTapMove after MaxTapTime has elapsed, trackstick mode is entered. In this mode, moving the finger slightly in any direction gives a speed vector that moves the pointer. The TrackstickSpeed parameter controls the ratio between pointer speed and finger movement distance. Trackstick mode is exited when the finger pressure drops below FingerLow or when the finger is moved further than MaxTapMove away from the initial position.

===========================

###Device Properties

Synaptics 1.0 and higher support input device properties if the driver is running on X server 1.6 or higher. On these driver versions, **Option** "SHMConfig" is not needed to enable run-time configuration. The synclient tool shipped with synaptics version 1.1 uses input device properties by default. Properties supported:
Synaptics Edges
32 bit, 4 values, left, right, top, bottom.
Synaptics Finger
32 bit, 3 values, low, high, press.
Synaptics Tap Time
32 bit.
Synaptics Tap Move
32 bit.
Synaptics Tap Durations
32 bit, 3 values, single touch timeout, max tapping time for double taps, duration of a single click.
Synaptics Tap FastTap
8 bit (BOOL).
Synaptics Middle Button Timeout
32 bit.
Synaptics Two-Finger Pressure
32 bit.
Synaptics Two-Finger Width
32 bit.
Synaptics Scrolling Distance
32 bit, 2 values, vert, horiz.
Synaptics Edge Scrolling
8 bit (BOOL), 3 values, vertical, horizontal, corner.
Synaptics Two-Finger Scrolling
8 bit (BOOL), 2 values, vertical, horizontal.
Synaptics Move Speed
FLOAT, 4 values, min, max, accel, trackstick.
Synaptics Edge Motion Pressure
32 bit, 2 values, min, max.
Synaptics Edge Motion Speed
32 bit, 2 values, min, max.
Synaptics Edge Motion Always
8 bit (BOOL).
Synaptics Button Scrolling
8 bit (BOOL), 2 values, updown, leftright.
Synaptics Button Scrolling Repeat
8 bit (BOOL), 2 values, updown, leftright.
Synaptics Button Scrolling Time
32 bit.
Synaptics Off
8 bit, valid values (0, 1, 2).
Synaptics Guestmouse Off
8 bit (BOOL).
Synaptics Locked Drags
8 bit (BOOL).
Synaptics Locked Drags Timeout
32 bit.
Synaptics Tap Action
8 bit, up to MAX_TAP values (see synaptics.h), 0 disables an element. order: RT, RB, LT, LB, F1, F2, F3.
Synaptics Click Action
8 bit, up to MAX_CLICK values (see synaptics.h), 0 disables an element. order: Finger 1, 2, 3.
Synaptics Circular Scrolling
8 bit (BOOL).
Synaptics Circular Scrolling Distance
FLOAT.
Synaptics Circular Scrolling Trigger
8 bit, valid values 0..8 (inclusive) order: any edge, top, top + right, right, right + bottom, bottom, bottom + left, left, left + top.
Synaptics Circular Pad
8 bit (BOOL).
Synaptics Palm Detection
8 bit (BOOL).
Synaptics Palm Dimensions
32 bit, 2 values, width, z.
Synaptics Coasting Speed
FLOAT.
Synaptics Pressure Motion
32 bit, 2 values, min, max.
Synaptics Pressure Motion Factor
FLOAT, 2 values, min, max.
Synaptics Grab Event Device
8 bit (BOOL).
Synaptics Gestures
8 bit (BOOL), 1 value, tap-and-drag.
Synaptics Area
The AreaLeftEdge, AreaRightEdge, AreaTopEdge and AreaBottomEdge parameters are used to define the edges of the active area of the touchpad. All movements, scrolling and tapping which take place outside of this area will be ignored. This property is disabled by default.
32 bit, 4 values, left, right, top, bottom. 0 disables an element.

Synaptics Capabilities
This read-only property expresses the physical capability of the touchpad, most notably whether the touchpad hardware supports multi-finger tapping and scrolling.
8 bit (BOOL), 5 values (read-only), has left button, has middle button, has right button, two-finger detection, three-finger detection.

Synaptics Pad Resolution
32 bit unsigned, 2 values (read-only), vertical, horizontal in units/millimeter.

===========================

###Notes

There is an example hal policy file in ${sourcecode}/fdi/11-x11-synaptics.fdi which will enable the driver based on the information if the hardware is available. Feel free to copy it to /etc/hal/fdi/policy and customize it to your needs. You can pass custom options to the driver using x11_options properties. Note that this requires xorg-server-1.5 or higher.
If either of Protocol "auto-dev" (default) or Protocol "event" is used, the driver initializes defaults based on the capabilities reported by the kernel driver. Acceleration, edges and resolution are based on the dimensions reported by the kernel. If the kernel reports multi-finger detection, two-finger vertical scrolling is enabled, horizontal two-finger scrolling is disabled and edge scrolling is disabled. If no multi-finger capabilities are reported, edge scrolling is enabled for both horizontal and vertical scrolling. Tapping is disabled by default for touchpads with one or more physical buttons. To enable it you need to map tap actions to buttons. See the "TapButton1", "TapButton2" and "TapButton3" options.

Button mapping for physical buttons is handled in the server. If the device is switched to left-handed (an in-server mapping of physical buttons 1, 2, 3 to the logical buttons 3, 2, 1, respectively), both physical and TapButtons are affected. To counteract this, the TapButtons need to be set up in reverse order (TapButton1=3, TapButton2=1).

===========================

###Removed Options

The following options are no longer part of the driver configuration:
**Option** "Repeater" "string"
**Option** "HistorySize" "integer"
**Option** "SpecialScrollAreaRight" "boolean"

===========================

###Authors

Peter Osterlund <petero2@telia.com> and many others.

===========================

###See Also

Xorg(1) , xorg.conf(5) , Xserver(1) , X(7) , synclient(1) , syndaemon(1)

===========================

###Table of Contents

1.Name
2.Synopsis
3.Description
4.Configuration Details
5.Device Properties
6.Notes
7.Removed Options
8.Authors
9.See Also

