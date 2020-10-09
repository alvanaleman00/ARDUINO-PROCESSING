# ARDUINO-PROCESSING
import processing.serial.*;

//Se declara la variable 
boolean estadoBoton = false;
Serial miSerial;
//Color indicador para el encendido y apagado del led 
color colorApagado = color(200, 0, 0);
color colorEncendido = color(0, 200, 0);
float distancia;
float val;      // Data received from the serial port

//Tamaño de la venta para el boton de encendido 
void setup() {
  size(400, 600);
  
  // Se indica el puerto de salida al que esta conectada la placa
  String nombrePuerto = "COM5";
  miSerial = new Serial(this, nombrePuerto, 9600);
}

void draw() {
  if ( miSerial.available() > 0) {  // If data is available,
    val = miSerial.read();         // read it and store it in val
  }
  background(255);
  if (estadoBoton) {
    fill(colorEncendido);
  } else {
    fill(colorApagado);
  }
  ellipse(200,200,350,350);
}

//Enviar la señal al micro controlador
void mouseClicked() {
 println(mouseX,mouseY);
 distancia = dist(200,200,mouseX,mouseY);
 println(distancia);
 if (distancia<175){
     estadoBoton = !estadoBoton;
     miSerial.write('a');
   }
}
