To change the name you go into the strings.xml file and edit the area next to "app name".
```
<resources>
    <string name="app_name">This is fine</string>
    <string name="action_external_web">External Web Page</string>
    <string name="action_internal_web">Internal Web Page</string>
</resources>
```

First of all for a webview to open a page we need access to the internet which is not a given permission by default. Therefore we need to navigate to the AndroidManifest.xml file and add that permission which is done by the line of code below.
```
 <uses-permission android:name="android.permission.INTERNET" />
```
To create a webview I went to the content_main.xml file and added the following code.
```
<WebView
        android:id="@+id/my_webview"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginStart="1dp"
        android:layout_marginLeft="1dp"
        android:layout_marginTop="1dp"
        android:layout_marginEnd="1dp"
        android:layout_marginRight="1dp"
        android:layout_marginBottom="1dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.0" />
 ```
 Now the first step is to create the variable for the webview which I do by..
```
private WebView myWebView;
```
that line of code. Then I use myWebView in the onCreate function to configure some of the elements for things to work out as shown below.
```
        myWebView = (WebView) findViewById(R.id.my_webview);

        myWebView.setWebViewClient(new WebViewClient());
        //setContentView(myWebView);

        myWebView.loadUrl("https://his.se");
        
        WebSettings webSettings = myWebView.getSettings();
        webSettings.setJavaScriptEnabled(true);
```
The loadUrl is used to just instantly open a webpage when this page is running.
Below is the code for depending on which button you click on you open either the internal or external webpage.
```
    public void showExternalWebPage(){
        // TODO: Add your code for showing external web page here
        myWebView.loadUrl("https://google.com/");
    }

    public void showInternalWebPage(){
        // TODO: Add your code for showing internal web page here
        myWebView.loadUrl("file:///android_asset/about.html");
    }
```
When opening the internal webpage the code below is executed to show a picture.
```
<h1>Hello There</h1>
<p>We test page here</p>
<p><img src="https://i.redd.it/g1ot0484k6821.png?auto=compress&amp;cs=tinysrgb&amp;dpr=2&amp;h=350&amp;w=540" alt="" width="400" height="400"/></p>
```
The code for the toolbar that provides the options and checks whether a button is pressed looks like the following.
```
@Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_external_web) {
            showExternalWebPage();
            return true;
        }

        if (id == R.id.action_internal_web) {
            showInternalWebPage();
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
```
The view for both internal and external looks like.
![Screenshot_1629399778](https://user-images.githubusercontent.com/62877630/130135332-40a81e43-d27d-42ef-aef5-6e9b826978d4.png)
![Screenshot_1627234929](https://user-images.githubusercontent.com/62877630/130135377-f4d12314-f7e6-4102-a2c2-fb9eb9602fd8.png)
