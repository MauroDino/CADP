![Diagrama ejercicio 5, práctica 3](URL_imagen)

```
{

Realizar un programa que lea información de autos que están a la venta en una concesionaria. De cada auto se
lee: marca, modelo y precio. La lectura finaliza cuando se ingresa la marca “ZZZ” que no debe procesarse. La
información se ingresa ordenada por marca. Se pide calcular e informar:
a. El precio promedio por marca.
b. Marca y modelo del auto más caro.

}

program Hello;

type
    auto = record
        marca: string;
        modelo: string;
        precio: integer;
    end;
    
procedure leerAuto (var a: auto);
    begin
        writeln ('Ingresar la marca del auto: ');
        readln (a.marca);
        if (a.marca <> 'ZZZ') then begin
            writeln ('Ingresar el modelo del auto: ');
            readln (a.modelo);
            writeln ('Ingresar el precio del auto: ');
            readln (a.precio);
        end;
    end;
    
var
    a: auto;
    precioTot: integer;
    contador: integer;
    marcaActual: string;
    precioMax: integer;
    marcaMax: string;
    modeloMax: string; 
    promedio: real;

begin
    
    precioMax := -999;
    marcaMax := ' ';
    modeloMax := ' ';
    
    leerAuto (a);
        
    while (a.marca <> 'ZZZ') do begin
        marcaActual := a.marca;
        contador := 0;
        precioTot := 0;
        
        while (a.marca <> 'ZZZ') and (a.marca = marcaActual) do begin
            contador := contador + 1;
            precioTot := a.precio + precioTot;
            
            if (a.precio > precioMax) then begin
                marcaMax := a.marca;
                modeloMax := a.modelo;
            end;
            leerAuto (a);
        end;
    promedio := precioTot / contador;
    writeln ('El precio promedio por marca es: ', promedio:0:2);
    end;
    
    writeln ('La marca y modelo del auto más caro es: ', marcaMax, modeloMax);
end.
