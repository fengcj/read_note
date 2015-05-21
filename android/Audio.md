## AudioManager
>>> AudioManager provides access to volume and ringer mode control. Using `Context.getSystemService(Context.AUDIO_SERVICE)` to get an instance of this class

#### Methods of AudioManager

		// load sound effect
        public void loadSoundEffects()
        
        // effectType can be AudioManager.FX_KEY_CLICK and so on
        public void playSoundEffect(int effectType)

        // Request audio focus. Send a request to obtain the audio focus
        // steamType can be AudioManager.STREAM_MUSIC ...
        // durationHint can be AudioManager.AUDIOFOCUS_GAIN_TRANSIENT ...
        public void requestAudioFocus(AudioManager.onAudioFocusChangeListener I, int streamType,int durationHint)
        
        // Sets the speakerphone on or off
        public void setSpeakerphoneOn(boolean on)
        
        // UnLoad sound effect
        public void unloadSoundEffects()
        
#### Interface of AudioManager

		//Interface definiation for a callback to be invoked when the audio focus of the system is updated
        Interface AudioManager.OnAudioFocusChangeListener{
        	
            void onAudioFocusChange(int focusChange);
        
        }

## SoundPool
>>> The SoundPool class manages and plays audio resources for applications.
A SoundPool is a collection of samples that can be loaded into memory from a resource inside the APK or from a file in the file system.

#### Methods of SoundPool
        
        // Load the sound from the specified APK resource, return a sound ID
        public int load(Context context,int resId,int priority)
        
        // Set the callback hook for the OnLoadCompleteListener
        public void setOnLoadCompleteListener(SoundPool.OnLoadCompleteListener listener)
        
        // Unload a sound from a sound ID
        public final boolean unLoad(int soundId)
        
        // Release the SoundPool resource. Release all memory and native resources used by the SoundPool object
        public final boolean release()
        

## RingtoneManager

>Ringtone provides a quick method for **playing** a ringtone, notification, or other similar types of sounds.
>RingtoneManager provides **access** to ringtones, notification, and other types of sounds.

#### Method of RingtoneManager

		// Return the Uri for the default ringtone of a particular type,
        public static Uri getDefaultUri(int type)

        // Return a Ringtone for a given sound URI
        public static Ringtone getRingtone(Context context,Uri ringtoneUri)
        
        // example
        Uri notification_ringtone_uri = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFACATION);
        Ringtone notification_ringtone = RingtoneManager.getRingtone(getApplicationContext(),notifaction_ringtone_uri);
        notification_ringtone.play();


## Reference

- http://developer.android.com/reference/android/media/SoundPool.html
- http://developer.android.com/reference/android/media/AudioManager.html
- http://stackoverflow.com/questions/6577646/what-is-audio-focus-in-android-class-audiomanager