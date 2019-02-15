---
title: Ejemplos de código de Linux | Azure RMS
description: En este tema se presentan escenarios importantes y elementos de código para la versión Linux de RMS SDK.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0F7714CA-1D3E-4846-B187-739825B7DE26
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5e955abc9d2d8fb488fa5c425cff44ac5e8c4222
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255827"
---
# <a name="linux-code-examples"></a>Ejemplos de código de Linux

En este tema se presentan escenarios importantes y elementos de código para la versión Linux de RMS SDK.

Los siguientes fragmentos de código pertenecen a las aplicaciones de ejemplo *rms\_sample* y *rmsauth\_sample*. Para más información, vea [samples](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples) (ejemplos) en el repositorio de GitHub.

## <a name="scenario-access-protection-policy-information-from-a-protected-file"></a>Escenario: Acceso a información de la directiva de protección desde un archivo protegido

**Abre y lee un archivo protegido por RMS**
**Origen**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: tras obtener del usuario el nombre de un archivo, leer los certificados (vea *MainWindow::addCertificates*), configurar la devolución de llamada de autorización con el identificador de cliente y la URL de redireccionamiento, llamar a *ConvertFromPFile* (vea el siguiente código de ejemplo), y luego leer el nombre de la directiva de protección, la descripción y la fecha de validez del contenido.

**C++**:

    void MainWindow::ConvertFromPFILE(const string& fileIn,
        const string& clientId,
        const string& redirectUrl,
        const string& clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this->consent);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e)
    {
    AddLog("ERROR: ", e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    }
    inFile->close();
    outFile->close();
    }

**Crear un flujo de archivos protegidos**
**Origen**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: este método crea un flujo de archivos protegidos desde el flujo base pasado a través del método SDK (*ProtectedFileStream::Aquire*) que después se devuelve al llamador.

**C++**:

    shared_ptr<GetProtectedFileStreamResult>PFileConverter::ConvertFromPFile(
    const string           & userId,
    shared_ptr<istream>      inStream,
    shared_ptr<iostream>     outStream,
    IAuthenticationCallback& auth,
    IConsentCallback       & consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast<ResponseCacheFlags>(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) && (fsResult->m_status == Success) &&
      (fsResult->m_stream != nullptr)) {
    auto pfs = fsResult->m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs->Size();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## <a name="scenario-create-a-new-protected-file-using-a-template"></a>Escenario: Creación de un nuevo archivo protegido mediante una plantilla

**Protege un archivo con una plantilla seleccionada por el usuario**
**Origen**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: tras obtener del usuario el nombre de un archivo, leer los certificados (vea *MainWindow::addCertificates*) y configurar la devolución de llamada de autorización con el identificador de cliente y la URL de redireccionamiento, el archivo seleccionado se protege mediante la llamada a *ConvertToPFileTemplates* (vea el siguiente código de ejemplo).

**C++**:

    void MainWindow::ConvertToPFILEUsingTemplates(const string& fileIn,
                                              const string& clientId,
                                              const string& redirectUrl,
                                              const string& clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this->consent, this->templates);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
   catch (const rmsauth::Exception& e) { AddLog("ERROR: ", e.error().c_str()); outFile->close(); remove(fileOut.c_str()); } catch (const rmscore::exceptions::RMSException& e) { AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }


**Protege un archivo con una directiva creada a partir de una plantilla**
**Origen**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: se captura una lista de plantillas asociadas con el usuario y después se usa la plantilla seleccionada para crear una directiva que sirve para proteger el archivo.

**C++**:

    void PFileConverter::ConvertToPFileTemplates(const string           & userId,
                                             shared_ptr<istream>      inStream,
                                             const string           & fileExt,
                                             std::shared_ptr<iostream>outStream,
                                             IAuthenticationCallback& auth,
                                             IConsentCallback& /*consent*/,
                                             ITemplatesCallback     & templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos < templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**Protege un archivo con una directiva determinada**
**Origen**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: crea un flujo de archivos protegidos mediante la directiva especificada y luego protege el archivo.

**C++**:

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr<UserPolicy>   policy,
                                               shared_ptr<istream>      inStream,
                                               const string           & fileExt,
                                               std::shared_ptr<iostream>outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream->Size();
    
    inStream->seekg(0, ios::end);
    totalSize = inStream->tellg();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream->Flush();
    }
    


## <a name="scenario-protect-a-file-using-custom-protection"></a>Escenario: Protección de un archivo con protección personalizada

**Protege un archivo con protección personalizada**
**Origen**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: tras obtener del usuario el nombre de un archivo, leer los certificados (vea *MainWindow::addCertificates*), recopilar la información de derechos del usuario y configurar la devolución de llamada de autorización con el identificador de cliente y la URL de redireccionamiento, el archivo seleccionado se proyecta mediante la llamada a *ConvertToPFilePredefinedRights* (vea el siguiente código de ejemplo).

**C++**:

    void MainWindow::ConvertToPFILEUsingRights(const string            & fileIn,
                                           const vector<UserRights>& userRights,
                                           const string            & clientId,
                                           const string            & redirectUrl,
                                           const string            & clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog("ERROR: ", "Please fill email and check rights");
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this->consent,
      userRights);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e) {
    AddLog("ERROR: ", e.error().c_str());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }


