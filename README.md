# vedmapnew
import UIKit
import MapKit

class ViewController: UIViewController {

    @IBOutlet weak var mapView: MKMapView!
    
    var no = 0
  
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        //ottawa latitude and longitude
        //45.4215 N ,-75.6972 W
        let latitude: CLLocationDegrees = 45.4215
        let longitude: CLLocationDegrees = -75.6972
               
        display(latitude: latitude,
                longitude: longitude,
                title: "My Location",
                subtitle: "my place")
        doubleTap()
        
    }
    
       func display(latitude:CLLocationDegrees,
                    longitude:CLLocationDegrees,
                    title:String,
                    subtitle:String)
       {
           let latDelta: CLLocationDegrees = 0.10
           let longDelta: CLLocationDegrees = 0.10
           let span = MKCoordinateSpan(latitudeDelta: latDelta, longitudeDelta: longDelta)
           let location = CLLocationCoordinate2D(latitude: latitude, longitude: longitude)
           let region = MKCoordinateRegion(center: location, span: span)
           
    
           mapView.setRegion(region, animated: true)
           let annotation = MKPointAnnotation()
           annotation.title = title
           annotation.subtitle = subtitle
           annotation.coordinate = location
           mapView.addAnnotation(annotation)
       }

    func doubleTap()
        {
            let tapping = UITapGestureRecognizer(target: self, action:
                                                    #selector(Pin))
            tapping.numberOfTapsRequired = 3
            mapView.addGestureRecognizer(tapping)
        }
// tap three times to drop pin
        @objc func Pin(sender: UITapGestureRecognizer){
            
            let cities = ["A","B","C","D"]
            
                if(no < 3){
                    let touchPoint = sender.location(in: mapView)
                    let coordinate = mapView.convert(touchPoint, toCoordinateFrom: mapView)
                    //print(coordinate)
                   
                    let annotation = MKPointAnnotation()
                    annotation.title = cities[no]
                    no += 1
                    annotation.coordinate = coordinate
                    mapView.addAnnotation(annotation)

                }
                else{}
        }
}


