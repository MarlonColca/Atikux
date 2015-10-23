# Atikux
Codigo Ejemplo de como hacer factura electronica.

En la carpeta:

..\Atikux\Atikux\bin\Debug

Esta el ejecutable: Atikux
Se le llama as�: Atikux 20392654861-01-F001-1.zip

D�nde 20392654861-01-F001-1.zip es el zip que contiene la factura, est� en inputs
La respuesta de Sunat estar� guardada en un zip dentro de ..\Atikux\Atikux\bin\Debug\outputs

Setting up(Visual Studio):

1. Agregar una referencia de servicio y poner esta direccion:
https://www.sunat.gob.pe:443/ol-ti-itcpgem-beta/billService?wsdl

Para mas informaci�n revisar: 
http://orientacion.sunat.gob.pe/index.php?option=com_content&view=article&id=1899:informacion-de-interes&catid=259:factura-electronica-desde-sistemas-contribuyente&Itemid=468

2. Ahora dentro del proyecto, buscar un archivo llamado "app.config". Buscar esta parte:

<endpoint address="https://www.sunat.gob.pe:443/ol-ti-itcpgem-beta/billService"
                binding="basicHttpBinding" bindingConfiguration="BillServicePortBinding"
                contract="DocumentosElectronicoSunat.billService" name="BillServicePort" />

Y reemplazarla por:


<endpoint address="https://www.sunat.gob.pe:443/ol-ti-itcpgem-beta/billService"
                binding="basicHttpBinding" bindingConfiguration="BillServicePortBinding"
                contract="DocumentosElectronicoSunat.billService" name="BillServicePort" >
              <headers>
                <wsse:Security mustUnderstand="0" xmlns:wsse="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
                  <wsse:UsernameToken Id="ABC-123">
                    <wsse:Username>[tu numero de ruc]MODDATOS</wsse:Username>
                    <wsse:Password>moddatos</wsse:Password>
                  </wsse:UsernameToken>
                </wsse:Security>
              </headers>
            </endpoint> 


MODDATOS es un usuario de pruebas, no necesita certificados ni nada, pero para los procesos de homologaci�n y producci�n si los vas a necesitar



3. El c�digo est� solo en Program.cs y en classes/SunatServices. Donde podr�s encontrar la llamada al m�todo para enviar la factura electr�nica. Los dem�s procesos est�n bien explicados en el manual del desarrollador.


Notas: 
* Adjunto tambi�n un factura que funciona(la copi� del archivo "Guia+XML+Factura+version+2+0.pdf" - P�gina 65 que est� colgada en sunat)
* Para hacer un programa que genere la factura, hay que tener en cuenta todos los c�digos que utiliza sunat, distribuidos en 17 cat�logos. Ahora estoy trabajando en documentarlos para que nadie tenga problemas a la hora de relacionar los c�digos de sunat con los de la empresa emisora del documento electr�nico
* No es un trabajo final, solo es para tener una idea de como est� funcionando el mecanismo de facturaci�n eletr�nica de Sunat - Per�



  