<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%204/Pr%C3%A1ctica%204%20P1,%20ejercicio%207.jpg?raw=true" alt="Diagrama ejercicio 7, práctica 4, parte 1" width="900" height="900">
</p>

```
{

Realizar un programa que lea números enteros desde teclado hasta que se ingrese el valor -1 (que no
debe procesarse) e informe:
a. La cantidad de ocurrencias de cada dígito procesado.
b. El dígito más leído.
c. Los dígitos que no tuvieron ocurrencias.

Por ejemplo: si la secuencia que se lee es: 63 34 99 94 96 -1, el programa deberá informar:
Número 3: 2 veces
Número 4: 2 veces
Número 6: 2 veces
Número 9: 4 veces
El dígito más leído fue el 9.
Los dígitos que no tuvieron ocurrencias son: 0, 1, 2, 5, 7, 8

}

program Hello;

type
    vector = array [0..9] of integer;
    
procedure informar (v: vector);
    var
        max: integer;
        i: integer;
        digimax: integer;
    
    begin
        max := -1;
        digimax := 0;
        
        for i := 0 to 9 do begin
            if (v[i] > max) then begin
                max := v[i];
                digimax := i;
            end;
            
            if (v[i] >= 1) then
                writeln ('El número ', i , ' apareció ', v[i], ' veces.')
            
        end;
        
        for i := 0 to 9 do begin
            if (v[i] = 0) then
                writeln ('El número ', i, ' no tiene ocurrencias.');
        end;
        
        writeln ('El número ', digimax, ' fue el que más veces apareció.');
    end;
    
procedure contar (var v: vector);
    var
        num: integer;
        digito: integer;

    begin
        writeln ('Ingresar un número entero: ');
        readln (num);
        while (num <> -1) do begin
            while (num <> 0) do begin
                digito := num mod 10; //me quedo con el último dígito
                v[digito] := v[digito] + 1;
                num := num div 10; //achico el número original hasta que sea 0
            end;
        writeln ('Ingresar un número entero: ');
        readln (num);
        end;
    end;
    
procedure inicializar (var v: vector);
    var
        i: integer;
    
    begin
        for i := 0 to 9 do begin
            v[i] := 0;
        end;
    end;

var
    
    v: vector;

begin
    inicializar (v);
    contar (v);
    informar (v);
end.
