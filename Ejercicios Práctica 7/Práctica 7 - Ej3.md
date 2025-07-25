

<p align="center">
<img src="https://github.com/MauroDino/Images/blob/main/Pr%C3%A1ctica%207/Pr%C3%A1ctica%207,%20ejercicio%203.jpg?raw=true" alt="Diagrama ejercicio 3, práctica 7" width="900" height="900">
</p>

```
{
Una remisería dispone de información acerca de los viajes realizados durante el mes de mayo de 2020. De
cada viaje se conoce: número de viaje, código de auto, dirección de origen, dirección de destino y
kilómetros recorridos durante el viaje. Esta información se encuentra ordenada por código de auto y para
un mismo código de auto pueden existir 1 o más viajes. Se pide:
a. Informar los dos códigos de auto que más kilómetros recorrieron.
b. Generar una lista nueva con los viajes de más de 5 kilómetros recorridos, ordenada por número de
viaje.
}

program P7Ej3;

type
    cadena20 = string[20];

    viaje = record
        numero: integer;
        codigo: integer;
        direccionOr: cadena20;
        direccionDest: cadena20;
        kilometros: integer;
    end;

    lista = ^nodo;

    nodo = record
        dato: viaje;
        sig: lista;
    end;

procedure insertarOrdenado (v: viaje; var L2: lista);
    var
        actual: lista;
        anterior: lista;
        nuevo: lista;

    begin
        new (nuevo);
        nuevo^.dato := v;
        anterior := L2;
        actual := L2;
        while (actual <> nil) and (v.num > actual^.dato.num) do begin
            anterior := actual;
            actual := actual^.sig;
        end;
        if (anterior = actual) then
            L := nuevo
        else
            anterior^.sig := nuevo;
        nuevo^.sig := actual;
    end;

procedure maximos (var codMax1: integer; var codMAx2: integer; var kmMax1: integer; var kmMax2: integer; km: integer; cod: integer);
    begin
        if (km > kmMax1) then begin
            kmMax2 := kmMax1;
            codMax2 := codMax1;
            kmMax1 := km;
            codMAx1 := cod;
        end
        else begin
            if (km > kmMax2) then begin
                kmMax2 := km;
                codMax2 := cod;
            end;
        end;
    end;

procedure recorrerLista (L: lista; var L2: lista);
    var
        codMax1: integer;
        codMax2: integer;
        kmMax1: integer;
        kmMax2: integer;
        codAutAct: integer;
        v: viaje;
        totKmReco: integer;
    
    begin
        codMax1 := 0;
        codMax2 := 0;
        kmMax1 := -1;
        kmMax2 := -1;
        totKmReco := 0;
        
        while (L <> nil) do begin
                codAutoAct := L^.dato.codigo;
                while (L <> nil) and (codAutoAct = L^.dato.codigo) do begin
                    totKmReco := totKmReco + L^.dato.kilometros;
                    
                    if (L^.dato.kilometros > 5) then
                        insertarOrdenado (L^.dato, L2);
                    L := L^.sig;
                end;
                maximos (codMax1, codMax2, kmMax1, kmMax2, totKmReco, L^.dato.codigo);
        end;
        writeln ('Los dos códigos que hicieron más kilómetros son: ', codMax1, ' y ', codMax2);
    end;

procedure cargarLista (var L: lista); // se dispone
    begin
    
    end;

var
    L: lista;
    L2: lista;

begin
    L := nil;
    L2 := nil;
    cargarLista (L); // se dispone
    recorrerLista (L, L2);
end.
