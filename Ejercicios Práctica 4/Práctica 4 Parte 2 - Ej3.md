<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%204/Pr%C3%A1ctica%204%20P2,%20ejercicio%203.jpg?raw=true" alt="Diagrama ejercicio 3, práctica 4, parte 2" width="900" height="900">
</p>

```
{ 

3. Una empresa de transporte de caudales desea optimizar el servicio que brinda a sus clientes. Para ello,
cuenta con información sobre todos los viajes realizados durante el mes de marzo. De cada viaje se cuenta
con la siguiente información: día del mes (de 1 a 31), monto de dinero transportado y distancia recorrida por
el camión (medida en kilómetros).

}

program Hello;

const
    dimF = 200;

type
    marzo = 1 .. 31;

    viaje = record
        dia: marzo;
        monto: integer;
        distancia: integer;
    end;

    arregloViajes = array [1 .. dimF] of viaje;

    arregloDia = array [marzo] of integer;

{c. Realizar un módulo que reciba el vector generado en a) 
y elimine todos los viajes cuya distancia
recorrida sea igual a 100 km.}
procedure eliminarViajes (var vi: arregloViajes; var dimL: integer);
    var
        i: integer;
        j: integer;
    
    begin
        j := 1;

        for i := 1 to dimL do begin
            if (vi[i].distancia <> 100) then begin
                vi[j] := vi[i];
                j := j + 1;
                
            end;
        end;
        dimL := j - 1;
    end;


{b. Realizar un módulo que reciba el vector generado en a) e informe:
- El monto promedio transportado de los viajes realizados
- La distancia recorrida y el día del mes en que se realizó el viaje que transportó menos dinero.
- La cantidad de viajes realizados cada día del mes.}
procedure inicializarArregloDia (var ad: arregloDia);
    var
        i: integer;

    begin
        for i := 1 to 31 do begin
            ad[i] := 0;
        end;
    end;

procedure informarAlgo (vi: arregloViajes; dimL: integer);
    var
        i: integer;
        montoTotViaj: integer;
        montoMin: integer;
        distanciaMin: integer;
        diaMin: integer;
        ad: arregloDia;

    begin
        montoTotViaj := 0;
        montoMin := 9999;
        distanciaMin := 0;
        diaMin := 0;

        inicializarArregloDia (ad);

        for i := 1 to dimL do begin
            montoTotViaj := vi[i].monto + montoTotViaj;

            if (vi[i].monto < montoMin) then begin
                montoMin := vi[i].monto;
                distanciaMin := vi[i].distancia;
                diaMin := vi[i].dia;
            end;

            ad[vi[i].dia] := ad[vi[i].dia] + 1;
            
        end;

        writeln ('El monto promedio transportado de los viajes realizados es: ', (montoTotViaj/dimL)0:2);
        writeln ('El monto $', montoMin, ' es el menor y fue transportado el día ', diaMin, ' por una distancia igual a: ', distanciaMin);
        for i := 1 to 31 do begin
            writeln ('El día ', i, ' del mes, se realizaron', ad[i], ' viajes');
        end;
    end;

//a. Realizar un programa que lea y almacene la información de los viajes (a lo sumo 200). La lectura finaliza
// cuando se ingresa una distancia recorrida igual a 0 km, que no debe procesarse.
procedure cargarViajes (var vi: arregloViajes; var dimL: integer);
    var
        v: viajes;

    begin
        writeln ('Ingresar la distancia recorrida: ');
        readln (v.distancia);
        while (v.distancia <> 0) and (dimL <= dimF) do begin
            writeln ('Ingresar el día en que se realiza el viaje: ');
            readln (v.dia);
            writeln ('Ingresar el monto de dinero transportado: ');
            readln (v.monto);
            dimL := dimL + 1;
            vi[dimL] := v;
        end;
    end;

var
    vi: arregloViajes;
    dimL: integer;

begin
    dimL := 0;

    cargarViajes (vi, dimL);
    informarAlgo (vi, dimL);
    eliminarViajes (vi, dimL);
end.
