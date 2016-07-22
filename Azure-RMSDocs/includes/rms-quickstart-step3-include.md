![](../media/AzRMS_QuickStartSteps3.PNG)

Para este paso, primero use Word para crear y guardar el documento que desea proteger y asígnele el nombre **Confidential.docx**. Para este tutorial, lo que importa no es el texto en concreto, si no el hecho de que haya texto para confirmar más fácilmente si el recipiente autorizado puede leerlo. Por ejemplo, puede escribir: **Si puede leer esto en los datos adjuntos del correo electrónico, el remitente ha compartido correctamente un archivo protegido con Azure RMS.**

A continuación, estará listo para compartir de forma segura este documento por correo electrónico.

![Recurso compartido de Azure RMS por capturas de pantalla de correo electrónico](../media/AzRMS_Tutorial_3_Screenshots.png)

#### Para compartir de forma segura el documento por correo electrónico

1.  En Outlook, cree un mensaje nuevo y adjunte el archivo que acaba de crear.

2.  En el cuadro **Para** , escriba una o más direcciones de correo electrónico empresarial. Asegúrese de especificar una dirección de correo electrónico empresarial, como **janetm@contoso.com** o **p.dover@fabrikam.com** porque, actualmente, Azure Rights Management no es compatible con las direcciones de correo electrónico personales que se usan en casa con el proveedor de Internet. No se preocupe por saber si la persona a la que envía el archivo también tiene Azure Rights Management o no.

3.  Escriba un asunto, como  **Documento confidencial** y, a continuación, escriba un mensaje breve para el correo electrónico, como **Lea este documento confidencial y no lo comparta con otros.**

4.  A continuación, en la pestaña **Mensaje** del grupo **RMS** , haga clic en **Uso compartido seguro** y luego haga clic en **Uso compartido seguro** nuevamente:

5.  En el cuadro de diálogo **Uso compartido seguro** :

    1.  Seleccione **Visor – Solo ver**.

        Esto significa que los destinatarios podrán ver el documento pero no editarlo ni imprimirlo.

    2.  Seleccione **Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**.

        Recibirá una notificación por correo electrónico cada vez que los destinatarios intenten abrir el archivo adjunto, y también si alguien más intenta abrirlo (por ejemplo, cuando el destinatario reenvía el correo electrónico a un compañero de trabajo. En este último caso, verá que se deniega el acceso y, a partir de los detalles del usuario, podrá decidir si enviar a esa persona una copia del documento que puede abrir.

    3.  Seleccione **Permítame revocar el acceso a estos documentos de forma instantánea**.

        Esta opción requiere que los destinatarios tengan una conexión a Internet cada vez que abran el archivo adjunto, pero con el beneficio de que si más adelante se revoca el documento, la próxima vez que intenten abrirlo, no podrán hacerlo. Si no selecciona esta opción, es posible que los destinatarios puedan abrirlo incluso sin una conexión a Internet, pero con la desventaja de que si más adelante se revoca el documento, puede producirse una demora para que esto tenga efecto.

    4.  Haga clic en **Enviar ahora**.

        El correo electrónico con datos adjuntos se envía a las direcciones de correo electrónico que especificó. Además del mensaje de correo electrónico, verán instrucciones sobre cómo leer el documento adjunto que está protegido con Azure Rights Management.

Ahora que ha enviado el documento protegido, está listo para pedir a los destinatarios que esperen a que llegue para luego abrirlo. Sin embargo, no debe cerrar Outlook, porque lo volveremos a usar en el último paso para realizar un seguimiento de los datos adjuntos.

|Si desea obtener más información|Información adicional|
|--------------------------------|--------------------------|
|Todas las instrucciones y los métodos alternativos para proteger los archivos que comparte por correo electrónico   →|[Proteger un archivo que comparte por correo electrónico mediante la aplicación de uso compartido Rights Management.](../rms-client/sharing-app-protect-by-email.md)|
|Acerca de las opciones del cuadro de diálogo **Uso compartido seguro** →|[Opciones del cuadro de diálogo para la aplicación de uso compartido Rights Management](../rms-client/sharing-app-dialog-box.md)|


<!--HONumber=Jun16_HO4-->


