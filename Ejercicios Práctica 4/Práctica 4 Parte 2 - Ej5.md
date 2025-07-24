<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%204/Pr%C3%A1ctica%204%20P2,%20ejercicio%205.jpg?raw=true" alt="Diagrama ejercicio 5, práctica 4, parte 2" width="900" height="900">
</p>

```
{ En el siguiente link, compartí el diagrama de flujo que hice para plantear brevemente la lógica del ejercicio y avanzar con el código:
https://github.com/MauroDino/Ejercicios-CADP/blob/Main/Practica4P2/Ejercicio5V2.md

5. La empresa Amazon Web Services (AWS) dispone de la información de sus 500 clientes monotributistas más
grandes del país. De cada cliente conoce la fecha de firma del contrato con AWS, la categoría del
monotributo (entre la A y la F), el código de la ciudad donde se encuentran las oficinas (entre 1 y 2400) y el
monto mensual acordado en el contrato. La información se ingresa ordenada por fecha de firma de contrato
(los más antiguos primero, los más recientes últimos).
Realizar un programa que lea y almacene la información de los clientes en una estructura de tipo vector. Una
vez almacenados los datos, procesar dicha estructura para obtener:
a. Cantidad de contratos por cada mes y cada año, y año en que se firmó la mayor cantidad de contratos
b. Cantidad de clientes para cada categoría de monotributo
c. Código de las 10 ciudades con mayor cantidad de clientes
d. Cantidad de clientes que superan mensualmente el monto promedio entre todos los clientes.
}

program Hello;

const
    dimF = 500;

type
    cod = 1 .. 2400;

    anioMes = 1 .. 12;

    monot = 'A' .. 'F';

    Fecha = record
        dia: 1..31;
        mes: 1..12;
        anio: integer;
    end;


    clientes = record
        fecha: Fecha;
        categoria: monot;
        codigo: cod;
        monto: real;
    end;

    vectorCiudades = array [1 .. 2400] of integer; // para llevar los 10 máximos del inciso c

    vectorClientes = array [1 .. dimF] of clientes;

    vectorMono = array [monot] of integer; // para llevar la cuenta de las categorías de monotributos

procedure codigo10Maximos (cClien: vectorClientes; vCiu: vectorCiudades);
    var
        max: integer;

    begin
        max := -1;

        if ()


    end;

procedure informarCategoria (vMono: vectorMono);
    var
        i: integer;

    begin
        for k := A to F do begin
            writeln ('La categoría ', k, ' tiene ', vMono[k], ' clientes.');
    end;

procedure actualizarMaximo (contrAnio: integer; anioActual: integer; var maximoContrato: integer; var anioMax: integer);
    begin
        if (contrAnio > maximoContrato) then begin
            maximoContrato := contrAnio;
            anioMax := anioActual;
        end;
    end;

procedure recorrerVector (cClien: vectorClientes; var vCiu: vectorCiudades; var vMono: vectorMono);
    var
        i: integer;
        anioActual: integer;
        contrAnio: integer;
        mesActual: integer;
        contrMes: integer;
        anioMax: integer;
        codMAx: integer;
        maximoContrato: integer;
        cantMontos: real;
        supera: integer;
        promedio: real;

    begin
        i := 1;
        anioMax := -1;
        maximoContrato := -1;
        cantMontos := 0;
        supera := 0;
        promedio := 0;

        while (i < dimF) do begin
            anioActual := cClien[i].fecha.anio;

            contrAnio := 0;
            while (cClien[i].fecha.anio = anioActual) do begin
                mesActual := cClien[i].fecha.mes;

                contrMes := 0;
                while (cClien[i].fecha.anio = anioActual) and (cClien[i].fecha.mes = mesActual) do begin
                    contrMes := contrMes + 1;
                    vMono[cClien[i].categoria] := vMono[cClien[i].categoria] + 1;
                    cantMontos := cantMontos + cClien[i].monto; 
                    vCiu[cClien[i].codigo] := vCiu[cClien[i].codigo] + 1; // Esta línea completa el vector contador de ciudades
                    
                    i := i + 1;
                end;
                contrAnio := contrAnio + contrMes;
                writeln ('La cantidad de contratos que tiene el mes ', mesActual, ' es: ', contrMes);

            end;
            writeln ('La cantidad de contratos que tiene el año ', anioActual, ' es: ', contrAnio);
            actualizarMaximo (contrAnio, anioActual, maximoContrato, anioMax); //contrAnio: lleva cantidad de contratos por año. anioActual: . anioMax: para informar el año. maximoContrato: para comparar y actualizar el máximo.
        end;

        writeln ('El año ', anioMax, ' es el que tiene mayor cantidad de contratos con ', maximoContrato, ' firmados.');
        informarCategorias (vMono);
        //Este lugar es para los 10 máximos
        promedio := cantMontos / dimF;
        
        for i := 1 to dimF do begin
            if (cClien[i].monto > promedio) then
                supera := supera + 1;
        end;
        writeln('La cantidad de clientes cuyo monto supera el promedio es: ', supera);
        codigo10Maximos (cClien, vCiu); // Acá se debe recorrer el vector de 1 a 2400 e informar los 10 máximos
    end;
        

procedure inicializarContadores (var vCiu: vectorCiudades; var vMono: vectorMono);
    var
        i: integer;
        j: char;

    begin
        for i := 1 to 2400 do begin
            vCiu[i] := 0;
        end;

        for j := A to F do begin
            vMono[j] := 0;
        end;
    end;

procedure leerCliente (var c: clientes);
    begin
        writeln ('Ingresar la fecha de la firma del contrato, separada en mes y año: ');
        writeln ('Mes: ');
        readln (c.fecha.mes);
        writeln ('Año: ');
        readln (c.fecha.anio);
        writeln ('Ingresar la categoría (entre A y F) de monotributo: ');
        readln (c.categoria);
        writeln ('Ingresar el código (entre 1 y 2400) de la ciudad de las oficinas: ');
        readln (c.codigo);
        writeln ('Ingresar el monto acordado en el contrato: ');
        readln (c.monto);
    end;

procedure cargarVectorClientes (var cClien: vectorClientes);
    var
        c: clientes;
        i: integer;

    begin
        i := 1;
        for i := 1 to dimF do begin
            leerCliente (c);
            cClien[i] := c;
        end;
    end;

var
    vCiu: vectorCiudades;
    vMono: vectorMono;
    cClien: vectorClientes;
    
begin
    cargarVectorClientes (cClien);
    inicializarContadores (vCiu, vMono);
    recorrerVector (cClien, vCiu, vMono);
end.


