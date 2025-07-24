<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%204/Pr%C3%A1ctica%204%20P1,%20ejercicio%2012.jpg?raw=true" alt="Diagrama ejercicio 12, práctica 4, parte 1" width="900" height="900">
</p>

```

{

12. En astrofísica, una galaxia se identifica por su nombre, su tipo (1. elíptica; 2. espiral; 3. lenticular; 4.
irregular), su masa (medida en kg) y la distancia en pársecs (pc) medida desde la Tierra. La Unión
Astronómica Internacional cuenta con datos correspondientes a las 53 galaxias que componen el
Grupo Local. Realizar un programa que lea y almacene estos datos y, una vez finalizada la carga,
informe:
a. La cantidad de galaxias de cada tipo.
b. La masa total acumulada de las 3 galaxias principales (la Vía Láctea, Andrómeda y Triángulo) y el
porcentaje que esto representa respecto a la masa de todas las galaxias.
c. La cantidad de galaxias no irregulares que se encuentran a menos de 1000 pc.
d. El nombre de las dos galaxias con mayor masa y el de las dos galaxias con menor masa

}

program Hello;

const
    galas = 53;

type
    rango = 1 .. 4;

    tipos = array [rango] of integer;
    
    galaxia = record
        nombre: string;
        tipo: rango;
        masa: integer;
        distancia: integer;
    end;

    grupo = array [ 1 .. galas] of galaxia;

procedure informar (g: grupo; tipis: tipos; cantTotMasa: integer; cantGala: Integer; masaMAx1: string; masaMax2: string; masaMin1: string; 
    masaMin2: string; promedio: real);

    var
        i: integer;
        j: integer;

    begin
            for j := 1 to 4 do begin
                writeln ('La cantidad del tipo de galaxia ', j , ' es: ', tipis[j]);
            end;
            WriteLn ('La masa total acumulada es: ', cantTotMasa);
            WriteLn ('El porcentaje es: ', promedio:2:0, ' %');
            writeln ('La cantidad de galaxias no irregulares que están a menos de 1000 pc es: ', cantGala);
            WriteLn ('Los nombres de las dos galaxias con mayor masa son: ', masaMAx1, ' y ', masaMax2);
            WriteLn ('Los nombres de las dos galaxias con menor masa son: ', masaMin1, ' y ', masaMin2);
        
    end;

function sacarPromedio (masaGlobal: integer; cantTotMasa: integer): real;
    begin
        sacarPromedio := (cantTotMasa * 100) / masaGlobal;
    end;

procedure minimos (g: grupo; var masaMin1: string; var masaMin2: string);
    var
        i: integer;
        min1: integer;
        min2: integer;
    
    begin
        min1 := 9999;
        min2 := 9999;
        for i := 1 to galas do begin
            if (g[i].masa < min1) then begin
                masaMin2 := masaMin1;
                masaMin1 := g[i].nombre;
                min1 := g[i].masa;
            end else
            if (g[i].masa < min2) then begin
                min2 := g[i].masa;
                masaMin2 := g[i].nombre;
            end;
        end;
    end;

procedure maximos (g: grupo; var masaMax1: string; var masaMax2: string);
    var
        i: integer;
        max1: integer;
        max2: integer;
    
    begin
        max1 := -1;
        max2 := -1;
        for i := 1 to galas do begin
            if (g[i].masa > max1) then begin
                masaMax2 := masaMax1;
                masaMax1 := g[i].nombre;
                max1 := g[i].masa;
            end else
            if (g[i].masa > max2) then begin
                max2 := g[i].masa;
                masaMax2 := g[i].nombre;
            end;
        end;
    end;

procedure inicializartipos (var tipis: tipos);
    var
        i: integer;

    begin
        for i := 1 to 4 do begin
            tipis[i] := 0;
        end;
    end;

procedure analizar (g: grupo; var tipis: tipos; var cantTotMasa: integer; var cantGala: integer; var masaMax1: string; var masaMax2: string; var masaMin1: string; 
    var masaMin2: string; var promedio: real);

    var
        i: integer;
        cantGalas: integer;
        masaGlobal: integer;

    begin
        inicializartipos (tipis);
        cantGalas := 0;
        masaGlobal := 0;
        
        for i := 1 to galas do begin
            if (g[i].nombre = 'via lactea') or (g[i].nombre = 'andromeda') or (g[i].nombre = 'triangulo') then
                cantTotMasa := cantTotMasa + g[i].masa;
                
            cantGalas := cantGalas + 1;
            
            if (g[i].distancia < 1000) and (g[i].tipo <> 4) then
            cantGala := cantGala + 1;
            
            tipis[g[i].tipo] := tipis[g[i].tipo] + 1;

            masaGlobal := g[i].masa + masaGlobal;
        end;
        maximos (g, masaMax1, masaMax2);
        minimos (g, masaMin1, masaMin2);
        promedio := sacarPromedio (masaGlobal, cantTotMasa);      
    end;
    
procedure inicializar (var cantTotMasa: integer; var cantGala: integer; var masaMax1: string; var masaMax2: string; var masaMin1: string;
    var masaMin2: string; var promedio: real);

    begin
        cantTotMasa := 0;
        cantGala := 0;
        masaMax1 := ' ';
        masaMax2 := ' ';
        masaMin1 := ' ';
        masaMin2 := ' ';
        promedio := 0;
    end;

procedure cargar (var gal: galaxia);
    begin
        writeln ('Ingresar nombre de la galaxia: ');
        readln (gal.nombre);
        writeln ('Ingresar número del tipo de galaxia: ');
        readln (gal.tipo);
        Writeln ('Ingresar la masa de la galaxia: ');
        readln (gal.masa);
        writeln ('Ingresar la distancia desde la Tierra: ');
        readln (gal.distancia);
    end;

procedure leer (var g: grupo);
    var
        i: integer;
        gal: galaxia;

    begin
        for i := 1 to galas do begin
            cargar (gal);
            g[i] := gal;
        end;
    end;

var
    g: grupo;
    tipis: tipos;
    cantTotMasa: integer;
    cantGala: integer;
    masaMax1: string;
    masaMax2: string;
    masaMin1: string;
    masaMin2: string;
    promedio: real;

begin
    leer (g);
    inicializar (cantTotMasa, cantGala, masaMax1, masaMax2, masaMin1, masaMin2, promedio);
    analizar (g, tipis, cantTotMasa, cantGala, masaMax1, masaMax2, masaMin1, masaMin2, promedio);
    informar (g, tipis, cantTotMasa, cantGala, masaMax1, masaMax2, masaMin1, masaMin2, promedio);
end.
