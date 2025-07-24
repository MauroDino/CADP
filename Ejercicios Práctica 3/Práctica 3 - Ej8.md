<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%203/P3%20Ej8.jpg?raw=true" alt="Diagrama ejercicio 8, práctica 3" width="900" height="900">
</p>

```
{
La Comisión Provincial por la Memoria desea analizar la información de los proyectos presentados en el
programa Jóvenes y Memoria durante la convocatoria 2020. Cada proyecto posee un código único, un título, el
docente coordinador (DNI, nombre y apellido, email), la cantidad de alumnos que participan del proyecto, el
nombre de la escuela y la localidad a la que pertenecen. Cada escuela puede presentar más de un proyecto.
La información se ingresa ordenada consecutivamente por localidad y, para cada localidad, por escuela. Realizar
un programa que lea la información de los proyectos hasta que se ingrese el proyecto con código -1 (que no
debe procesarse), e informe:
● Cantidad total de escuelas que participan en la convocatoria 2018 y cantidad de escuelas por cada
localidad.
● Nombres de las dos escuelas con mayor cantidad de alumnos participantes.
● Título de los proyectos de la localidad de Daireaux cuyo código posee igual cantidad de dígitos pares e
impares.
}

program Hello;

type
    coordinador = record
        documento: integer;
        NyA: string;
        email: string;
    end;

    proyecto = record
        codigo: integer;
        titulo: string;
        docente: coordinador;
        cantAlu: integer;
        nombreEscue: string;
        localidad: string;
    end;

function impar (num: integer): integer;
    var
        espar: integer;
        digito: integer;
    begin
        espar := 0;
        while (num <> 0) do begin
            digito := num mod 10;
            if (digito mod 2 = 0) then
                espar := espar +1;
            num := num div 10;
        end;
        impar := espar;
    end;
    
function par (num: integer): integer;
    var
        espar: integer;
        digito: integer;
    begin
        espar := 0;
        while (num <> 0) do begin
            digito := num mod 10;
            if (digito mod 2 = 0) then
                espar := espar +1;
            num := num div 10;
        end;
        par := espar;
    end;
    
procedure leerProyecto (var p: proyecto);
    begin
        writeln ('Ingresar código único: ');
        readln (p.codigo);
        if (p.codigo <> -1) then begin
            writeln ('Ingresar título del proyecto: ');
            readln (p.titulo);
            writeln ('Ingresar DNI del docente: ');
            readln (p.c.documento);
            writeln ('Ingresar nombre y apellido del docente: ');
            readln (p.c.NyA);
            writeln ('Ingresar email del docente: ');
            readln (p.c.email);
            writeln ('Ingresar cantidad de alumnos que participan del proyecto: ');
            readln (p.cantAlu);
            writeln ('Ingresar el nombre de la escuela: ');
            readln (p.nombreEscue);
            writeln ('Ingresar localidad: ');
            readln (p.localidad);
            writeln ('Ingresar código único: ');
            readln (p.codigo);
        end;
    end;
    
var
    p: proyecto;
    c: coordinador;
    cantEscue: integer;
    locaActual: string;
    cantEscueLoca: integer;

begin
    cantEscue := 0;
    locaActual := ' ';
    cantEscueLoca := 0;
    

    leerProyecto (p);
    while (p.codigo <> -1) do begin
        cantEscue := cantEscue + 1;
        locaActual := p.localidad;

        while (p.localidad = locaActual) and (p.codigo <> -1) do begin
            cantEscueLoca := cantEscueLoca + 1;
            
            if (par(p.codigo) = impar(p.codigo)) then
                writeln ('Título de los proyectos de la localidad de Daireaux con igual cantidad de dígitos pares e impares: ', p.titulo);
        end;
        writeln ('De ', locaActual, ' se anotaron ', cantEscueLoca, ' escuelas.');
        leerProyecto (p);
    end;
    writeln ('La cantidad de escuelas que participaron de la convocatoria es: ', cantEscue);
end.

● Nombres de las dos escuelas con mayor cantidad de alumnos participantes.
