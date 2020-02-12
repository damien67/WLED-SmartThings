metadata {
	definition (name: "WLED", namespace: "Damien", author: "Damien") {
		capability "Switch"
		capability "Switch Level"
		capability "Light"
		capability "Color Control"
		
        command "on"
		command "off"
        command "setColor"
		command "setLevel"

		attribute "color", "String"
		attribute "level", "Number"

	}

	simulator {

	}
	
	tiles (scale: 2) { 
    // void controlTile(String tileName, String attributeName, String controlType [, Map options, Closure closure])
            standardTile("switch", "device.switch", width: 3, height: 2, canChangeIcon: true) {
            state "on", label:'${name}', action:"off", icon:"st.switches.light.on", backgroundColor:"#00a0dc"
            state "off", label:'${name}', action:"on", icon:"st.switches.light.off", backgroundColor:"#ffffff"
		}
		//BRIGHTNESS
     		controlTile("level", "level", "slider",  width: 3, height: 2, inactiveLabel: false,range:"(0..255)" ) {
			state "level", action:"setLevel", label: "Level"
		}
        
		//COLOR
		 controlTile("rgbSelector", "color", "color", width: 6, height: 6, inactiveLabel: false) {
         state "color", action:"setColor"
        }
		
		main "switch"
		details([
		"switch","levelLabel", "level","rgbSelector" 
         
        ])
	}
	
	preferences {
        input name: "internal_ip", type: "text", title: "Internal IP", required: true
		input name: "internal_port", type: "text", title: "Internal Port", defaultValue: 80, required: true   	      
	}
}

/*
=============================================
ON/OFF
=============================================
*/
def off() {
	sendEvent(name: "switch", value: "off", isStateChange: true)
    //log.debug("Turn OFF")
	
    return sendGetRequest("/win&T=0")
} 
def on() {
    sendEvent(name: "switch", value: "on", isStateChange: true)
	//log.debug("Turn ON, Color:${state.SavedColor}, Brightness: ${state.SavedLevel}, Color2: ${state.SavedColor2}")
	
    return sendGetRequest("/win&T=1&FX=0" )
}

/*
=============================================
BRIGHTNESS LEVEL
=============================================
*/
def setLevel(Integer value,rate=0) {
    state.SavedLevel = value
    
    sendEvent(name: "switch", value: "on", isStateChange: true)
    sendEvent(name: "level", value: state.SavedLevel, isStateChange: true)
    
	//log.debug("Turn ON, Color:${state.SavedColor}, Brightness: ${state.SavedLevel}, Color2: ${state.SavedColor2}")
	
    return sendGetRequest("/win&A=${value}")
}

/*
=============================================
COLOR
=============================================
*/ 

def setColor(value) {

	state.SavedColor = value
    
    //log.debug("Turn ON, Color:${state.SavedColor}, Brightness: ${state.SavedLevel}, Color2: ${state.SavedColor2}")
	//sendEvent(name: "switch", value: "on", isStateChange: true)
    
    //log.debug("Set Color:${value}")
	def h = (value.hue)*65535/100
    def s = (value.saturation)*255/100
    
    return sendGetRequest("/win&HU=${h}&SA=${s}")
    
}

/*
=============================================
HTTP SEND
=============================================
*/ 

private sendGetRequest(String url) {
	log.debug("${internal_ip}:${internal_port}${url}")
    
    def result = new physicalgraph.device.HubAction(
        method: "GET",
		path: "${url}",
        headers: [
            HOST: "${internal_ip}:${internal_port}" 
			]
        )
    //return result;
}
