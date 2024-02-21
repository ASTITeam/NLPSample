
# NLP Location Provider
Network Location Provider can use in POS device and smart android device sdk .


## Sopports Android 7 - 14 (Nougat-to-UPSIDE_DOWN_CAKE):
**Systems app tracking cases:**
**Network Location Provider is provided for you to:**
1. Will read data from cellular GNSS information  from App
2. and will calculate and parse  location information ,
3. view and analyze carrier phase (if it is present in the log file).

## Install the library
    implementation ("com.github.ASTITeam:nlplib:1.0.0"){ transitive = true }

Or if the library is to be used only for debug builds and not release builds, then

    debugImplementation ("com.github.ASTITeam:nlplib:1.0.0"){ transitive = true }

Add repository maven url, If required to find repositories version:

    repositories 
    {
        google()
        maven {
           url "https://github.com/ASTITeam/nlplib/tree/main/releases/com/github/ASTITeam/nlplib"
        }
    }

## Initialize start and stop location latlng's

**Start POS Location Service to capture Location using LocationListener:**

      POSLocationBuilder poslocationBuilder = new POSLocationBuilder(getContext(), CLIENT_TOKEN, new CustomLocationListener() {
            @Override
            public void onLocationChanged(CustomLocation customLoc) {
                printLog("loc","provider: "+location.getProvider()
                        +"latlng: "+location.getLatitude() +","+location.getLongitude()
                        +" accuracy: "+location.getAccuracy() +" time: "+location.getTime(),Color.WHITE);
            }
        });
    //interval in min's min 2 minutes
    poslocationBuilder.setIntervalTimeInMins(2);
    poslocationBuilder.startLocationCapture();

**Stop location capturing:**
    poslocationBuilder.stopLocationCapture();

Last Recorded Location: (Required to start POSLocationProviderService service
to get last Recorded location)

    POSLocationBuilder.getLocation(getContext())

For Sample Location fragment initialization:

      LoggerFragment editProfileFragment = LoggerFragment.getInstance("CLIENT_TOKEN");
            fragmentManger.beginTransaction()
                    .replace(R.id.logger_fragment, editProfileFragment)
                    .addToBackStack(null)
                    .commit();