**Crea una directiva de protección con unos derechos seleccionados por el usuario determinados**
**Origen**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**Descripción**: crea un descriptor de directiva y lo rellena con la información de derechos del usuario. Después, usa el descriptor de directiva para crear una directiva de usuario. Esta directiva se usa para proteger el archivo seleccionado mediante una llamada a *ConvertToPFileUsingPolicy* (esto se describe en una sección anterior de este tema).

**C++**:

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            & userId,
    shared_ptr<istream>       inStream,
    const string            & fileExt,
    shared_ptr<iostream>      outStream,
    IAuthenticationCallback & auth,
    IConsentCallback& /*consent*/,
    const vector<UserRights>& userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared<string>("https://client.test.app"));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name("Test Name");
    desc.Description("Test Description");
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## <a name="workerthread---a-supporting-method"></a>WorkerThread - un método auxiliar


El método *WorkerThread()* se invoca en dos de los escenarios de ejemplo anteriores (**Crear un flujo de archivos protegidos** y **Protege un archivo con una directiva determinada**) de la siguiente manera:

**C++**:

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));


**Método auxiliar, WorkerThread()**

**C++**:

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector<thread> threadPool;
    
    static void WorkerThread(shared_ptr<iostream>           stdStream,
                         shared_ptr<ProtectedFileStream>pStream,
                         bool                           modeWrite) {
    vector<uint8_t> buffer(4096);
    int64_t bufferSize = static_cast<int64_t>(buffer.size());
    
    while (totalSize - readPosition > 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition <= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream->seekg(offsetRead);
        stdStream->read(reinterpret_cast<char *>(&buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream->WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException("Error while writing data");
        }
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    } else {
      auto read =
        pStream->ReadAsync(&buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream->seekp(offsetWrite);
        stdStream->write(reinterpret_cast<const char *>(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    }
    }
    }


## <a name="scenario-rms-authentication"></a>Escenario: Autenticación de RMS

Los ejemplos siguientes muestran dos métodos de autenticación diferentes; obtener el token de oAuth2 de autenticación de Azure con la interfaz de usuario y sin la interfaz de usuario.
**Adquirir el token de autenticación de oAuth2 con la interfaz de usuario**
**Origen**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Paso 1**: cree un punto compartido del objeto **rmsauth::FileCache**.
Descripción: se puede establecer la ruta de acceso de caché o usar el valor predeterminado.

**C++**:

    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();


**Paso 2**: cree el objeto **rmsauth::AuthenticationContext**. Descripción: especifique el *URI de autoridad* de Azure y el objeto *FileCache*.

**C++**:

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**Paso 3**: llame al método **aquireToken** del objeto **authContext** y especifique los parámetros siguientes: Descripción:

-   *Recurso solicitado*: recurso protegido al que quiere acceder.
-   *Identificador único del cliente*: usualmente un GUID.
-   *URI de redireccionamiento*: URI que será redirigida una vez capturado el token de autenticación.
-   *Comportamiento de solicitud de autenticación*: si establece **PromptBehavior::Auto**, la biblioteca intenta usar la memoria caché y el token de actualización si es necesario.
-   *Id. de usuario*: nombre de usuario que aparece en la ventana del símbolo del sistema.

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**Paso 4**: obtenga el token de acceso de los resultados. Descripción: llame al método **result -> accessToken()**.

**Nota**  Cualquiera de los métodos de la biblioteca de autenticación puede generar **rmsauth::Exception**.

 
**Adquirir el token de autenticación de oAuth2 sin la interfaz de usuario**
**Origen**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**Paso 1**: cree un punto compartido del objeto **rmsauth::FileCache**. Descripción: se puede establecer la ruta de acceso de caché o usar el valor predeterminado.

**C++**:

    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();


**Paso 2**: cree el objeto **UserCredential**. Descripción: especifique las credenciales de *inicio de sesión de usuario* y *contraseña*.

**C++**:

    auto userCred = std::make_shared<UserCredential>("john.smith@msopentechtest01.onmicrosoft.com",
                                                 "SomePass");


**Paso 3**: cree el objeto **rmsauth::AuthenticationContext**. Descripción: especifique el *URI* de autoridad de Azure y el objeto *FileCache*.

**C++**:

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**Paso 4**: llame al método **aquireToken** del objeto **authContext** y especifique los siguientes parámetros:
-   *Recurso solicitado*: recurso protegido al que quiere acceder.
-   *Identificador único del cliente*: usualmente un GUID.
-   *Credenciales de usuario*: pase el objeto creado.

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**Paso 5**: obtenga el token de acceso de los resultados. Descripción: llame al método **result -> accessToken()**.

**Nota**  Cualquiera de los métodos de la biblioteca de autenticación puede generar **rmsauth::Exception**.
