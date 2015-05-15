## GestureDetector

>>>Android provides special types of touch screen events such as pinch , double tap, scrolls , long presses and flinch. These are all known as gestures.

>>>Android provides `GestureDetector` class to receive `motion events` and tell us that these events correspond to gestures or not. To use it , you need to **create an object of GestureDetector** and then extend another class with `GestureDetector.SimpleOnGestureListener` to act as a listener and override some methods. Its syntax is given below:

    GestureDetector myG;
    myG = new GestureDetector(this,new Gesture());
    Class Gesture extends GestureDetector.SimpleOnGestureDetector{
        @override
        public boolean onDoubleTap(MotionEvent e){
            // code
        }
        // GestureDetector.SimpleGestureDetector has 9 methods
    }
    public boolean onTouch(MotionEvent ev){
        // when we double Tap the screen,this method will be call,and pass event the myG
        // then the method onDoubleTap will be call
        myG.onTouchEvent(ev);
        return true;
    }
    
    
    


## Reference
- http://www.tutorialspoint.com/android/android_gestures.htm