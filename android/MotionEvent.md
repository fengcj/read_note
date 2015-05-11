## MotionEvent

### Definition
`class MotionEvent extends InputEvent implements Paracelable`

### Class Overview

>>>Object used to report movement (mouse, pen, finger, trackball) events. Motion events may hold either absolute or relative movements and other data, depending on the type of device.

>>>Some devices can report multiple movement traces at the same time. Multi-touch screens emit one movement trace for each finger. **The individual fingers or other objects that generate movement traces are referred to as pointers.** Motion events contain information about all of the pointers that are currently active even if some of them have not moved since the last event was delivered.

### Id and Index
You keep track of individual pointers within a MotionEvent via each pointer's index and ID:

>>>Index: A MotionEvent effectively stores information about each pointer in an array. The index of a pointer is its position within this array. Most of the MotionEvent methods you use to interact with pointers take the pointer index as a parameter, not the pointer ID.

>>>> ID: Each pointer also has an ID mapping that stays persistent across touch events to allow tracking an individual pointer across the entire gesture.

Index will be change, but Id not.

### Pointer
![](https://github.com/fengcj/read_note/tree/master/android/MotionEvent_Pointer.png)


### getActionMasked() and getAction()

>>>Unlike the older getAction() method, getActionMasked() is designed to work with multiple pointers. It returns the masked action being performed, without including the pointer index bits.

This means `getActionMasked()` will return like `ACTION_DOWN`

more info can be get form:

- http://stackoverflow.com/questions/17384983/android-what-is-the-difference-between-getaction-and-getactionmasked-in-moti
- https://developer.android.com/training/gestures/multi.html