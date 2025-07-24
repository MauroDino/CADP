<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%204/Pr%C3%A1ctica%204%20P1,%20ejercicio%2014.jpg?raw=true" alt="Diagrama ejercicio 14, práctica 4, parte 1" width="900" height="900">
</p>

```

{

El repositorio de código fuente más grande en la actualidad, GitHub, desea estimar el monto invertido
en los proyectos que aloja. Para ello, dispone de una tabla con información de los desarrolladores que
participan en un proyecto de software, junto al valor promedio que se paga por hora de trabajo:

CÓDIGO ROL                                VALOR/HORA (USD)
1      Analista Funcional                 35,20
2      Programador                        27,45
3      Administrador de bases de datos    31,03
4      Arquitecto de software             44,28
5      Administrador de redes y seguridad 39,87
Nota: los valores/hora se incluyen a modo de ejemplo

Realizar un programa que procese la información de los desarrolladores que participaron en los 1000
proyectos de software más activos durante el año 2017. De cada participante se conoce su país de
residencia, código de proyecto (1 a 1000), el nombre del proyecto en el que participó, el rol que cumplió
en dicho proyecto (1 a 5) y la cantidad de horas trabajadas. La lectura finaliza al ingresar el código de
proyecto -1, que no debe procesarse. 

Al finalizar la lectura, el programa debe informar:
a. El monto total invertido en desarrolladores con residencia en Argentina.
b. La cantidad total de horas trabajadas por Administradores de bases de datos.
c. El código del proyecto con menor monto invertido.
d. La cantidad de Arquitectos de software de cada proyecto

}

program Hello;

const
    mil: 1000;


type

    rango = 1 .. mil;
    otroRango = 1 .. 5;

    programador = record
        pais: string;
        codigo: rango;
        nombreProyecto: string;
        rol: otroRango;
        cantHoras: real;
    end;

    vectorSalarios = array [otroRango] of real;
    vectorContadorMontos = array [rango] of real; // Almacena los montos, para después analizar cuando sea necesario
    vectorArquitectos = array [rango] of integer;

procedure calcularMinimo (vc: vectorContadorMontos; var minimo: integer);
    var
        i: integer;
        aux: real;

    begin
        aux := 9999;
        for i := 1 to mil do begin
            if (vc[i] < aux) then begin
                aux := vc[i];
                minimo := i;
            end;
        end;

    end;

procedure leerProgramador (var p: programador);
    begin
        writeln ('Ingresar el código del proyecto: ');
        readln (p.codigo);
        if (p.codigo <> -1) then begin
            writeln ('Ingresar país del programador: ');
            readln (p.pais);
            writeln ('Ingresar el nombre del proyecto: ');
            readln (p.nombreProyecto);
            writeln ('Ingresar el rol del programador, entre 1 y 5: ');
            readln (p.rol);
            writeln ('Ingresar cantidad de horas trabajadas: ');
            readln (p.cantHoras);
        end;
        
    end;

procedure inicializarVectorArqui (var vArqui: vectorArquitectos);
    var
        i: integer;
    
    begin
        for i := 1 to mil do begin
            vArqui[i] := 0;
        end;
    end;

procedure cargarVectorSalarios (var vSal: vectorSalarios);   
    begin
        vSal[1] := 35.20;
        vSal[2] := 27.45;
        vSal[3] := 31.03;
        vSal[4] := 44.28;
        vSal[5] := 39.87;
    end;


procedure inicializarVector (var vc: vectorContadorMontos);
    var
        i: integer;
    
    begin
        for i := 1 to mil do begin
            vc[i] := 0;
        end;
    end;

var
    vc: vectorContadorMontos;
    p: programador;
    mTotArg: real;
    vSalarios : vectorSalarios;
    totHsAdmin: real;
    vArqui: vectorArquitectos;
    montos: real;
    i: integer;
    minimo: integer;
    montosAux: real;
    
begin
    inicializarVector (vc); // este vector va a llevar el total de montos por proyecto, para después hacer la comparación e informar mínimo
    cargarVectorSalarios (vSalarios); // este vector va a tener en cada índice el valor de hora por rol
    inicializarVectorArqui (vArqui); // este vector va a llevar la cantidad de arquitectos por proyecto. Cada proyecto es un índice.
    
    mtotArg := 0;
    totHsAdmin := 0;
    minimo := 0;
    
    leerProgramador (p);
    while (p.codigo <> -1) do begin

        
        montosAux := (vSalarios[p.rol] * p.cantHoras); // determino el monto por proyecto
        vc[p.codigo] := vc[p.codigo] + montosAux; // cargo los montos para después compararlos y obtener el mínimo
    
        //a. El monto total invertido en desarrolladores con residencia en Argentina.
        if (p.pais = 'Argentina') then
            mTotArg := mTotArg + (vSalarios[p.rol] * p.cantHoras);

        // b. La cantidad total de horas trabajadas por Administradores de bases de datos.
        if (p.rol = 3) then
            totHsAdmin := totHsAdmin + p.cantHoras;

        //d. La cantidad de Arquitectos de software de cada proyecto
        if (p.rol = 4) then 
            vArqui[p.codigo] := vArqui[p.codigo] + 1;

        leerProgramador (p);
    end;

    //c. El código del proyecto con menor monto invertido. Está fuera del while porque se tiene que hacer una vez que terminó la carga.
        calcularMinimo (vc, minimo);
    
    writeln ('El monto total invertido en desarrolladores con residencia en Argentina es: ', mTotArg:0:2);
    writeln ('La cantidad total de horas trabajadas por administradores de bases de datos es: ', totHsAdmin:0:2);
    writeln ('El código del proyecto con menor monto invertido es: ', minimo);

    for i := 1 to mil do begin
        writeln ('La cantidad de Arquitectos de software de cada proyecto es: ', vArqui[i]);
    
    end;
end.
