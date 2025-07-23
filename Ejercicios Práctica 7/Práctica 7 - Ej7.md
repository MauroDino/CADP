

<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%207/Pr%C3%A1ctica%207,%20ejercicio%207.jpg?raw=true" alt="Diagrama ejercicio 5, práctica 3" width="900" height="900">
</p>

```
{
7. La Facultad de Informática desea procesar la información de los alumnos que finalizaron la carrera de
Analista Programador Universitario. Para ello se deberá leer la información de cada alumno, a saber:
número de alumno, apellido, nombres, dirección de correo electrónico, año de ingreso, año de egreso y las
notas obtenidas en cada una de las 24 materias que aprobó (los aplazos no se registran).
1. Realizar un módulo que lea y almacene la información de los alumnos hasta que se ingrese el alumno
con número de alumno -1, el cual no debe procesarse. Las 24 notas correspondientes a cada alumno
deben quedar ordenadas de forma descendente.
2. Una vez leída y almacenada la información del inciso 1, se solicita calcular e informar:
a. El promedio de notas obtenido por cada alumno.
b. La cantidad de alumnos ingresantes 2012 cuyo número de alumno está compuesto únicamente
por dígitos impares.
c. El apellido, nombres y dirección de correo electrónico de los dos alumnos que más rápido se
recibieron (o sea, que tardaron menos años)
3. Realizar un módulo que, dado un número de alumno leído desde teclado, lo busque y elimine de la
estructura generada en el inciso 1. El alumno puede no existir.
}
// NO TERMINÉ DE RESOLVER. HASTA DONDE LLEGUÉ, TENGO QUE CORREGIR UNAS CUANTAS COSAS
program P7Ej7;


type
    cadena20 = string[20];

    vectorMaterias = array [1 .. 24] of integer;

    alumno = record
        numero: integer;
        apellido: cadena20;
        nombre: cadena20;
        email: cadena20;
        anioIngre: integer;
        anioEgre: integer;
        nota: vectorMaterias;
    end;

    lista = ^nodo;

    nodo = record
        dato: alumno;
        sig: lista;
    end;

procedure eliminarAlumno (var L: lista; numero: integer);
    var
        anterior: lista;
        actual: lista;

    begin
        actual := L;
        while (actual <> nil) and (actual^.dato.numero <> numero) do begin
            anterior := actual;
            actual := actual^.sig;
        end;
        if (actual <> nil) then
            if (actual = L) then
                L := L^.sig
            else
                anterior^.sig := actual^.sig;
        dispose (actual);
    end;

procedure minimos (var ap1: cadena20; var ap2: cadena20; var nombre1: cadena20; var nombre2: cadena20; var email1: cadena20; var email2: cadena20; apellido: cadena20; nombre: cadena20; email: cadena20; anioIngre: integer; anioEgre: integer; var tiempo1: integer; var tiempo2: integer);
    var
        demora: integer;

    begin
        demora := anioEgre - anioIngre;
        if (demora < tiempo1) then begin
            tiempo2 := tiempo1;
            nombre2 := nombre1;
            ap2 := ap1;
            email2 := email1;
            tiempo1 := demora;
            nombre1 := nombre;
            ap1 := apellido;
            email1 := email;
        end
        else begin
            if (demora < tiempo2) then begin
                tiempo2 := demora;
                nombre2 := nombre;
                ap2 := apellido;
                email2 := email;
            end;
        end;
    end;

function cumple (num: integer): boolean;
    var
        ok: boolean;
        dig: integer;
        
        begin
        ok := true;
        cantPar := 0;
        cantImpar := 0;
        while (num <> 0) do begin
            dig := dig mod 10;
            if (dig mod 2 = 0) then
                ok := false;
            num := num div 10;
        end;
        cumple := ok;
    end;

procedure procesarLista (L: lista; vm: vectorMaterias);
    var
        i: integer;
        totalNotas: integer;
        cantVeinteDoce: integer;
        ap1: cadena20;
        ap2: cadena20;
        nombre1: cadena20;
        nombre2: cadena20;
        email1: cadena20;
        email2: cadena20;
        tiempo1: integer;
        tiempo2: integer;
        numeroEli: integer;
        J: integer;

    begin
        while (L <> nil) do begin
            totalNotas := 0;
            cantVeinteDoce := 0;
            tiempo1 := 9999;
            tiempo2 := 9999;
            while (j <= 24) do begin
                totalNotas := totalNotas + vm[j];
                j := j + 1;
            end;
            writeln ('El promedio de notas obtenido por el alumno ', L^.dato.nombre, ' es: ', totalNotas / 24);

            if (L^.dato.anioIngre = 2012) and (cumple(L^.dato.numero)) then
                cantVeinteDoce := cantVeinteDoce + 1;

            minimos (ap1, ap2, nombre1, nombre2, email1, email2, L^.dato.apellido, L^.dato.nombre, L.^.dato.email, L^.dato.anioIngre, L^.dato.anioEgre, tiempo1, tiempo2);

            L := L^.sig;
        end; 


        writeln ('Ingrese número de alumno a eliminar: ');
        readln (numeroEli);
        eliminarAlumno (L, numeroEli);
    end;
procedure agregarAtras (var L: lista; a: alumno; ultimo: lista);
    var
        nuevo: lista;
    
    begin
        new (nuevo);
        nuevo^.dato := a;
        nuevo^.sig := nil;
        if (L = nil) then
            L := nuevo
        else
            ultimo^.sig := nuevo;
        ultimo := nuevo;
    end;

procedure leerAlumno (var a: alumno; var vm: vectorMaterias);
    var
        i: integer;
        nota: integer;

    begin
        writeln ('Ingrese el número de alumno: ');
        readln (a.numero);
        if (a.numero <> -1) then begin
            writeln ('Ingrese el nombre: ');
            readln (a.nombre);
            writeln ('Ingrese email: ');
            readln (a.email);
            writeln ('Ingrese año de ingreso: ');
            readln (a.anioIngre);
            writeln ('Ingrese año de egreso: ');
            readln (a.anioEgre);
            for i := 1 to 24 do begin
                writeln ('Ingresar la nota de la materia ', i, ': ');
                readln (nota);
                if (nota > 3) and (nota < 11) and (nota > vm[i]) then
                    vm[i] := nota;
            end;
        end;
    end;

procedure cargarLista (var L: lista; var vm: vectorMaterias);
    var
        a: alumno;
        ultimo: lista;

    begin
        ultimo := nil;
        leerAlumno (a, vm);
        while (a.numero <> -1) do begin
            agregarAtras (L, a, ultimo); // porque quiero practicarlo
            leerAlumno (a, vm);
        end;

    end;

var
    L: lista;
    vm: vectorMaterias;

begin
    L: nil;

    cargarLista (L, vm);
end.
