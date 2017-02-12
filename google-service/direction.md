direction.java
```java
package komis.me.utils;

import com.google.android.gms.maps.model.LatLng;

/**
 * Created by Kazaf on 2015/9/21.
 */
public class Direction {

    private Routes[] routes;
    private String error_message;

    private class Routes {
        private OverView overview_polyline;
        private Bounds bounds;
        private String copyrights;

        private class Bounds {
            private NorthEast northeast;
            private SouthWest southwest;

            private class NorthEast {

                private String lat;
                private String lng;

            }

            private class SouthWest {

                private String lat;
                private String lng;

            }
        }

        private class OverView {
            private String points;
        }
    }

    public String getPoints() {

        // only got first result so we get first result
        return routes[0].overview_polyline.points;
    }

    public LatLng getMidPoint(){

        Double N = Double.parseDouble(routes[0].bounds.northeast.lat);
        Double E = Double.parseDouble(routes[0].bounds.northeast.lng);
        Double S = Double.parseDouble(routes[0].bounds.southwest.lat);
        Double W = Double.parseDouble(routes[0].bounds.southwest.lng);

        LatLng midPoint = new LatLng((N+S)/2,(E+W)/2);

        return midPoint;
    }

    public String printErrorMessage(){
        return error_message;
    }
}




```


```java
  StringBuilder builder = new StringBuilder()
                .append("https://maps.googleapis.com/maps/api/directions/json?avoid=highways&origin=")
                .append(bundle.getString(Constants.key.LATITUDE))
                .append(",")
                .append(bundle.getString(Constants.key.LONGITUDE))
                .append("&destination=")
                .append(bundle.getString(Constants.key.LATITUDE_DES))
                .append(",")
                .append(bundle.getString(Constants.key.LONGITUDE_DES));
                ```
