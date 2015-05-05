## TransitionDrawable

>>> 
An extension of LayerDrawables that is intended to **cross-fade between the first and second layer**. To start the transition, call startTransition(int). To display just the first layer, call resetTransition().It can be defined in an XML file with the <transition> element. Each Drawable in the transition is defined in a nested <item>. For more information, see the guide to Drawable Resources.

#### XML File for TransitionDrawable
        <?xml version="1.0" encoding="UTF-8"?>
            <transition xmlns:android="http://schemas.android.com/apk/res/android">
             <!-- The drawables used here can be solid colors, gradients, shapes, images, etc. -->
            <item android:drawable="@drawable/new_state" />
             <item android:drawable="@drawable/original_state" />
            </transition>
            
#### Code for TransitionDrawable

        RelativeLayout layout = (RelativeLayout) findViewById(R.id.Layout);
        layout.setBackgroundResource(R.drawable.translate);
        TransitionDrawable transition = (TransitionDrawable) layout.getBackground();
        transition.startTransition(5000);
        


## AnimationDrawable

>>> An object used to create **frame-by-frame animations**, defined by a series of Drawable objects, which can be used as a View object's background.The simplest way to create a frame-by-frame animation is to define the animation in an XML file, placed in the res/drawable/ folder, and set it as the background to a View object. Then, call start() to run the animation.

>>> An AnimationDrawable defined in XML consists of a single <animation-list> element, and a series of nested <item> tags. Each item defines a frame of the animation.

#### XML File for AnimationDrawable
        
        <!-- this file named spin_animation.xml -->
        <!-- Animation frames are wheel0.png -- wheel5.png files inside the
    res/drawable/ folder -->
        <animation-list android:id="@+id/selected" android:oneshot="false">
            <item android:drawable="@drawable/wheel0" android:duration="50" />
            <item android:drawable="@drawable/wheel1" android:duration="50" />
            <item android:drawable="@drawable/wheel2" android:duration="50" />
            <item android:drawable="@drawable/wheel3" android:duration="50" />
            <item android:drawable="@drawable/wheel4" android:duration="50" />
            <item android:drawable="@drawable/wheel5" android:duration="50" />
        </animation-list>


#### Code for AnimationDrawable

         // Load the ImageView that will host the animation and
        // set its background to our AnimationDrawable XML resource.
        ImageView img = (ImageView)findViewById(R.id.spinning_wheel_image);
        img.setBackgroundResource(R.drawable.spin_animation);

        // Get the background, which has been compiled to an AnimationDrawable object.
        AnimationDrawable frameAnimation = (AnimationDrawable) img.getBackground();

        // Start the animation (looped playback by default).
        frameAnimation.start();

















