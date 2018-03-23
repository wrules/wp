---
title: GMap InfoWindow
position: 1
parameters:
  - name:
    content:
content_markdown: |-
  Goolge maps style infoWindow (https://github.com/googlemaps/v3-utility-library) infobox.
  
left_code_blocks:
  - code_block: |-
        google.maps.event.addDomListener(window, 'load', init);
        function init() {
            var mapOptions = {
                zoom: 15,
                mapTypeControl: false,
                zoomControl: false,
                streetViewControl: false,
                fullscreenControl:false,
                center: new google.maps.LatLng(40.665460, -73.810414)
            };
            var mapElement = document.getElementById("googleMapLocations");
            var map = new google.maps.Map(mapElement, mapOptions);
            
            var pin_1 = new google.maps.Marker({
                position: new google.maps.LatLng(40.665460, -73.810414),
                map: map,
                icon: '/wp-content/themes/terminal/assets/img/star.png'
            });
            var pinLoc_1 = new google.maps.LatLng(40.665460, -73.810414);
            var pinContent_1 = '' +
                '<div>' +
                    '<img src="/wp-content/themes/terminal/assets/img/locations-img.jpg" width="150" height="75">' +
                    '<address style="padding: 20px 20px 0 20px">' +
                    '<span>Fast Fleet Systems</span>' +
                    '<span>130-24 South Conduit Ave Jamaica, N.Y. 11430</span>' +
                    '</address>' +
                '</div>';
            var pinOption_1 = {
                content: pinContent_1,
                boxStyle: {
                    background: "white",
                    textAlign: "center",
                    fontSize: "8pt",
                    width: "150px",
                    boxShadow: "5px 5px 15px rgba(0,0,0,0.2)",
                    fontWeight: "600"
                },
                disableAutoPan: true,
                pixelOffset: new google.maps.Size(-185, -100),
                position: pinLoc_1,
                closeBoxURL: "",
                isHidden: false,
                enableEventPropagation: true
            };
            var pinAction_1 = new InfoBox(pinOption_1);
            pin_1.addListener('mouseover', function() {
                pinAction_1.open(map);
                $("#loc1").addClass("active");
            });
            pin_1.addListener('mouseout', function() {
                pinAction_1.close(map);
                $("#loc1").removeClass("active");
            });
            $("#loc1").hover(
                function() {
                    pinAction_1.open(map);
                },
                function() {
                    pinAction_1.close(map);
                }
            );
        }   
    title: JS 
    language: javascript
---