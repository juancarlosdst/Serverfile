# Serverfile
SAP ABAP S4/HANA: ¿Cómo permitir al usuario seleccionar un archivo en una carpeta del servidor?

Función: /SAPDMC/LSM_F4_SERVER_FILE

En el parámetro de entrada "DIRECTORY" pones la ruta de la carpeta. 

En el parámetro de salida "SERVERFILE" tendrás el nombre del archivo seleccionado.

El tipo de la variable SERVERFILE puede que ser LOCALFILE.

DATA: ld_serverfile TYPE localfile.

CALL FUNCTION '/SAPDMC/LSM_F4_SERVER_FILE'
  EXPORTING
    directory        = '/SAPINTERFACES/BP/FICHEROS_CARGA' "El nombre de tu directorio
  IMPORTING
    serverfile       = ld_serverfile
  EXCEPTIONS
    canceled_by_user = 1
    OTHERS           = 2.

IF sy-subrc <> 0.

  MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
        WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.

ENDIF.
