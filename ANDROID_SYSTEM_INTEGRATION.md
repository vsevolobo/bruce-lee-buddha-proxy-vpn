# ANDROID_SYSTEM_INTEGRATION

## Connecting the VPN App to Android System using Native Android VPN Service

1. **Setup a VPNService subclass**  
   - Create a new class that extends `VpnService`.  
   - Override `onCreate()`, `onDestroy()`, and `onStartCommand()` methods as necessary.  
   
2. **Configure the VPN**  
   - Use `Builder` class to configure VPN properties.  
   - Set the necessary parameters such as server address, DNS servers, and routes:  
     ```java  
     Builder builder = new VpnService.Builder();  
     builder.addAddress("192.168.1.2", 24); // Add your VPN address  
     builder.addDnsServer("8.8.8.8");    // Google DNS  
     builder.addRoute("0.0.0.0", 0);       // Route all traffic  
     ```  
   - Call `establish()` method to create a VPN interface.

3. **Instantiate and Start the VPN Service**  
   - Start the VPN service by calling `startService()` with an appropriate intent.
   - Use `bindService()` if you need to interact with the service directly.

## System Settings Integration

1. **Declare Permissions**  
   - In your `AndroidManifest.xml`, declare the permission to use the VPN service:
     ```xml  
     <uses-permission android:name="android.permission.BIND_VPN_SERVICE" />
     ```  
   
2. **Show Connection Settings**  
   - Prompt the user to grant permission for the VPN connection. You can direct users to the settings via:  
     ```java  
     startActivity(new Intent(Settings.ACTION_VPN_SETTINGS));
     ```  
   
3. **User Notifications**  
   - Notify users when the VPN is connected or disconnected using the notification manager.  
   
## Routing All Traffic Through the VPN Proxy on Android 15 and Compatible Versions

1. **Using the VPN Interface**  
   - Ensure that the `addRoute()` method is used properly to redirect traffic through your VPN proxy. 
   
   ```java  
   builder.addRoute("0.0.0.0", 0);  // This will route all traffic
   ```  

2. **Testing the VPN Configuration**  
   - After establishing a connection, verify that all traffic is routed through the VPN proxy:
    - Use tools such as ping, traceroute, or web services to confirm public IP changes.

3. **Handle API changes in Android 15**  
   - Stay updated with Android documentation to handle any new changes or deprecations in VPN service APIs.

## Conclusion
Following these instructions will help you set up a VPN service that integrates with the Android system settings and routes all traffic as needed for Android 15 and below compatibility.

---