#Android Camera Preferences
The provided examples incorporate a user-adjustable camera preferences screen. There are two key preferences implemented- Firstly, on devices with more than one camera, the choice of camera, and secondly, the camera resolution.

This preferences screen is provided as part of the ARBaseLib library in the ARToolKit for Android distribution. The class identifier is org.artoolkit.ar.base.camera.CameraPreferencesActivity. It is quite straightforward to incorporate this class into your ARToolKit application.

There are two approaches, depending on whether your application's AR activity inherits from org.artoolkit.ar.base.ARActivity, or whether it uses its own Activity and CameraSurface classes.

## Applications Inheriting from ARActivity
The example applications which inherit from ARActivity are:

-  ARSimple
-  ARSimpleInteraction
-  ARSimpleNative
-  ARSimpleNativeCars

If your application falls into this category, you need add only the essential lines of code to register the CameraPreferencesActivity in your manifest. The behavior of providing the settings menu in response to the menu button is automatically provided by the ARActivity class. The preferences chosen by the user are automatically used in the CameraPreview class.

Just add the following to your AndroidManifest.xml file:
<pre>
    <activity android:name="org.artoolkit.ar.base.camera.CameraPreferencesActivity"></activity>
</pre>

## Applications using Custom Activity Subclasses
The example applications which use their own Activity and CameraSurface classes are:

- ARNative
- ARNativeOSG
- nftSimple
- nftBook
- ARMovie

If your application is based on one of these applications, a handful of changes need to be made to initialize the preferences the first time the application is run after being freshly installed, to invoke the preferences activity, and to use the actual preferences in setting up the camera.

###Initialize Preference Defaults
Add the following code where it will be run once per install of Application, and prior to using any of the camera preferences. If you are subclassing `Application.onCreate()` (as all the examples do), put it into `Application.onCreate()`. If not subclassing Application, put it in your `Activity.onCreate()` method.
<pre>
    import android.preference.PreferenceManager;
    PreferenceManager.setDefaultValues(this, org.artoolkit.ar.base.R.xml.preferences, false);
</pre>

###Invoke Preferences Activity
The suggested method of invoking the preferences activity is to make it available via your applications settings menu. This is quite straightforward. Add the following code to your Activity subclass:
<pre>
    import org.artoolkit.ar.base.camera.CameraPreferencesActivity;
    import android.view.Menu;
    import android.view.MenuInflater;
    import android.view.MenuItem;
    
    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.options, menu);
        return true;
    }
    
    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        if (item.getItemId() == R.id.settings) {
            startActivity(new Intent(this, CameraPreferencesActivity.class));
            return true;
        } else {
            return super.onOptionsItemSelected(item);
        }
    }
</pre>

This will use the menu resource provided by the ARBaseLib library. If you already have an options menu, you will most likely want to incorporate the existing values from ARBaseLib's res/menu/options.xml.

###Using Preferences
Once the user has actually chosen the preferences, you need to make sure you're actually using the choices, or that you're using the default values if no choice has yet been made. This code will typically be in a class which inherits from Surface and which implements CameraPreviewCallback. Take a look at the CameraSurface class in the native examples for example usage.

Code to open the correct camera chosen by the user:
<pre>
    import android.os.Build;
    import android.preference.PreferenceManager;
    Camera camera = null;
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.GINGERBREAD) camera = Camera.open(Integer.parseInt(PreferenceManager.getDefaultSharedPreferences(callingContext).getString("pref_cameraIndex", "0")));
    else camera = Camera.open();
</pre>

Code to attempt to configure the camera resolution:
<pre>
    String camResolution = PreferenceManager.getDefaultSharedPreferences(callingContext).getString("pref_cameraResolution", getResources().getString(R.string.pref_defaultValue_cameraResolution));
    String[] dims = camResolution.split("x", 2);
    Camera.Parameters parameters = camera.getParameters();
    parameters.setPreviewSize(Integer.parseInt(dims[0]),Integer.parseInt(dims[1]));
    camera.setParameters(parameters);
</pre>

Don't forget that the chosen resolution may not be accepted by the camera, so don't assume that the camera preview buffers will be the preferred size. You should read back the actual size in use after setting the preferred value (e.g. when sizing buffers).

##Customizing
The full source of CameraPreferencesActivity is provided and is easy to customize. The source refers to a number of resources, found at the following paths:

- ARBaseLib/res/drawable-hdpi/settings.png
- ARBaseLib/res/drawable-mdpi/settings.png
- ARBaseLib/res/drawable-xhdpi/settings.png
- ARBaseLib/res/menu/options.xml
- ARBaseLib/res/values/strings.xml
- ARBaseLib/xml/preferences.xml

These resources are automatically available in any project referring to ARBaseLib. If you wish to customize these, you can override in your Activity by using the same resource ID with the new value.

##A Note on Camera Resolutions
Take care when the user chooses camera resolutions. A camera resolution with a different aspect ratio to the aspect ratio of ARToolKit's [calibrated camera parameters][config_camera_calibration] (camera_para.dat or similar) will not track correctly!

[config_camera_calibration]: 2_Configuration:config_camera_calibration
