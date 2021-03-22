# lab01- sumador 
laboratorio 01 introducción a HDL

Alejandra Rojas Huertas

La simulación del sumador de 4 bits corrió de manera exitosa, al simularla de manera "manual", es decir, forzando algunas de las entradas y haciendo la cuenta de manera manual. Como también corrió bien al simularla con el Testbench. 

Para comprobar el correcto funcionamiento del programa se verifica la suma del número binario 0111 y 0011, efectivamente se tiene que el resultado es 1010 con acarreo 0.

A continuación, se explica de manera detallada el código con el que se crea el Testbench para el sumador de 4 bits:

`timescale 1ns / 1ps

module sum4b_TB;

  // Inputs    //se crean los registros de entrada A y B que tendrán un tamaño de 4 bits
  reg [3:0] A;
  reg [3:0] B;

  // Outputs // se definen a S como un vector de 4 bits y representa la salida del sumador. co es el acarreo
  wire co;
  wire [3:0] S;

  // Instantiate the Unit Under Test (UUT) //Al programa sum4bcc se le asigna las variables antes instanciadas 
  sum4bcc uut (
    .xi(A), 
    .yi(B), 
    .co(co), 
    .zi(S)
  );

  
  initial begin
  

  // Initialize Inputs
    A=0; 
	 for (B = 0; B < 16; B = B + 1) begin //ciclo que hace recorrer b desde 0 hasta 15, aumentando de uno en uno.
      if (B==0)
        A=A+1; //si B=0, A tomará el valor que tenía antes más 1, así ambas entradas A y B iterarán al tiempo.
      #2 ;
		$display("El valor de %d + %d = %d",A, B,S) ; //como se mostrará la salida en la consola
    end
	
  end      

  initial begin: TEST_CASE
     $dumpfile("sum4b_TB.vcd");
     $dumpvars(-1, uut);
     #(200) $finish; // tiempo que tardará un ciclo en pico segundos
   end


endmodule

NOTA: se adjunta a este repositorio una carpeta llamada archivos_quartus, en donde se guardaron los programas 
del sumador de 4 bits y el testbench para el mismo sumador.