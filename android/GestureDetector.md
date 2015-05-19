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
    


## GestureOverlayView
 - this class extends from `android.widget.FrameLayout`
 - it is a **transparent overlay** for gesture input that can be palced on top of other widgets or contains other widgets
 - if you want use this, you need implement `OnGesturePerformedListener` to override `onGesturePerformed(GestureOverlayView overlay,Gesture gesture)` method
 - at the same time, you need use gesture library to load the gesture(R.raw.gesture) file which defined by your self by using "GestureBuilder"
 
### code example
    
     public class YourClass extends Activity implements OnGesturePerformedListener {

        private GestureLibrary mLibrary;
        mLibrary = GestureLibraries.fromRawResource(this, R.raw.gestures);
        if (!mLibrary.load()) {
            finish();
        }
        GestureOverlayView gestures =    (GestureOverlayView)findViewById(R.id.gestures);
        gestures.addOnGesturePerformedListener(this);

        public void onGesturePerformed(GestureOverlayView overlay, Gesture gesture) {
            ArrayList<Prediction> predictions = mLibrary.recognize(gesture);
            Log.v("performed","performed");
            // We want at least one prediction
            if (predictions.size() > 0) {
                Prediction prediction = predictions.get(0);
                // We want at least some confidence in the result
                if (prediction.score > 1.0) {
                    if(prediction.name.equalsIgnorecase("right")){
                      //do you thing here//
                      }
        }

## Reference
- http://www.tutorialspoint.com/android/android_gestures.htm
- http://stackoverflow.com/questions/5434258/using-a-gesture-overlay-view-in-android
- http://www.vogella.com/tutorials/AndroidGestures/article.html
- http://stackoverflow.com/questions/15038335/how-to-add-our-own-gestures-in-android