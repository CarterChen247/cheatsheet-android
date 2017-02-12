```java
        StringBuilder builder = new StringBuilder()
                .append("http://maps.googleapis.com/maps/api/geocode/json?language=zh-TW&latlng=")
                .append(bundle.getString(Constants.key.LATITUDE))
                .append(",")
                .append(bundle.getString(Constants.key.LONGITUDE));
                ```

Geocoding.java        
```java
package komis.me.utils;

/**
 * Created by Kazaf on 2015/10/1.
 * <p/>
 * ---Address_components---
 * 0 - street_number
 * 1 - route (Road)
 * 2 - administrative_area_level_4 (X)
 * 3 - administrative_area_level_3
 * 4 - administrative_area_level_2 (County)
 * 5 - country
 * 6 - postal_code
 */
public class Geocoding {

    private Results[] results;

    private class Results {

        private Address_components[] address_components;

        private class Address_components {
            private String long_name;
//            private String short_name;
//            private String[] types;
        }
    }

    public String getApproxRoad() {

        // declare parameters
        String letterRoad = "路";
        String route = results[0].address_components[1].long_name;
        int charIndex = 0;

        StringBuilder builder = new StringBuilder();

        while ((route.charAt(charIndex) != letterRoad.charAt(0))) {

            builder.append(route.charAt(charIndex));
            charIndex++;
        }

        builder.append(route.charAt(charIndex)).append("附近");
        return builder.toString();
    }

    public String getApproxZone() {
        StringBuilder builder = new StringBuilder();
        builder
                .append(results[0].address_components[3].long_name)
                .append(results[0].address_components[1].long_name)
                .append("附近");
        return builder.toString();
    }

}
```