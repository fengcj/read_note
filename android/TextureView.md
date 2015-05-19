## TextureView
this class is extends `android.view.View`. TextureView in android is used to dispaly video, OpenGL scense, lived feed from camera device etc.


>>>In order to use TextureView, all you need to do is get its `SurfaceTexture`.The SurfaceTexture can then be used to render content. In order to do this, you just need to do instantiate an object of this class and implement `SurfaceTextureListener` interface.
    
    public class MyActivity extend Activity implements SurfaceTextureListener{
        private TextureView myTexture;
        private Camera mCamera;
        @Override
        protected void onCreate(Bundle savedInstanceState){
            super.OnCreate(saveInstanceState);
            myTexture = new TextureView(this);
            myTexture.setSurfaceTextureListener(this);
            setContentView(myTexture);
        }
    }
    
    