# android-market-api
An open-source API for the Android Market

This is not an official api. I'm not afiliated to google in any way.

This library allow you to ask directly google's official android market servers for information, search for apps, ...

Main target is java but it can be easily adapted to other languages since it's Google ProtoBuf based.

There is a Ruby port by jberkel here and a PHP port by splitfeed here. These is also a crawler on top of this library by Raunak Gupta here.

For any help using this API please use the google group HERE, no direct help request please, i won't answer.
Requirement

No specific requirement, it use java.net.URL for communication with the google market server, that's all. So it should run without problem on Google App Engine or in an Android app. Include androidmarketapi-X.Y.jar and protobuf-java-X.Y.Z.jar in your classpath and you're good to go.
Current progress

    You can browse market with any carrier or locale you want.
    Search for apps using keywords or package name.
    Retrieve an app info using an app ID.
    Retrieve comments using an app ID.
    Get PNG screenshots and icon 

Version History

    Version 0.6 : Fix corrupted session when exception occur. Change default android id and default sdk version
    Version 0.5 : Fix random 400 errors, fields recentChanges and promotionalVideo added
    Version 0.4 : Better error handling at login, default to android 2.2 (passion:8)
    Version 0.3 : GetImage api added, now searching for android 2.0 apps 

About authentication

A google account is required. You can use the login method with a valid login/password pair or provide an authsub token for service "android".

See Auth for installed apps for more info about authsub. You can also get a valid authsub token from an android device using the unofficial google clientlogin api for android (client.jar), see details here.
Basic Command-line usage

put the 2 jars in a folder and type : java -jar androidmarketapi-X.Y.jar myemail mypassword myquery
Basic Java Example

    MarketSession session = new MarketSession();
    session.login(email,password);
    session.getContext.setAndroidId(myAndroidId);
    
    String query = "maps";
    AppsRequest appsRequest = AppsRequest.newBuilder()
                                    .setQuery(query)
                                    .setStartIndex(0).setEntriesCount(10)
                                    .setWithExtendedInfo(true)
                                    .build();
                           
    session.append(appsRequest, new Callback<AppsResponse>() {
             @Override
             public void onResult(ResponseContext context, AppsResponse response) {
                      // Your code here
                      // response.getApp(0).getCreator() ...
                      // see AppsResponse class definition for more infos
             }
    });
    session.flush();
    
Check out how to :

  -  HowToSearchApps
  -  HowToGetAppComments
  -  HowToGetAppScreenshot 
