---
title: "Desarrollo de la aplicación | Azure RMS"
description: "Instrucciones sobre cómo desarrollar una aplicación mediante RMS SDK 2.1."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/01/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4560a1cf3424ae4dddd3a0675b62e9c5e55de9fa
ms.openlocfilehash: 1f46d93a47fae3b7e7de334db73b7e7b65ea6eea


---

# <a name="developing-your-application"></a>Desarrollo de la aplicación

Este tema contiene instrucciones esenciales sobre los principales aspectos de una aplicación habilitada para RMS y puede servir como base para el desarrollo de su propia aplicación.

## <a name="introduction"></a>Introducción

Las instrucciones de este tema se basan en la aplicación de ejemplo, *IPCHelloWorld*, que le servirá para conocer los conceptos básicos y el código de una aplicación con derechos habilitados. El proyecto *IPCHelloWorld* ya está configurado para Rights Management Services SDK 2.1.

### <a name="download-sample"></a>Descargar ejemplo
- Compruebe que se ha registrado en el sitio de Connect:
  - Para registrarse, vaya a [Connect](http://connect.microsoft.com)
  - Inicie sesión con su cuenta de Microsoft
  - Vaya al [Sitio de Rights Management Connect](https://connect.microsoft.com/site1170)
  - Combinación 
- Puede descargar la aplicación de ejemplo *IPCHellowWorld* completa, como [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)

Si quiere información sobre cómo configurar un proyecto nuevo para usar RMS SDK 2.1, vea [Configure Visual Studio](how-to-configure-a-visual-studio-project-to-use-the-ad-rms-sdk-2-0.md) (Configurar Visual Studio).



## <a name="loading-msipcdll"></a>Carga de MSIPC.dll

Antes de que se puedan llamar a las funciones de RMS SDK 2.1, primero debe llamarse a la función [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) para cargar el archivo MSIPC.dll.

        C++
        hr = IpcInitialize();
        if (FAILED(hr)) {
          wprintf(L"Failed to initialize MSIPC. Are you sure the runtime is installed?\n");
          goto exit;
        }

## <a name="enumerating-templates"></a>Enumeración de plantillas

Una plantilla de RMS define la directiva usada para proteger los datos, es decir, define los usuarios que tienen acceso a los datos y sus derechos. Las plantillas de RMS se instalan en el servidor RMS.

El fragmento de código siguiente enumera las plantillas de RMS disponibles en el servidor RMS predeterminado.

      C++
      hr = IpcGetTemplateList(NULL, 0, 0, NULL, NULL, &pcTil);

      if (FAILED(hr)) {
        DisplayError(L"IpcGetTemplateList failed", hr);
        goto exit;
      }

Mediante esta llamada se recuperan las plantillas de RMS que están instaladas en el servidor predeterminado, se cargan los resultados en la estructura [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx), a la que apunta la variable *pcTil*, y luego se muestran las plantillas.

      C++
      if (0 == pcTil->cTi) {
        wprintf(L"*** No templates configured for your RMS server ***\n\n");
        wprintf(L"\\------------------------------------------------------\n\n");
        goto exit;
      }

      for (DWORD dw = 0; dw < pcTil->cTi; dw++) {
        wprintf(L"Template #%d:\n", dw);
        wprintf(L"    Name:         %s\n", pcTil->aTi[dw].wszName);
        wprintf(L"    Description:  %s\n", pcTil->aTi[dw].wszDescription);
        wprintf(L"    Issued by:    %s\n", pcTil->aTi[dw].wszIssuerDisplayName);
        wprintf(L"\n");
      }

## <a name="serializing-a-license"></a>Serialización de una licencia

Para poder proteger los datos, es necesario serializar una licencia y obtener una clave de contenido. La clave de contenido se usa para cifrar los datos confidenciales. Por lo general, la licencia serializada va adjunta a los datos cifrados y es usada por el consumidor de los datos protegidos. El consumidor deberá llamar a la función [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx) con la licencia serializada para obtener la clave de contenido que le permita descifrar el contenido y obtener la directiva asociada con el contenido.

Por simplicidad, use la primera plantilla de RMS devuelta por [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) para serializar una licencia.

Normalmente, se usaría un cuadro de diálogo de la interfaz de usuario para permitir al usuario seleccionar la plantilla que quiera.

      C++
      hr = IpcSerializeLicense((LPCVOID)pcTil->aTi[0].wszID, IPC_SL_TEMPLATE_ID,
        0, NULL, &hContentKey, &pSerializedLicense);

      if (FAILED(hr)) {
        DisplayError(L"IpcSerializeLicense failed", hr);
        goto exit;
      }

Una vez hecho esto, ya tiene la clave de contenido *hContentKey*, y la licencia serializada, *pSerializedLicense*, que debe asociar a los datos protegidos.


## <a name="protecting-data"></a>Protección de datos

Ahora está listo para cifrar los datos confidenciales mediante la función [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx). En primer lugar, debe preguntar a la función **IpcEncrypt** cuál será el tamaño de los datos cifrados.

      C++
      cbText = (DWORD)(sizeof(WCHAR)*(wcslen(wszText)+1));
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        NULL, 0, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Aquí, *wszText* contiene el texto sin formato que se va a proteger. La función [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx) devuelve el tamaño de los datos cifrados en el parámetro *cbEncrypted*.

Ahora asigne la memoria para los datos cifrados.

      C++
      pbEncrypted = (PBYTE)LocalAlloc(LPTR, cbEncrypted);

      if (NULL == pbEncrypted) {
        wprintf(L"Out of memory\n");
        goto exit;
      }

Por último, puede realizar el cifrado en sí.

      C++
      hr = IpcEncrypt(hContentKey, 0, TRUE, (PBYTE)wszText, cbText,
        pbEncrypted, cbEncrypted, &cbEncrypted);

      if (FAILED(hr)) {
        DisplayError(L"IpcEncrypt failed", hr);
        goto exit;
      }

Completado este paso, ya tiene los datos cifrados, *pbEncrypted*, y la licencia serializada, *pSerializedLicense*, que los consumidores usarán para descifrar los datos.

## <a name="error-handling"></a>Control de errores

En esta aplicación de ejemplo, la función *DisplayError* se usa para controlar los errores.

      C++
      void DisplayError(LPCWSTR wszErrorInfo, HRESULT hrError)
      {
        LPCWSTR wszErrorMessageText = NULL;

        if (SUCCEEDED(IpcGetErrorMessageText(hrError, 0, &wszErrorMessageText))) {
          wprintf(L"%s: 0x%08X (%s)\n", wszErrorInfo, hrError, wszErrorMessageText);
        }
        else {
          wprintf(L"%s: 0x%08X\n", wszErrorInfo, hrError);
        }
      }

La función *DisplayError* usa la función [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx) para obtener el mensaje de error del código de error correspondiente e imprimirlo en la salida estándar.

## <a name="cleaning-up"></a>Limpieza

Antes de acabar, hay que liberar todos los recursos asignados.

      C++
      if (NULL != pbEncrypted) {
        LocalFree((HLOCAL)pbEncrypted);
      }

      if (NULL != pSerializedLicense) {
        IpcFreeMemory((LPVOID)pSerializedLicense);
      }

      if (NULL != hContentKey) {
        IpcCloseHandle((IPC_HANDLE)hContentKey);
      }

      if (NULL != pcTil) {
        IpcFreeMemory((LPVOID)pcTil);
      }

## <a name="related-topics"></a>Temas relacionados

- [Instrucciones e información para desarrolladores](developer-notes.md)
- [IpcEncrypt](https://msdn.microsoft.com/library/hh535259.aspx)
- [IpcGetErrorMessageText](https://msdn.microsoft.com/library/hh535261.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_TIL](https://msdn.microsoft.com/library/hh535283.aspx)
- [Webinar_Collateral.zip](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)



<!--HONumber=Nov16_HO1-->


